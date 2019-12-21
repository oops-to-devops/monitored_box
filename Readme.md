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

