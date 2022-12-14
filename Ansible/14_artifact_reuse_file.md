# 아티펙트 재사용 - 파일


Artifact: 인공물
- 애플리케이션이 작동해서 생성한 데이터
- 사람이 직접 작성한 코드

파일을 용도별로 구분을 해서 재사용하기 위함
- 변수 파일
- 작업 파일
- 플레이/플레이북 파일
- 역할(Role)

## 변수 파일

**vars_files**

플레이의 키워드
``` yaml
- hosts: x
  vars_files:
    - vars/a.yaml

  tasks:
  ...
```

**include_vars** 모듈
``` yaml
- hosts: x

  tasks:
    - include_vars:
        dir: vars/
```

## 인벤토리 변수
### 인텐보리 내부 파일에 변수 설정

**호스트 변수**
``` yaml
node1 message="hello world"
```

**그룹 변수**
``` ini
[wordpress]
node1
node2

[wordpress:vars]
message="hello world"
```

### 인벤토리 외부 파일에 변수 설정
인벤토리 파일 또는 플레이북 파일이 있는 디렉토리에
- `group_vars/<GROUP NAME>`
- `host_vars/<HOST NAME>`

`<GROUP NAME>`, `<HOST NAME>` 디렉토리 또는 파일을 생성

```
.
├── ansible.cfg
├── group_vars
│   └── nodes
├── host_vars
│   ├── 192.168.100.11
│   └── 192.168.100.12
│       └── var.yaml
└── inven.ini
```

`ansible.cfg`
``` ini
[defaults]
inventory = inven.ini
```

`inven.ini`
``` ini
[nodes]
192.168.100.11
192.168.100.12
```

`host_vars\192.168.100.11`
``` yaml
---
message: hello node1
```

`host_vars\192.168.100.12\var.yaml`
``` yaml
---
message: hello node2
```

`group_vars\nodes`
``` yaml
service_port: 8080
message: hello world
```

``` bash
ansible-inventory --list
ansible-inventory --host <HOST>
```

`test.yaml`
``` yaml
---
- hosts: nodes
  tasks:
    - debug:
        msg: "{{ message }} - {{ service_port }}"
```

## 작업 재사용
include_vars: 변수 가져오기
include_role: 역할 가져오기
include_tasks: 작업 가져오기

import_playbook: 플레이북 가져오기
import_role: 역할 가져오기
import_tasks: 작업 가져오기

**include vs. import**

|	|include	|import|
|-|-|-|
|적용 시점|	동적|	정적|
|루프 사용 가능|	가능	|불가능|
|핸들러 호출 가능|	불가능	|가능|

### import에서 루프 불가능
``` yaml
- hosts: 192.168.100.11
  tasks:
    - debug:
        msg: in play
    - include_tasks:
        file: task.yaml
      with_sequence: start=1 end=3 # 안됨
    - debug:
        msg: in play
```

**해결방법**
``` yaml
- hosts: 192.168.100.11
  tasks:
    - debug:
        msg: in play
    - include_tasks:
        file: task.yaml
    - debug:
        msg: in play
```

`task.yaml`
```yaml
- debug:
  with_sequence: start=1 end=3
```

### include에서 핸들러 호출 불가능
``` yaml
- hosts: 192.168.100.11
  tasks:
    - command: hostname
      notify:
        - hello notify
  handlers:
    - include_tasks: task.yaml
```

`task.yaml`
``` yaml
- name: hello notify
  debug:
    msg: hello notify
```

**해결방법**
``` yaml
- hosts: 192.168.100.11
  tasks:
    - command: hostname
      notify:
        - hello notify
  handlers:
    - name: hello notify
	  include_tasks: task.yaml
```