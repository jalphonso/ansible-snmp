This playbook demonstrates how to install the
minimum SNMPv3 configuration.

To run simply execute:
```ansible-playbook -i hosts site.yml -vv```

A diff of the config will be saved for each
device with a timestamp.

To test your device you can install snmp and run:
```
sudo apt install snmp
snmpget -v3 -u mysecretv3username -l authPriv \
-a SHA -A mysecretv3password -x AES \
-X mysecretv3password <DEVICE IP> \
1.3.6.1.2.1.1.1.0
```
