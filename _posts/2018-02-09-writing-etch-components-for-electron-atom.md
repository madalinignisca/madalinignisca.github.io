---
layout: post
title:  "How to write Etch components for Electron and Atom"
date:   2018-02-09 12:53:00
categories: electron
---

_Article in progress..._

[*Etch*](https://github.com/atom/etch) is a very light virtual-dom implementation intended to be used in Electron
apps and Atom Editor packages.

It's much more lightweight compared to [*React*](https://reactjs.org), as it's main target is to build minimal
components that support updating the components and basic children support.

If you're in deep need for something more full featured, you should look into using React, like many packages for
Atom are using React, as for example the Git/Github core package.

For most of the usecases I found *Etch* as really offering a great start, as I'm not into *React* (yet) and as it
is covering all basic needs to render information, I considered to use it for my projects for the much faster
and easier learning curve of it.

...

Must have at the beggining of the component file:
```
"use babel"
/** @jsx etch.dom */
```
