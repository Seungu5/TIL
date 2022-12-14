# 조건문
>https://docs.ansible.com/ansible/latest/user_guide/playbooks_conditionals.html#basic-conditionals-with-when 
>https://docs.ansible.com/ansible/latest/user_guide/playbooks_tests.html#playbooks-tests
>https://docs.ansible.com/ansible/latest/user_guide/playbooks_filters.html#playbooks-filters

작업에서 `when` 키워드 사용, 조건을 정의 `test`, `filter` 사용

> 조건 정의 시 `{{ }}` 사용 하지 않는다.

``` yaml
- hosts: 192.168.100.11
  vars:
    switch: "on"
  tasks:
    - debug:
        msg: "hello switch on"
      when: switch == "on"
    - debug:
        msg: "hello switch off"
      when: switch == "off"
```
![](./img/09_1.png)

조건문에 많이 사용하는 팩트 변수

| https://docs.ansible.com/ansible/latest/user_guide/playbooks_conditionals.html#commonly-used-facts
- ansible_facts["distribution"]
- ansible_distribution

``` yaml
- hosts: wp
  tasks:
    - debug:
        msg: "hello CentOS"
      when: ansible_facts["distribution"] == "CentOS"
    - debug:
        msg: "hello Ubuntu"
      when: ansible_facts["distribution"] == "Ubuntu"
```
![](./img/09_2.png)

![](./img/09_3.png)