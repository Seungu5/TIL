# 핸들러

idempotent: 멱등
가능하면 멱등성을 만족
모든 모듈, 모듈의 파라미터가 멱등성을 막족하지는 않음

예시: 문제가 있는 코드
``` yaml
- hosts: 192.168.100.11
  become: yes
  vars:
    web_svc_port: "80"
  tasks:
    - yum:
        name: httpd
        state: installed
    - lineinfile:
        path: /etc/httpd/conf/httpd.conf
        regexp: '^Listen'
        line: 'Listen {{ web_svc_port }}' 
    - service:
        name: httpd
        state: restarted
        enabled: yes
```

예시: 문제를 해결하기 위한 코드
``` yaml
- hosts: 192.168.100.11
  become: yes
  vars:
    web_svc_port: "80"
  tasks:
    - yum:
        name: httpd
        state: installed
    - lineinfile:
        path: /etc/httpd/conf/httpd.conf
        regexp: '^Listen'
        line: 'Listen {{ web_svc_port }}' 
      register: result
    - service:
        name: httpd
        state: started
        enabled: yes
    - service:
        name: httpd
        state: restarted
        enabled: yes
      when: result is changed
```

## 플레이, 작업의 이름

``` yaml
- name: Name Test Playbook
  hosts: 192.168.100.11
  tasks:
    - name: task1
      debug:
        msg: hello world
    - name: task2
      debug:
        msg: hello world
    - name: task3
      debug:
        msg: hello world
    - debug:
        msg: hello world
      name: task4
```

## 핸들러
핸들러? 특정 작업이 **변경사항**을 발생하는 경우에만 실행하기 위한 작업을 지정

> 핸들러의 작업은 반드시 이름이 있어야 함

핸들러가 실행되는 순서
- 알림을 받은 핸들러 작업만 순서대로 실행
- 모든 작업(tasks)이 완료되어야 핸들러가 실행
- 알림을 받은 회수와 상관없이 한 번만 실행

예제
``` yaml
- name: handler example
  hosts: 192.168.100.11
  
  tasks:
    - name: task1
      file:
        path: /tmp/test1
        state: touch
      notify:
        - handle2
        - handle1
    #- name: error
    #  command: ls -P
    - name: task2
      file:
        path: /tmp/test2
        state: touch
      notify:
        - handle1

  handlers:
    - name: handle1
      debug:
        msg: "handle1"
    - name: handle2
      debug:
        msg: "handle2"
```

``` yaml
- name: Handler Example
  hosts: 192.168.100.11
  become: yes
  vars:
    web_svc_port: "80"
  
  tasks:
    - name: Install httpd Package
      yum:
        name: httpd
        state: installed
    - name: Reconfigure httpd service port
      lineinfile:
        path: /etc/httpd/conf/httpd.conf
        regexp: '^Listen'
        line: 'Listen {{ web_svc_port }}' 
      notify:
        - Restart httpd Service
    - name: Start httpd Service
      service:
        name: httpd
        state: started
        enabled: yes 
  handlers:
    - name: Restart httpd Service
      service:
        name: httpd
        state: restarted
        enabled: yes
```

## 핸들러가 실행되지 않고 후속 작업에서 실패한 경우
핸들러가 실행되지 않음
``` yaml
- name: Flush handlers
  meta: flush_handlers
```

``` bash
ansible-playbook test.yaml --forve-handlers
```

강제로 핸들러를 실행하게 하는 설정