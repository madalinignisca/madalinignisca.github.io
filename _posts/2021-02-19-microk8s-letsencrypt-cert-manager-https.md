---
title: Let's encrypt certificates, HTTPS on MicroK8s
type: post
date: 2021-02-19 13:30
categories: wpk8s
---

Took me two days, well, not full days, but two rounds of my 1h hour per
day to work on the WordPress on MicroK8s book, to figure out how to get
Let's encrypt working with default setup of MicroK8s and provision a real
certificate for a real domain I use.

First, examples from [cert-manager](https://cert-manager.io/docs/) did not
work out of the box, but were perfect to get started.

1st, MicroK8s by enabling dns and ingress addons, simply will give you a well
configured Nginx ingress controller and a compatible expected internal dns for network communication between pods.

To install cert-manager simply running:
`kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.2.0/cert-manager.yaml`
worked, and if you follow along, make sure to look at current latest tag and
replace `v1.2.0` with what is right now.

*If you use RBAC on MicroK8s, at this moment I have not yet experimented as
it is not in my scope for the moment, but when I will experiment with it, I
will update on this.*

Next, you need to setup Issuers, and for MicroK8s the example is slightly
different from the official docs:

> Make sure you will edit according to your needs the **email**,
> **privateKeySecretRef/name**!!!

```yaml
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: letsencrypt-staging
spec:
  acme:
    # You must replace this email address with your own.
    # Let's Encrypt will use this to contact you about expiring
    # certificates, and issues related to your account.
    email: user@example.com
    server: https://acme-staging-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      # Secret resource that will be used to store the account's private key.
      name: example-issuer-account-key
    # Add a single challenge solver, HTTP01 using nginx
    solvers:
    - http01:
        ingress:
          class: public
```

The difference is in the *class*, which needs to be public and not nginx. I
guess that nginx is default on official installation of nginx ingress and
MicroK8s is configuring it to public. I noticed that in the logs of
the nginx ingress pod, the first lines. Also the other difference is in
the *kind* which on MicroK8s only ClusterIssuer worked, and for the official
Issuer example in documentation, simply errors that ingress is unknown for http01.
Not sure on the error, but other examples in the official documentation
do use ClusterIssuer, so it might need some updates.

The above example will configure it for Let's encrypt staging so you can
experiment without getting your domain/subdomain blocked while experimenting.
To go for production, create one for production. You can and should have
both staging and production Issuers.

Here the production equivalent you need to adapt and apply:

```yaml
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: letsencrypt-prod
spec:
  acme:
    # You must replace this email address with your own.
    # Let's Encrypt will use this to contact you about expiring
    # certificates, and issues related to your account.
    email: user@example.com
    server: https://acme-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      # Secret resource that will be used to store the account's private key.
      name: example-issuer-account-key
    # Add a single challenge solver, HTTP01 using nginx
    solvers:
    - http01:
        ingress:
          class: public
```

For the Ingress definition, all you need to do is add the annotation like:
`cert-manager.io/cluster-issuer: letsencrypt-staging` or
`cert-manager.io/cluster-issuer: letsencrypt-prod`. Use staging to test
change to prod if all is ok for you.

Here is an example for a basic service I use for healthcheck of my home
server:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: healthcheck-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$1
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
spec:
  tls:
  - hosts:
    - healthcheck.home.madalin.me
    secretName: healthcheck-home-tls
  rules:
    - host: healthcheck.home.madalin.me
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: healthcheck
                port:
                  number: 8080
```

*The service can be any web server that responds with HTTP 200 and any
content you wish*

Major benefit: it will self renew the cert with 15 days before expiration.

Also, you can use cert-manager to manage other types of certificates and
has some Cloudflare integration which I want to explore next.

{% include wpk8s-book-promo.md %}
