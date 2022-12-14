# 역할

> https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html#playbooks-reuse-roles

역할 생성 -> 통합 -> 플레이북 통일화된 구조

``` bash
mkdir roles
ansible-galaxy init common --init-path roles
```

```
.
└── roles
    └── common
        ├── defaults
        │   └── main.yml
        ├── files
        ├── handlers
        │   └── main.yml
        ├── meta
        │   └── main.yml
        ├── README.md
        ├── tasks
        │   └── main.yml
        ├── templates
        ├── tests
        │   ├── inventory
        │   └── test.yml
        └── vars
            └── main.yml
```

`roles/common`: 역할의 이름

`tasks/main.yml`: 작업이 위치 `handlers/main.yml`: 핸들러 작업이 위치

`tests/inventory`: 역할을 테스트 하기 위한 인벤토리 `tests/test.yml`: 역할을 테스트 하기 위한 플레이북

`defaults/main.yml`: 기본 역할 변수(우선 순위가 매우 낮음) `vars/main.yml`: 역할 변수(우선 순위가 매우 높음)

`files`: 파일 관련 모듈의 src: 파라미터에서 참조하는 파일의 위치 `files/a.txt`: 경로 지정할 필요 없음

```
- copy:
	src: a.txt
```

`templates`: 템플릿 모듈의 `src`: 파라미터에서 참조하는 파일의 위치 `templates/a.j2`

```
- templates:
    src: a.j2
```

`meta/main.yml`: 역할을 설명하고 있는 파일

- 역할 버전
- 역할 이름
- 역할 만든 사람
- 역할 적용되는 플렛폼(리눅스 배포판)
- 역할의 의존성

## Playbook에서 작업 실행 순서

```
# Play
- hosts:
  
  pre_tasks:
  
  roles:
  
  tasks:
  
  post_tasks:

  handlers:
```

1. pre_tasks
2. pre_tasks의 handlers
3. roles
4. roles의 handlers
5. tasks
6. tasks의 handlers
7. post_tasks
8. post_tasks의 handlers

---

## ansible-galaxy

> https://galaxy.ansible.com/

- 역할(Role)
- 컬랙션(Collection): 역할 + 3rd Party 모듈
- 번들(Bundle): RedHat OpenShift <-- 역할

### 역할 목록 확인

``` bash
ansible-galaxy list
```

(0. 현재 디렉토리의 roles)

1. /home/vagrant/.ansible/roles
2. /usr/share/ansible/roles
3. /etc/ansible/roles

```
ansible-galaxy list --roles-path roles
```

```
ansible-galaxy search elasticsearch
ansible-galaxy info geerlingguy.elasticsearch
ansible-galaxy install geerlingguy.elasticsearch
ansible-galaxy remove geerlingguy.elasticsearch
```