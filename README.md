# LXC/LXD Cheatsheet

# Set unprivileged container to privileged
```bash
lxc config set $CONTAINER_NAME security.privileged true
```

# Set container to support NESTING
```bash
lxc config set $CONTAINER_NAME security.nesting true
```

# Set container to share directory with the host
```bash
lxc config device add $CONTAINER_NAME $SOMENAME disk source="/dir_from_host" path="/home/user/dir_on_container"
```