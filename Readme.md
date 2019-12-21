monitored_box
=============

Underlying ansible roles: `sa-prometheus-exporters`.  Check roles documentation for whole set of parameters to override.

Supported tags:

`sa_prometheus_exporters`

Supported parameters overrides:


```
```


Using with vagrant boilerplate (https://github.com/Voronenko/devops-vagrant-ansible-boilerplate)

```ruby

    config.vm.provision "monitored_box", type: "ansible" do |ansible|
        ansible.playbook = "deployment/provisioners/monitored_box/playbook.yml"
        ansible.galaxy_role_file = "deployment/provisioners/monitored_box/requirements.yml"
        ansible.galaxy_roles_path = "deployment/provisioners/monitored_box/roles"
        ansible.verbose = true
        ansible.groups = {
            "monitored_box" => [vconfig['vagrant_machine_name']]
        }
        # ansible.tags = ["sa_mysql"]
        ansible.extra_vars = {
            box_provider: "vagrant",
            env: "vagrant"
        }
    end
```

Using gilt

```yaml

  - git: https://github.com/oops-to-devops/monitored_box.git
    version: master
    files:
      - src: roles
        dst: provisioners/monitored_box/roles
      - src: Makefile
        dst: provisioners/monitored_box
      - src: Readme.md
        dst: provisioners/monitored_box
      - src: "*.yml"
        dst: provisioners/monitored_box
      - src: version.txt
        dst: provisioners/monitored_box
      - src: init_galaxy.sh
        dst: provisioners/monitored_box
      - src: provision_box.sh
        dst: provisioners/monitored_box
```


Example of mapping in ec2 dynamic inventory

```yaml
plugin: aws_ec2
# boto_profile: OPTIONAL_SPECIFY
regions:
  - us-east-1
  - us-east-2
  - us-west-1
  - us-west-2
filters:
  vpc-id: vpc-0ec210f7af56a4846
  tag:env: default
  tag:role:
    - proj
  tag:Project: proj

# keyed_groups may be used to create custom groups
strict: False
hostnames:
  - ip-address
groups:
  # Workaround to add hosts to the group k8s-master and k8s-node since the
  monitored_box: "'proj' == tags.role"
#  monitored_box: true
keyed_groups:
  # add hosts to tag_Name_Value groups for each Name/Value tag pair
  - prefix: tag
    key: tags
  - key: tags['role']
    prefix: role
  - key: tags['Name']
    prefix: host
  # create a group per region e.g. us_east_2
  #- key: placement.region
  #  prefix: region
compose:
  ansible_user: "'ubuntu'"
```
