monitored_box
=============

Underlying ansible roles: `sa-prometheus-exporters`.  Check roles documentation for whole set of parameters to override.

Supported tags:

`sa_prometheus_exporters`

Supported parameters overrides:


```
```


Using with vagrant boilerplate (https://github.com/Voronenko/devops-vagrant-ansible-boilerplate)

```

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
