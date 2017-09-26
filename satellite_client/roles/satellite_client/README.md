# satellite_client

This role allows the registration of baremetal,virtual and cloud instances running Red Hat Enterprise Linux 5,6,7 against a Red Hat Satellite 6 server. The role gives you the option to register your hosts with or without puppet as a configuration management tool. It also gives you the ability to update the hosts to the latest patch level during registration. If you choose puppet as a configuration management tool you can add a hostgroup to the ansible run which will apply your puppet classes within that hostgroup during registration.  

## Requirements

>= ansible 2.1

You need to have a working Red Hat Satellite 6 server in place with an activation key allowing you to register with Satellite 6.
To be successful you need to add the following yum repos to the activationkey:

rhel-7-server-rpms  
rhel-7-server-satellite-tools-6.2-rpms

## Role Variables

Available variables are listed below, along with default values:

```
sat6_fqdn: https://satellite.bit63.net
admin_user: admin  
org: Bit63  
location: Winchester  
hostgroup: rhel7base or "false" if none  
activationkey: ak-Reg_To_Library_soe_no_puppet or "false" if none  
updatehost: "true" or "false"
```

## Dependencies

For the admin password you will need to generate a `vault_admin_pass` variable and place the variable 

```
admin_pass: "{{ vault_admin_pass }}" 
```

in the group_vars/all/vars file.  
This tells ansible to go look for the encrypted vault\_admin\_pass variable in the encrypted group\_vars/all/vault file. 

If you are running this from a roles/ directory specify the path to the vars and vault file in your playbook calling the sat6register role.  
 
```
vars_files:  
    - "roles/satellite_client/group_vars/all/vars"  
    - "roles/satellite_client/group_vars/all/vault"  
```


## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - { role: satellite_client, sat6_fqdn: https://sat6ldo.rdu.salab.redhat.com }

## License

GPLv3

## Author Information
This role was created in 2016 by Laurent Domb, and modified by Peter McGowan
