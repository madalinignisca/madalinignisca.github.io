---
layout: post
title:  "How to use Keepalived? v1"
date:   2024-09-25 17:00:00
categories: [howto,linux,ha]
tags: [keepalived,pgbouncer,postgresql,cluster,tpa,repmgr]
---

The last few days I experimented with [TPA - Trusted Postgresql Architect](https://www.enterprisedb.com/products/trusted-postgres-architect-tpa) and ended up with a desired state of some Postgresql clusters, using streaming replication.

The architecture is prety simple and classic:

* 1 Primary and 1 or more Replicas
* 1 Backup server
* Each Postgresql node runs repmgr and pgbouncer

Pgbouncer will use the current Primary as target, and repmgr, if Primary goes down, will promote first selected Replica as new Primary.

I chosen repmgr, as TPA can do upgrades on cluster, as for M1 architecture at the time of writing this article, using Patroni replication manager will fail TPA to upgrade the cluster, and I don't want to avoid bugs and especially security fixes for all software involved.

But, for us, using TPA and Postgresql for free, this comes with a limit. Repmgr is setup only to promote new primary and tell the rest of replicas to follow new primary. It will not reconfigure pgbouncer.

So here comes in action, Keepalived. This is the first version, and an update will be linked here and mention if this might not work perfect.

BTW, I use Debian, but you can adapt easy on your favorite distribution if using some other package manager. Also I asume you use a distribution nor older then 3 years, I mean, you don't run on Centos 7, right?

BTW again, I do setup using LUKS all volumes for postgresql and barman, which makes default to not start postgresql on many situations that could lead to many nodes thinking they are primary and get the cluster not usable. If you don't use this, disable start on boot for postgresql, in case of a unknown reboot of the server, as you will endup with 2 healthy servers thinking both are primary. If data was written to new promoted Primary, the first one will win the VIP and data will diverge on nodes. When using TPA, you must use TPA for all maintenance actions and try to avoid any manual intervention in any node.

Keepalived, allows us to have a VIP (Virtual IP address) that can be moved from node to node. It also supports custom check scripts and custom notification scripts.

Basically, I'm going check which one is the primary postgresql node and reconfigure pgbouncer when that changes, monitor status of postgresql, so if it goes down, i'll turn off also pgbouncer, and will ensure to have the node with primary, alive, have the highest prio and own the VIP.

Pgbouncer is not critical to run on replicas. Applications are supposed to talk with Postgresql by using the VIP, and not the normal IP addresses of the servers.

The disaster scenario would be no postgresql node being healthy and keepalived having no candidate for VIP and set any corrections in pgbouncer. But with proper monitoring, I should be able to take action before the full cluster goes down.

*You do monitoring right?*

Let's dive.

First, install on all nodes Keepalived: `apt install keepalived`

Next, let's prepare the configuration. On each Postgresql node, add in order of nodes the following configurations. If you have only 1 primary and one replica, use the first 2 examples, if more then 3, adapt for 4th and others.

Place this on 1st server in `/etc/keepalived/keepalived.conf`

```ini
vrrp_script chk_postgresql {
    script "/etc/keepalived/check_postgresql.sh"
    interval 5           # Check every 5 seconds
    weight -75           # Decrease priority by 10 if PostgreSQL is unhealthy
}

vrrp_script chk_primary {
    script "/etc/keepalived/check_primary.sh"
    interval 5
    weight -50
}

vrrp_instance VI_1 {
    state MASTER                     # Node starts as Master
    interface eth0                   # Network interface
    virtual_router_id 100            # VRRP group identifier (must match Primary node)
    priority 175                     # High priority for the master node
    advert_int 1                     # Advertisement interval (in seconds)
    virtual_ipaddress {
        192.168.1.100                # This is the VIP that clients will connect to
    }

    track_script {
        chk_postgresql               # Track the PostgreSQL script
        chk_primary                  # check if we are replica and healthy
    }

    authentication {
        auth_type PASS
        auth_pass securepassword      # Simple password for VRRP (must match Primary node)
    }

    notify_master "/etc/keepalived/notify_master.sh"
    notify_backup "/etc/keepalived/notify_backup.sh"
    notify_fault  "/etc/keepalived/notify_fault.sh"
}
```

Place this on 2nd server in `/etc/keepalived/keepalived.conf`

```ini
vrrp_script chk_postgresql {
    script "/etc/keepalived/check_postgresql.sh"
    interval 5           # Check every 5 seconds
    weight -75           # Decrease priority by 10 if PostgreSQL is unhealthy
}

vrrp_script chk_primary {
    script "/etc/keepalived/check_primary.sh"
    interval 5
    weight -50
}

vrrp_instance VI_1 {
    state BACKUP                     # Node starts as Backup
    interface eth0                   # Network interface
    virtual_router_id 100            # VRRP group identifier (must match Primary node)
    priority 150                     # High priority for the master node
    advert_int 1                     # Advertisement interval (in seconds)
    virtual_ipaddress {
        192.168.1.100                # This is the VIP that clients will connect to
    }

    track_script {
        chk_postgresql               # Track the PostgreSQL script
        chk_primary                  # check if we are replica and healthy
    }

    authentication {
        auth_type PASS
        auth_pass securepassword      # Simple password for VRRP (must match Primary node)
    }

    notify_master "/etc/keepalived/notify_master.sh"
    notify_backup "/etc/keepalived/notify_backup.sh"
    notify_fault  "/etc/keepalived/notify_fault.sh"
}
```

Place this on 3rd server in `/etc/keepalived/keepalived.conf`

```ini
vrrp_script chk_postgresql {
    script "/etc/keepalived/check_postgresql.sh"
    interval 5           # Check every 5 seconds
    weight -75           # Decrease priority by 10 if PostgreSQL is unhealthy
}

vrrp_script chk_primary {
    script "/etc/keepalived/check_primary.sh"
    interval 5
    weight -50
}

vrrp_instance VI_1 {
    state BACKUP                     # Node starts as Backup
    interface eth0                   # Network interface
    virtual_router_id 100            # VRRP group identifier (must match Primary node)
    priority 125                     # High priority for the master node
    advert_int 1                     # Advertisement interval (in seconds)
    virtual_ipaddress {
        192.168.1.100                # This is the VIP that clients will connect to
    }

    track_script {
        chk_postgresql               # Track the PostgreSQL script
        chk_primary                  # check if we are replica and healthy
    }

    authentication {
        auth_type PASS
        auth_pass securepassword      # Simple password for VRRP (must match Primary node)
    }

    notify_master "/etc/keepalived/notify_master.sh"
    notify_backup "/etc/keepalived/notify_backup.sh"
    notify_fault  "/etc/keepalived/notify_fault.sh"
}
```

Next let's add the check scripts.

check_postgresql.sh:

```bash
#!/bin/bash

# Check if PostgreSQL is accepting connections
pg_isready -q -h 127.0.0.1 -p 5432

# If PostgreSQL is running, exit with 0
if [ $? -eq 0 ]; then
    exit 0
else
    exit 1
fi
```

With this script, it means Postgresql is not even running. We want to take it to lowest prio, right?

So, if postgresql service is running (we could have used systemd's is-active check, but that does not really mean postgresql is healthy), we want to know if it is primary. I'm doing this check and want to have healthy postgresql primary to have highest prio, so the server gets the VIP. This way, the primary server will always have the VIP.

check_primary.sh:

```bash
#!/bin/bash

# Exit with 1 if postgresql is not running
if ! systemctl is-active --quiet postgresql; then
    exit 1
fi

# Check if the standby mode or recovery state is active
if [ "$( su - postgres -c 'psql -t -c "SELECT pg_is_in_recovery();"')" = " f" ]; then
  # Primary server
  exit 0
else
  # Replica server
  exit 1
fi
```

Place it in all nodes in `/etc/keepalived/` and run `chmod +x /etc/keepalived/check*` to make both executables.

So, we will get penality if we are not primary. The script will return 1 also when check fails.

Now, because we decided default MASTER and priorities, this values must be changed in such a way that healthy primary always has highest primary. The default, is our ideal case where server 1 would be healthy and primary, so a value of 175 sounds good. 

If Postgresql is not healthy, gets a penality of 75. If it is alive, but not primary, gets a penality of 50. so, 175, 100 as replica, 50 if broken.

The second, gets a priority of 150, and we penalize the same if has issues, so it can end up with 150 if primary, 75 alive and replica, and 25 points if broken.

In case we have a 3rd one, it gets a prio of 125. If it is healthy and primary, the others will have max 100, repectively 75 max points. If is healthy replica, gets 75 points. If all dead, gets 0.

So, prio will make the healthy primary always have the VIP.

What's next?

We have this other scripts, that we run depending on state.

We want to run pgbouncer when the state is MASTER (will they rename state in the future from this ugly term?). But if we are not, we don't want pgbouncer to run.

So let's take a pick at our 3 extra scripts and place them in `/etc/keepalived/` and run after `chmod +x /etc/keepalived/notify*`

When a MASTER is promoted:

notify_master.sh
```bash
#!/bin/bash

# Let's log to syslog, you do use it, right? (journald has you covered)
logger "This node has become the MASTER. Promoting this node to PostgreSQL primary."

# let's make sure pgbouncer connects to localhost
echo "* = host=127.0.0.1 port=5432 auth_user=pgbouncer_auth_user" > /etc/pgbouncer/pgbouncer.databases.ini

# ensure pgbouncer is running
systemctl restart pgbouncer
```

When it becomes replica

notify_backup.sh
```bash
#!/bin/bash

# log to beloved syslog
logger "This node has become the BACKUP. Demoted to standby."

# let's stop pgbouncer it's not a big problem
systemctl stop pgbouncer
```

When something gets wrong

notify_fault.sh
```bash
#!/bin/bash

# if you are able, now you should use an sms api and spam your phone
logger "Keepalived is in FAULT state. Something went wrong with this node."
```

Enable and run keepalived on all servers and enjoy.

Probably, this scripts could be enhanced more, achieving same results.

My current concerns are only what happens when a postgresql that was primary, restarts again, situation that should not be possible when manual maintenance is not happening.

*This article will be updated after further tests are completed*
