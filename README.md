
# Setup Redmine on Docker in CentOS via Vagrant

## Fully automated

1. Install [VirtualBox](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html) and [Vagrant](https://www.vagrantup.com/downloads.html).
2. Run `vagrant` and setup preconfigured CentOS7.
   ```console
   $ vagrant up
   ```
3. Then initializing process begins.
4. `docker-disk-volume.vdi` is a disk file vagrant created and has been added to the original VM as a part of LVM. DO NOT REMOVE.
5. After all, open http://localhost:3000.
