## `ulimit` release

A BOSH release which mimics the function of
[ulimit](http://tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/x4733.html)

### 0. Usage

Upload release to director.

Set properties in manifest:

```
properties:
  nofile:
    soft: 16384
    hard: 16384
```

### Inner workings & Bugs

Only works for the ulimit property "open files".

Creates `/etc/security/limits.d/62-ulimit.conf`.

Dynamically adjust monit's "Max open files".

This runs as a [pre-start](https://bosh.io/docs/pre-start.html) script.

Fixes: `Accept error: accept tcp [::]:80: accept4: too many open files`.

Defaults to 16384/16384 soft/hard limit for all users.

This was tested on Ubuntu and CentOS stemcells.
