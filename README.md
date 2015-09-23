vagrant-docker-compose
======================

Using Vagrant
-------------

Workflow

```bash
vagrant up
vagrant ssh
cd /vagrant; docker-compose logs
docker exec -it [container] /bin/bash --login
vagrant suspend
```

There are three ways to ask Vagrant to rebuild the VM.

```bash
# Run the provisioner without stopping the VM
vagrant provision
# Restart VM and re-provision
vagrant reload
# Create new VM 
vagrant destroy --force && vagrant up
```

Using Docker
------------

```bash
docker-compose up
docker-compose stop
docker-compose rm
```
