# 구성 파일
| https://docs.ansible.com/ansible/latest/reference_appendices/config.html

설정파일 위치
1. `ANSIBLE_CONFIG` (environment variable if set)
```
touch /tmp/ans.cfg
export ANSIBLE_CONFIG=/tmp/ans.cfg
ansible --version

unset ANSIBLE_CONFIG
ansible --version
```

2. `ansible.cfg` (현재 작업 디렉토리)
3. `~/.ansible.cfg` (홈 디렉토리)
4. `/etc/ansible/ansible.cfg` : 기본 설정 파일