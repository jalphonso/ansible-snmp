This playbook demonstrates how to install the
minimum SNMPv3 configuration on a Junos device.

To run, update credentials in group_vars/all.yml,
list of hosts in site.yml, and execute:
```
ansible-playbook -i hosts site.yml
```

A diff of the config will be saved for each
device with a timestamp.

To test your device you can install snmp and run:
```
sudo apt install snmp
snmpget -v3 -u mysecretv3username -l authPriv \
-a MD5 -A mysecretv3password -x AES \
-X mysecretv3password <DEVICE IP> \
1.3.6.1.2.1.1.1.0
```

This playbook deploys the config safely to the
device by first showing you the diff without
committing the changes and giving you the
option to continue or abort. Then it
will perform a commit confirm, check to see
the device is still reachable, and then
issue the final commit. The SNMP credentials
that you provide are stored temporarily in
a temp directory and cleaned up immediately
after each communication to the device has
completed.

Lastly, there is an additional role that
is responsible for adding the device to
Junos Space via the REST API. If you want
to skip this run the playbook with
the skip-tags argument for space and these tasks
will be skipped. Example below:
```
ansible-playbook -i hosts --skip-tags space site.yml
```

NOTE: If planning on running playbooks in Ansible
Tower vars_prompt should be removed. Set variables
in group_vars/all.yml instead and fill out in Tower
