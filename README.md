# Hadoop multi-node cluster with Ansible
Multi-server deployment Ambari and Ansible in AWS

## Version and Tools

Ubuntu 16.04 LTS
Ansible 2.3
Anbari 2.1.2.1

## Role Variables

  apt_cache_valid_time: 3600
  ambari_repo: http://public-repo-1.hortonworks.com/ambari/ubuntu14/2.x/updates/2.1.2.1/ambari.list


## Quick Start (Master)


1. Edit host file with the Public ip address of the instances and PEM key
2. Edit nodes-ip with the private ip address of the instances
   Ex.
   - hostname: ambari-server.local
     ip: x.x.x.x
   - hostname: ambari-node.local
     ip: x.x.x.x

3. run: ansible-playbook -i hosts play.yml


## Ports

8080 UI http

### Daemon Ports
8080
8040
8042


## Run blueprint Example

curl -H "X-Requested-By: ambari" -X POST -u admin:admin http://x.x.x.x:8080/api/v1/blueprints/multinode-hdp -d @cluster_configuration.json

curl -H "X-Requested-By: ambari" -X PUT -u admin:admin http://x.x.x.x:8080/api/v1/stacks/HDP/versions/2.3/operating_systems/ubuntu14/repositories/HDP-2.3 -d @repo.json

curl -H "X-Requested-By: ambari" -X PUT -u admin:admin http://x.x.x.x:8080/api/v1/stacks/HDP/versions/2.3/operating_systems/ubuntu14/repositories/HDP-UTILS-1.1.0.20 -d @hdputils-repo.json

curl -H "X-Requested-By: ambari" -X POST -u admin:admin http://x.x.x.x:8080/api/v1/clusters/multinode-hdp -d @hostmapping.json
