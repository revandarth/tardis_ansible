
The repository is a demonstration of ansible playbooks for deploying the following open source [http_collector_go](https://github.com/Comcast/HTTP-Collector) service on both AWS ec2 server and EKS (kubernetes) cluster.


# Ansible

## ~/.ansible.cfg example
```
[defaults]
pipelining = True
forks = 20
become = True
vault_password_file = ~/.ansible_vault_password

[ssh_connection]
scp_if_ssh=True
```

## Installing the development certificate authority onto your desktop

```
sudo security add-trusted-cert -d -r trustRoot -k roles/common/files/ssl/ca.cert.pem
```

## Anisble Examples

### Do an operation across all inventories

_This could be useful if you need to do a mass operation._

```
$ for inventory in `find inventory -maxdepth 1 -mindepth 1` ; do ansible -i $inventory consul -b -m shell -a 'yum update -y' ; done
```

for INV in `find inventory -maxdepth 1 -mindepth 1` ; do ansible -i "${INV}" consul -b -m shell -a '' ; done

_Update across a region._

```
$ ansible -i hosts/tardis/stage/hosts all -b -m shell -a 'yum clean all ; rm -rf /var/cache/yum ; yum makecache ; yum update -y'
```


Ansible command to deploy in prod in east region 

```
ansible-playbook -i hosts/tardis/green -l hc-east -e site_region=e1 hc-go.yml -t deploy
```
