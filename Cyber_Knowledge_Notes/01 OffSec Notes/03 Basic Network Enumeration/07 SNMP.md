If you would like to install `snmpcheck` on your local Linux box, consider the following commands.

```
git clone https://gitlab.com/kalilinux/packages/snmpcheck.git
```

```
cd snmpcheck/
```

```
gem install snmp
```

```
chmod +x snmpcheck-1.9.rb
```

## query servers related to SNMP

```
snmpcheck.rb 10.10.71.103 -c COMMUNITY_STRING
```