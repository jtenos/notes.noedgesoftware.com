---
layout: home
---
The syntax for making git checkout "remote-ready" is rather easy: simply add the "--track" flag and the remote branch's ref like in the following example:

```
$ git checkout --track origin/newsletter
```

Branch newsletter set up to track remote branch newsletter from origin.
Switched to a new branch 'newsletter'

Based on the remote branch "origin/newsletter", we now have a new local branch named "newsletter".

Note that, by default, Git uses the same name for the local branch. Being a good convention, there's rarely the need to change this.