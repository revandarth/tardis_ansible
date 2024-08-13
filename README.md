
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


Ansible command to deploy http collector in production aws east region 

```
ansible-playbook -i hosts/tardis/green -l hc-east -e site_region=e1 hc-go.yml -t deploy
```
