# 변수
## 변수 정의 및 참조
``` yaml
template:
  src: foo.cfg.j2
  dest: '{{ remote_install_path }}/foo.cfg'
  name: '{{ abc }}'
  dest: '{{ abc }}/abc.com'
  dest: '{{ abc }}'/abc.com #문법 오류
```
``` yaml
- hosts: 192.168.100.11
  vars:
    msg: hello world
    
  tasks:
    - debug:
        var: msg
    - debug:
        msg: '{{ msg }} korea'
```
``` yaml
- hosts: 192.168.100.11
  vars:
    msg: hello world
    web:
      message: hello web
    fruits:
      - apple
      - banana

  tasks:
    - debug:
        msg: '{{ msg }} korea'
    - debug:
        msg: "{{ web['message'] }}"
        #msg: '{{ web["message"] }}' O
        #msg: '{{ web['message'] }}' X
    - debug:
        msg: '{{ fruits[0] }} {{ fruits[1] }}'
```

![ansible_version](./img/07_1.png)

## 등록 변수
등록: registered variable
``` yaml
- hosts: 192.168.100.11

  tasks:
    - apt:
        name: apache2
        state: installed
      register: apt_result #등록 변수

    - debug:
        var: apt_result
    - debug:
        var: apt_result["rc"]
```

## 변수 정의 위치
- 플레이북
- 인벤토리
- 외부 참조 파일
- 역할
- 명령 -e 옵션

### 플레이북에서 변수 정의
**vars**
``` yaml
- hosts: a
  vars:
    message: hello
```

**vars_prompt**
``` yaml
- hosts: 192.168.100.11
  vars_prompt:
    - name: username
      prompt: What is your username?
      private: no

    - name: password
      prompt: What is your password?

  tasks:
    - debug:
        msg: 'Logging in as {{ username }}, password is {{ password }}'
```
| 참조: https://docs.ansible.com/ansible/latest/user_guide/playbooks_prompts.html#interactive-input-prompts

**vars_files**
``` yaml
- hosts: a
  vars_files:
    - vars.yaml

  tasks:
    - debug:
        var: msg
```

`vars.yaml`
``` yaml
msg: hello world
```

### 인벤토리에서 변수 정의
| 변수의 미치는 범위 특정 호스트 또는 그룹에게 영향을 줌
``` ini
[nodes]
192.168.100.11 msg=seoul
192.168.100.12 msg=busan

[nodes:vars]
message="hello world"
```

``` yaml
- hosts: nodes
  tasks:
    - debug:
        var: msg
    - debug:
        var: message     
```

### 명령에서 변수 정의
``` bash
ansible-playbook test.yaml -e msg=korea
```

## 변수의 우선순위
| https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#understanding-variable-precedence

내림차순
- 인벤토리 변수
- 플레이 vars
- 플레이 vars_prompt
- 플레이 vars_files
- 명령 -e, --extra-vars 높음

## 변수의 범위
- 글로벌: 명령의 -e
- 플레이: vars, vars_files, vars_prompt
- 호스트: 인벤토리 변수

## 필터
변수에서 필요한 내용만 취득 변수에서 가공/형식변경

| https://docs.ansible.com/ansible/latest/user_guide/playbooks_filters.html
```
{{ msg | filter }}
```
``` yaml
- hosts: 192.168.100.11
  vars:
    pwd: P@ssw0rd
  tasks:
    - user:
        name: devops
        password: "{{ pwd | password_hash('sha512', 65534 | random(seed=inventory_hostname) | string) }}"
        state: present
```

## 팩트 변수
`setup` 모듈에 의해 수집(하드웨어, OS) 되는 호스트의 변수
플레이북 실행 항상 첫 작업 `gathering facts` 작업에 의해서 수집

``` yaml
- hosts: 192.168.100.11
  gather_facts: no
```

## 특수 변수
| https://docs.ansible.com/ansible/latest/reference_appendices/special_variables.html

- groups
- hostvars
- inventory_hostname
- ...

## 템플릿
jinja 템플릿
| https://jinja.palletsprojects.com/en/2.10.x/

``` yaml
- hosts: 192.168.100.11
  vars:
    message: korea
  tasks:
    - copy:
        src: origin.txt
        dest: /tmp/copy.txt
    - template:
        src: origin.txt
        dest: /tmp/template.txt
```

`origin.txt`
```
hello {{ message }} world
```
| jinja 템프릿 파일 확장자 .j2 , .jinja2