#### To check if deployment or namespace already exists
` ansible-playbook -i hosts/tardis/red/hosts -l eks-build-server-e1 -e "site_color=red site_role_name=hc site_region=e1 site_project=tardis change_cause='app verions or change description'" -t precheck eks-hc.yml`

#### To deploy the application use below command
` ansible-playbook -i hosts/tardis/red/hosts -l eks-build-server-e1 -e "site_color=red site_role_name=hc site_region=e1 site_project=tardis change_cause='app verions or change description'" -t deploy eks-hc.yml`

#### OR with out change_cause, version will be used as change_cause
` ansible-playbook -i hosts/tardis/red/hosts -l eks-build-server-e1 -e "site_color=red site_role_name=hc site_region=e1 site_project=tardis" -t deploy eks-hc.yml`

#### To rollback the deployment to previous version
` ansible-playbook -i hosts/tardis/red/hosts -l eks-build-server-e1 -e "site_color=red site_role_name=hc site_region=e1 site_project=tardis" -t rollback eks-hc.yml`

#### Rollback the deployment to specific version
` ansible-playbook -i hosts/tardis/red/hosts -l eks-build-server-e1 -e "site_color=red site_role_name=hc site_region=e1 site_project=tardis revision=3" -t rollback eks-hc.yml`


#### Update the deployment traffic
` ansible-playbook -i hosts/tardis/red/hosts -l eks-build-server-e1 -e "site_color=red site_role_name=hc site_region=e1 site_project=tardis prod_weight=100 canary_weight=0" -t update_traffic eks-hc.yml`


#### Update the deployment hpa
` ansible-playbook -i hosts/tardis/red/hosts -l eks-build-server-e1 -e "site_color=red site_role_name=hc site_region=e1 site_project=tardis min_replicas=0" -t update_hpa eks-hc.yml`

#### To delete the deployment
` ansible-playbook -i hosts/tardis/red/hosts -l eks-build-server-e1 -e "site_color=red site_role_name=hc site_region=e1 site_project=tardis" -t deletedeployment eks-hc.yml`


### ansible command to remove application from gslb, dns name will be taken from eks-common.yml based on app name and site_color
`ansible-playbook -i hosts/tardis/red/hosts -e "site_region=e1 site_color=red app_name=hc" -t remove_dns  eks-route53.yml `

### ansible command to create application gslb, dns name will be taken from eks-common.yml based on app name and site_color
`ansible-playbook -i hosts/tardis/red/hosts -e "site_region=e1 site_color=red app_name=hc" -t create_dns  eks-route53.yml `
