## Local Port Forwarding

E.g. Accessing an online server's database (MySQL, Postgres, Redis, etc.) using a fancy UI tool from your laptop.

```
ssh -L [local_addr:]local_port:remote_addr:remote_port [user@]sshd_addr
```

The `-L` flag indicates we're starting a _local port forwarding_.

What it actually means is:

- On your machine, the SSH client will start listening on `local_port` (likely, on localhost).
- Any traffic to this port will be forwarded to the `remote_private_addr:remote_port` on the machine you SSH-ed to.

![[Pasted image 20260116115242.png]]
---
## Remote Port Forwarding

Expose a local service to the outside world, e.g. exposing a dev service from your laptop to the public Internet for a demo.

```
ssh -R [remote_addr:]remote_port:local_addr:local_port [user@]gateway_addr
```

The `-R` flag indicates we're starting a _remote port forwarding_.

![[Pasted image 20260116115253.png]]