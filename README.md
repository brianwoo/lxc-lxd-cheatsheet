# LXC/LXD Cheatsheet

# Add user to lxd
```bash
usermod -aG lxd $USER
```

# Setup LXD
```bash
lxd init
# use dir for storage backend
# create network bridge
```

# Show LXC storage directory (show where all the images stored.)
```bash
lxc storage list
```

# Show all the remote repositories
```bash
lxc remote list
```

# Images
```bash
# Show all the images already downloaded on the local machine
lxc image list

# show images available from "images" repository
lxc image list images:

# Search all Alma Linux images available for download
lxc image list images:alma
```

# Start / create a container from an image
```bash
lxc launch ubuntu:20.04   # with random name
lxc launch almalinux/9 almaDev  # almaDev is the name of the container
```

# Delete a container
```bash
lxc stop $CONTAINER_NAME
lxc delete $CONTAINER_NAME
```

# List all the created containers
```bash
lxc list
```

# Move one container to another machine / Rename a container
```bash
lxc move $CONTAINER_NAME new-name  # rename container to new-name
```

# Login to the container
```bash
lxc exec $CONTAINER_NAME bash   # login as root
lxc exec $CONTAINER_NAME su - ubuntu   # login as user ubuntu
```

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
lxc config device add $CONTAINER_NAME $SOMENAME disk \
  source="/dir_from_host" \
  path="/home/user/dir_on_container"
```

# Fix LXC containers that lost outgoing networking connection
```bash
for ipt in iptables iptables-legacy ip6tables ip6tables-legacy; \
  do $ipt --flush; $ipt --flush -t nat; $ipt --delete-chain; $ipt --delete-chain -t nat; \
  $ipt -P FORWARD ACCEPT; $ipt -P INPUT ACCEPT; $ipt -P OUTPUT ACCEPT; \
done
systemctl reload snap.lxd.daemon 
```
