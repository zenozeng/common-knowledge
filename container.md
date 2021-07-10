# Container

## Docker

- Linux Namespaces (PID, Mount, IPC, Network, User)
- cgroups
- change root

### Storage driver

- https://docs.docker.com/storage/storagedriver/overlayfs-driver/
- https://docs.docker.com/storage/storagedriver/btrfs-driver/
- https://docs.docker.com/storage/storagedriver/aufs-driver/

Note: The overlay and overlay2 drivers are supported on xfs backing filesystems, but only with d_type=true enabled.

## References

- 深入剖析 Kubernetes
