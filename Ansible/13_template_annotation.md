# 탬플릿 주석

`ansible.cfg`
```
[defaults]
ansible_managed = Ansible managed: {file} modified on %Y-%m-%d %H:%M:%S by {uid} on {host}
```

`templates/port.cnf.j2`
```
{{ ansible_managed | comment }}
[mysqld]
port={{ database["svc_port"] }}
```

> 경고의 목적