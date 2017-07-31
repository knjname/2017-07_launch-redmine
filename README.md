
# Setup Redmine on Docker in CentOS 7.3 via Vagrant

1. Install [VirtualBox](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html) and [Vagrant](https://www.vagrantup.com/downloads.html).
2. Run `vagrant up`.
   ```console
   $ vagrant up
   ```
3. Then initializing vbox process gets started.
4. A disk image file `docker-disk-volume.vdi` (up to 50GiB) will be created. This has been mounted to `/opt/docker`. DO NOT REMOVE.
5. After all initialization process finished, open http://localhost:3000. There is a Redmine. (`admin`/`admin123`)

## Resources

* https://github.com/sameersbn/docker-redmine

## License

MIT License
