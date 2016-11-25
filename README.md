# ansible-cloudfoundry

Cloud Foundry resource automation using Ansible

Have a look at the file:
https://github.com/SpringerPE/ansible-cloudfoundry/blob/master/inventory/group_vars/cf.yml
to see how to define the resources: feature flags, domains, security groups, quotas,
environment variables, users, organizations and spaces.

You can manage different Cloud Foundry environments by using inventory
files: https://github.com/SpringerPE/ansible-cloudfoundry/blob/master/inventory/cf.ini

Once CF credentials are defined in the inventory and the resources in the manifest,
just run ansible:

```
ansible-playbook -i inventoy/cf.ini cf.yml
```


## Components

### `library`

Set of Ansible modules to manage Cloud Foundry configuration entities,
not aimed to manage apps, routes, service brokers, etc.

Current available modules make possible to manage:

* **cf_config**: Environment variables, feature flags and default security groups.
* **cf_domain**: Private (with owner/shared organizations) and shared domains
* **cf_org**: Organizations (and user roles: user, manager, auditor and billing_manager)
* **cf_space**: Spaces (and user roles: user, manager, auditor)
* **cf_quota**: Organization and space Quotas
* **cf_secgroup**: Security groups
* **cf_secgroup_rule**: Security group rules
* **cf_user**: Manage CF users via UAA
* **cf_org_facts**: Get facts from a CF Org or Space

They depend on https://github.com/SpringerPE/python-cfconfigurator ,
just install it via pip.

```
pip install -r requirements.txt
```

For examples, have a look at `examples` folder.


### `role`

Ansible role which makes use of the previous modules to perform a set
of tasks to defice CF resources as described in the manifest.


### `inventory`

Folder with the variables needed to set-up on each CF environment.
Have a look at the [Readme in the folder](https://github.com/SpringerPE/ansible-cloudfoundry/blob/master/inventory/Readme.md), to see how to operate.


### `cf.yml`

Ansible playbook to run.

```
ansible-playbook -i inventory/test.ini cf.yml
```



## Author

José Riguera López, jose.riguera@springer-sbm.com

SpringerNature Platform Engineering
