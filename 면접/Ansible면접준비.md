# 전제

Ansible은 Red Hat의 제품이며 여러 기능을 가지고 있습니다. 우리는 Ansible을 언급할 때 주로 Ansible Core에 대해 이야기할 것입니다. 따라서 Ansible은 IT 자동화 도구입니다. 구성 관리, 지속적인 배포를 위한 플레이북 실행, 기본적으로 배포 간소화, 다양한 환경 조정에 도움이 됩니다. 처음에 이것을 설정하는 것은 약간 까다로울 수 있지만 문서에서 많은 도움을 받았습니다.


## 기본 Ansible 인터뷰 질문

### 1. CI/CD란 무엇입니까?

지속적인 통합은 개발 및 배포 프로세스를 간소화하는 데 사용되는 것입니다. 이는 응집력 있는 소프트웨어의 보다 신속한 개발로 이어집니다. 
반면에 Continuous Delivery는 원격 리포지토리로 푸시된 코드를 언제든지 프로덕션으로 가져올 수 있는 프로세스입니다.


위의 다이어그램에서 통합 테스트 및 단위 테스트는 수동 개입 없이 수행되었으며 UAT 이후에는 테스트된 기능을 프로덕션으로 배송하고 CI/CD가 필요한 프로세스를 만들기 위해 승인이 필요했습니다.

### 2. 구성 관리란 무엇입니까?

일정 기간 동안 시스템에 들어오는 모든 업데이트를 추적하기 위해 따라야 하는 관행입니다. 이는 또한 몇 가지 새로운 변경 사항으로 인해 시스템에 주요 버그가 도입되어 최소 가동 중지 시간으로 수정해야 하는 상황에서도 도움이 됩니다. 버그를 수정하는 대신 이 버그를 일으킨 새로운 변경 사항을 추적하면서 롤백할 수 있습니다.

### 3. Ansible은 어떻게 작동합니까?

Ansible은 자동화 도구가 되기 위해 함께 작동하는 여러 조각의 조합입니다. 주로 모듈, 플레이북 및 플러그인입니다.

모듈은 실행될 작은 코드입니다. 빌드 작업의 시작점 역할을 하는 여러 내장 모듈이 있습니다.
플레이북에는 작업 그룹인 연극이 포함되어 있습니다. 프로세스를 완료하는 데 필요한 워크플로 또는 단계를 정의하는 곳입니다.
플러그인은 로깅 목적으로 주 제어 시스템에서 실행되는 특별한 종류의 모듈입니다. 다른 유형의 플러그인도 있습니다.

플레이북은 Ansible 자동화 엔진을 통해 실행되었습니다. 이러한 플레이북에는 기본적으로 호스트 시스템에서 실행되는 작업인 모듈이 포함되어 있습니다. 여기에서 따라야 하는 메커니즘은 푸시 메커니즘입니다. 따라서 가능한 시스템은 원하는 시스템 상태의 리소스 모델이 되도록 작성된 이러한 호스트 시스템에 작은 프로그램을 푸시합니다.
![img](https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/319/original/working_of_ansible.jpg?1618840647)

### 4. Ansible의 특징은 무엇입니까?

다음과 같은 기능이 있습니다.

Agentless – 꼭두각시나 요리사와 달리 노드를 관리하는 소프트웨어나 에이전트가 없습니다.
Python – 스크립트를 배우고 작성하기 매우 쉬운 python과 강력한 프로그래밍 언어 중 하나를 기반으로 구축되었습니다.
SSH – 암호가 없는 네트워크 인증으로 보다 안전하고 쉽게 설정할 수 있습니다.
푸시 아키텍처 – 핵심 개념은 여러 개의 작은 코드를 구성에 푸시하고 클라이언트 노드에서 작업을 실행하는 것입니다.
설정 – 매우 낮은 학습 곡선과 모든 오픈 소스로 설정이 매우 쉬워 누구나 실습할 수 있습니다.
재고 관리 – 기계의 주소는 간단한 텍스트 형식으로 저장되며 Openstack, Rackspace 등과 같은 플러그인을 사용하여 목록을 가져오기 위해 다양한 정보 소스를 추가할 수 있습니다.

### 5. 인프라를 코드로 설명하시겠습니까?

IaC(Infrastructure as a Code)는 DevOps 팀이 인프라를 보다 조직적으로 관리하기 위해 따라야 하는 프로세스입니다. 일부 폐기 스크립트 또는 수동으로 클라우드 구성 요소를 구성하는 대신 이 모든 것이 있고 구성 변경을 통해 수행해야 하는 코드 저장소가 있어야 합니다. 소스 제어 하에 두는 것도 현명합니다. 이를 통해 속도, 일관성 및 책임성이 향상됩니다.

### 6. 앤서블 갤럭시란?

Galaxy는 사용자 간에 공유할 수 있고 실행을 위해 플레이북에 직접 드롭할 수 있는 Ansible 역할의 저장소입니다. 또한 역할, 플러그인 및 컬렉션이라고도 하는 모듈을 포함하는 패키지 배포에 사용됩니다. ansible-galaxy-collection 명령은 init, build, install 등과 유사한 명령을 ansible-galaxy 명령처럼 구현합니다.

### 7. Ansible 모듈에 대해 자세히 설명하시겠습니까?

Ansible 모듈은 특정 작업을 멱등적으로 실행하는 함수 또는 독립 실행형 스크립트와 같습니다. 이들의 반환 값은 stdout의 JSON 문자열이며 입력은 모듈 유형에 따라 다릅니다. Ansible 플레이북에서 사용합니다.
Ansible에는 두 가지 유형의 모듈이 있습니다.

핵심 모듈
핵심 Ansible 팀은 이러한 모듈을 유지 관리할 책임이 있으므로 Ansible 자체와 함께 제공됩니다. 보고된 문제는 "추가" 리포지토리에 있는 문제보다 우선적으로 수정됩니다.

추가 모듈
Ansible 커뮤니티는 이러한 모듈을 유지 관리하므로 현재로서는 Ansible과 함께 제공되지만 향후 중단될 수 있습니다. 사용할 수 있지만 기능 요청이나 문제가 있는 경우 낮은 우선 순위로 업데이트됩니다.

이제 인기 있는 추가 모듈이 언제든지 핵심 모듈에 들어갈 수 있습니다. 이러한 모듈에 대한 별도의 저장소를 각각 ansible-modules-core 및 ansible-modules-extra로 찾을 수 있습니다.

### 8. YAML 파일이란 무엇이며 Ansible에서 어떻게 사용합니까?

YAML 또는 파일은 JSON 또는 XML과 같은 몇 가지 규칙 집합이 있는 형식화된 텍스트 파일과 같습니다. Ansible은 다른 형식보다 읽기 쉽기 때문에 플레이북에 이 구문을 사용합니다.
JSON 대 YAML의 예는 다음과 같습니다.
```
{
 "object": {
"key": "value",
"array": [
  {
    "null_value": null
  },
  {
    "boolean": true
  },
  {
    "integer": 1
  },
  {
    "alias": "aliases are like variables"
  }
]
 }
}
```


```
---
object:
 key: value
 array:
 - null_value:
 - boolean: true
 - integer: 1
 - alias: aliases are like variables
```

### 9. Ansible 작업이란 무엇입니까?

작업은 Ansible의 단위 작업입니다. 구성 정책을 더 작은 파일이나 코드 블록으로 쪼개어 도움이 됩니다. 이러한 블록은 프로세스를 자동화하는 데 사용할 수 있습니다. 예를 들어 패키지를 설치하거나 소프트웨어를 업데이트하려면
```
Install <package_name>, update <software_name>
```


### 10. JAVA, Python 등과 같은 고급 프로그래밍 언어에서 YAML 파일을 사용하는 방법은 무엇입니까?

YAML은 대부분의 프로그래밍 언어에서 지원되며 사용자 프로그램과 쉽게 통합될 수 있습니다.
JAVA에서는 XML 및 JSON도 구문 분석하는 Jackson 모듈을 사용할 수 있습니다. 예를 들어

```
// We need to declare Topic class with necessary attributes such as name, total_score, user_score, sub_topics
List<Topic> topics = new ArrayList<Topic>();
topics.add(new Topic("String Manipulation", 10, 6));
topics.add(new Topic("Knapsack", 5, 5));
topics.add(new Topic("Sorting", 20, 13));
// We want to save this Topic in a YAML file
Topic topic = new Topic("DS & Algo", 35, 24, topics);
// ObjectMapper is instantiated just like before
ObjectMapper om = new ObjectMapper(new YAMLFactory());
// We write the `topic` into `topic.yaml`
om.writeValue(new File("/src/main/resources/topics.yaml"), topic);
```

```
---
name: "DS & Algo"
total_score: 35
user_score: 24
sub_topics:
- name: "String Manipulation"
 total_score: 10
 user_score: 6
- name: "Knapsack"
 total_score: 5
 user_score: 5
- name: "Sorting"
 total_score: 20
 user_score: 13
 ```

마찬가지로 YAML에서도 읽을 수 있습니다.
```
// Loading the YAML file from the /resources folder
ClassLoader classLoader = Thread.currentThread().getContextClassLoader();
File file = new File(classLoader.getResource("topic.yaml").getFile());
// Instantiating a new ObjectMapper as a YAMLFactory
ObjectMapper om = new ObjectMapper(new YAMLFactory());
// Mapping the employee from the YAML file to the Employee class
Topic topic = om.readValue(file, Topic.class);
```
파이썬에서도 마찬가지로 pyyaml ​​라이브러리를 사용하여 YAML 형식으로 쉽게 읽고 쓸 수 있습니다.

## 중급 Ansible 인터뷰 질문

### 11. 직접 액세스할 수 없는 서버에 액세스하도록 점프 호스트를 설정하는 방법은 무엇입니까?

먼저 ansible_ssh_common_args 인벤토리 변수에 ProxyCommand를 설정해야 합니다. 이 변수에 지정된 모든 인수는 관련 호스트에 연결할 때 sftp/scp/ssh 명령줄에 추가되기 때문입니다. 예를 들어
```
[gatewayed]
staging1 ansible_host=10.0.2.1
staging2 ansible_host=10.0.2.2
```
이들을 위한 점프 호스트를 생성하려면 ansible_ssh_common_args에 명령을 추가해야 합니다.
```
ansible_ssh_common_args: '-o ProxyCommand="ssh -W %h:%p -q user@gateway.example.com"'
```
이런 식으로 게이트웨이 그룹의 호스트에 연결을 시도할 때마다 이 인수가 명령줄에 추가됩니다.

### 12. 암호화된 파일을 사용하여 플레이북에서 암호 입력을 자동화하는 방법은 무엇입니까?

비밀번호 입력을 자동화하기 위해 암호화된 파일의 모든 비밀번호에 대한 비밀번호 파일이 저장되고 필요할 때 이를 가져오기 위해 호출을 할 수 있습니다.
```
ansible_ssh_common_args: '-o ProxyCommand="ssh -W %h:%p -q user@gateway.example.com"'
```
이것은 또한 암호를 지정하는 별도의 스크립트를 사용하여 달성할 수 있습니다. 그러나 이 경우 성가신 오류 없이 작동하려면 stdout에 대한 암호를 인쇄해야 합니다.
```
ansible-playbook launch.yml --vault-password-file ~/ .vault_pass.py
```
### 13. Ansible에서 콜백 플러그인이란 무엇입니까?

콜백 플러그인은 기본적으로 cmd 프로그램을 실행하는 동안 표시되는 대부분의 출력을 제어합니다. 그러나 추가 출력을 추가하는 데에도 사용할 수 있습니다. 예를 들어 log_plays 콜백은 플레이북 이벤트를 로그 파일에 기록하는 데 사용되며 메일 콜백은 플레이북 실패 시 이메일을 보내는 데 사용됩니다. 사용자 정의 콜백 플러그인을 play에 인접한 callback_plugins 디렉토리, 역할 내부에 추가하거나, sible.cfg에 구성된 콜백 디렉토리 소스 중 하나에 추가할 수도 있습니다.

### 14. Ansible Inventory와 그 유형은 무엇입니까?

Ansible에는 정적 및 동적의 두 가지 유형의 인벤토리 파일이 있습니다.

정적 인벤토리 파일은 일반 텍스트 파일의 호스트 이름 또는 IP 주소를 사용하여 호스트 그룹 아래에 선언된 관리 호스트 목록입니다. 관리 호스트 항목은 각 행의 그룹 이름 아래에 나열됩니다. 예를 들어
```
[gatewayed]
staging1 ansible_host=10.0.2.1
staging2 ansible_host=10.0.2.2
```

동적 인벤토리 는 Python 또는 기타 프로그래밍 언어로 작성된 스크립트 또는 플러그인(선호)을 사용하여 생성됩니다. 클라우드 설정에서는 가상 서버를 중지했다가 다시 시작하면 IP 주소가 변경되므로 정적 인벤토리 파일 구성이 실패합니다. 다음과 같은 구성을 위한 demo_aws_ec2.yaml 파일을 생성합니다.
```
plugin: aws_ec2 regions:
ap-south-1 filters:
tag:tagtype: testing
```
이제 이 명령을 사용하여 가져올 수 있습니다.
```
ansible-inventory -i demo_aws_ec2.yaml -graph
```

### 15. Ansible Vault란 무엇입니까?
Ansible 볼트는 플레이북이나 역할에 일반 텍스트로 저장하는 대신 비밀번호와 같은 민감한 데이터를 보관하는 데 사용됩니다. 모든 구조화된 데이터 파일 또는 YAML 파일 내부의 단일 값은 Ansible로 암호화할 수 있습니다. 

파일을 암호화하려면
```
ansible-vault encrypt foo.yml bar.yml baz.yml
```
그리고 암호를 해독하는 것과 유사하게
```
ansible-vault decrypt foo.yml bar.yml baz.yml
```
### 16. 템플릿 내에서 그룹의 호스트 목록에 대해 어떻게 루핑을 수행할 수 있습니까?

다음과 같이 템플릿의 "$groups" 사전에 액세스하여 이를 수행할 수 있습니다.
```
{% for host in groups['db_servers'] %}
{{ host }}
{% endfor %}
```
사실에 액세스해야 하는 경우 사실이 채워졌는지도 확인해야 합니다. 예를 들어, db_servers와 대화하는 플레이:
```
- hosts: db_servers
tasks:
- debug: msg="Something to debug"
```
이제 다음과 같이 템플릿 내에서 사용할 수 있습니다.
```
{% for host in groups['db_servers'] %}
{{ hostvars[host]['ansible_eth0']['ipv4']['address'] }}
{% endfor %}.
```
### 17. Ansible에서 임시 명령이란 무엇입니까?

임시 명령은 특정 작업만 수행하기 위한 한 줄짜리 플레이북과 같습니다. 임시 명령의 구문은 다음과 같습니다.
```
ansible [pattern] -m [module] -a "[module options]"
```
예를 들어 스테이징 그룹의 모든 서버를 재부팅해야 합니다.
```
ansible atlanta -a "/sbin/reboot"  -u username --become [--ask-become-pass]
```
### 18. Ansible 플레이북을 사용하여 Nginx를 설치하시겠습니까?

플레이북 파일은 다음과 같습니다.
```
- hosts: stagingwebservers
 gather_facts: False
 vars:
  - server_port: 8080
 tasks:
  - name: install nginx
    apt: pkg=nginx state=installed update_cache=true
  - name: serve nginx config
     template: src=../files/flask.conf dest=/etc/nginx/conf.d/
     notify:
     - restart nginx
 handlers:
   - name: restart nginx
     service: name=nginx state=restarted
   - name: restart flask app
     service: name=flask-demo state=restarted
...
```
위의 플레이북에서 우리는 이러한 작업을 실행하기 위해 stagingwebservers 그룹의 모든 호스트를 가져오고 있습니다. 첫 번째 작업은 Nginx를 설치한 다음 구성하는 것입니다. 우리는 또한 참고용으로 플라스크 서버를 가져오고 있습니다. 결국 상태가 변경될 경우 Nginx를 다시 시작하도록 핸들러도 정의했습니다. 위 플레이북을 실행한 후 Nginx가 설치되었는지 여부를 확인할 수 있습니다.
```
ps waux | grep nginx
```
### 19. 프로그래밍 방식으로 변수 이름에 액세스하려면 어떻게 해야 합니까?

변수 이름은 문자열을 함께 추가하여 작성할 수 있습니다. 예를 들어, 역할 매개변수 또는 다른 입력을 통해 사용할 인터페이스가 제공될 수 있는 임의의 인터페이스의 ipv4 주소를 가져와야 하는 경우 이러한 방식으로 수행할 수 있습니다.
```
{{ hostvars[inventory_hostname]['ansible_' + which_interface]['ipv4']['address'] }}
```
### 20. Ansible과 Puppet의 차이점은 무엇입니까?

관리 및 스케줄링:  Ansible에서 서버는 구성을 꼭두각시로 노드에 푸시하고 클라이언트는 서버에서 구성을 가져옵니다. 또한 예약을 위해 꼭두각시에는 모든 노드가 바람직한 상태에 있는지 확인하기 위해 30분마다(기본 설정) 폴링하는 에이전트가 있습니다. Ansible에는 무료 버전에 해당 기능이 없습니다.
가용성: Ansible에는 백업 보조 노드가 있고 puppet에는 둘 이상의 마스터 노드가 있습니다. 따라서 둘 다 고가용성을 위해 노력합니다.
설정: Puppet은 클라이언트-서버 아키텍처를 가지고 있고 고유한 선언적 언어인 Puppet DSL이라는 특정 언어가 있기 때문에 설정이 가능한 것보다 더 어려운 것으로 간주됩니다.

### 21. Ansible Tower란 무엇이며 어떤 특징이 있나요?

Ansible Tower는 RedHat의 엔터프라이즈급 솔루션입니다. 웹 기반 콘솔 및 REST API를 제공하여 조직의 팀 간에 Ansible을 관리합니다. 등의 많은 기능이 있습니다

워크플로 편집기 - 플레이북 간에 서로 다른 종속성을 설정하거나 한 번에 여러 팀에서 유지 관리하는 여러 플레이북을 실행할 수 있습니다.
실시간 분석 - 모든 플레이 또는 작업의 상태를 쉽게 모니터링할 수 있으며 다음에 실행할 내용을 확인할 수 있습니다.
감사 추적 - 로그 추적은 나쁜 일이 발생하면 신속하게 기능 상태로 되돌릴 수 있도록 매우 중요합니다.
원격으로 명령 실행 - 타워를 사용하여 인벤토리에 있는 호스트 또는 호스트 그룹에 명령을 실행할 수 있습니다.
작업 예약, 알림 통합, CLI 등과 같은 다른 기능도 있습니다.

### 22. 어떻게 파일을 대상 호스트에 재귀적으로 복사할 것인지 설명하십시오.

재귀 매개변수가 있는 복사 모듈이 있지만 많은 수의 파일에 더 효율적인 동기화라는 것이 있습니다. 

예를 들어:
```
- synchronize:
   src: /first/absolute/path
   dest: /second/absolute/path
   delegate_to: "{{ inventory_hostname }}"
```
### 23. 콘텐츠를 재사용/재배포 가능하게 만드는 가장 좋은 방법은 무엇입니까?

콘텐츠를 재사용 및 재배포 가능하게 만들기 위해 Ansible 역할을 사용할 수 있습니다. Ansible 역할은 기본적으로 플레이북을 구성하기 위한 추상화 수준입니다. 예를 들어 5개의 시스템에서 10개의 작업을 실행해야 하는 경우 플레이북에 모든 작업을 작성하면 실수와 혼란이 발생할 수 있습니다. 대신 우리는 10개의 역할을 만들고 플레이북 내에서 호출합니다.

### 24. 핸들러란 무엇입니까?

핸들러는 태스크에 "알림" 지시문이 포함된 경우에만 실행되는 특수 태스크와 같습니다. 
```
tasks:
  - name: install nginx
    apt: pkg=nginx state=installed update_cache=true
    notify:
     - start nginx
 handlers:
   - name: start nginx
     service: name=nginx state=started
```
위의 예에서는 NGINX를 설치한 후 `start nginx` 핸들러를 사용하여 서버를 시작하고 있습니다.

### 25. 사용자 모듈에 대한 암호화된 암호를 생성하는 방법은 무엇입니까?

Ansible에는 이를 위한 매우 간단한 임시 명령이 있습니다.
```
ansible all -i localhost, -m debug -a "msg={{ 'mypassword' | password_hash('sha512', 'mysecretsalt') }}"
```
Python의 Passlib 라이브러리를 사용할 수도 있습니다. 예를 들어
```
python -c "from passlib.hash import sha512_crypt; import getpass; print(sha512_crypt.using(rounds=5000).hash(getpass.getpass()))"
```
게다가, 우리는 또한 플레이북이나 host_vars에 원시 암호를 저장하는 것을 피해야 합니다. 대신에 우리는 암호의 해시 버전을 생성하기 위해 통합 방법을 사용해야 합니다.

### 26. 변수의 점 표기법과 배열 표기법은 어떻게 다른가요?

점 표기법은 다음과 같은 몇 가지 특별한 경우를 제외하고는 잘 작동합니다.

변수에 밑줄 또는 알려진 공용 속성으로 시작하거나 끝나는 점(.), 콜론(:)이 포함된 경우.
python 사전의 메서드와 속성 간에 충돌이 있는 경우.
배열 표기법은 또한 동적 변수 합성을 허용합니다.

## 고급 Ansible 인터뷰 질문

### 27. Ansible 동기화 모듈은 어떻게 작동합니까?

Ansible 동기화는 플레이북에서 사용할 수 있는 Linux 시스템의 rsync와 유사한 모듈입니다. 기능은 아카이브, 압축, 삭제 등과 같은 rsync와 유사하지만 다음과 같은 제한 사항도 거의 없습니다.

Rsync는 소스 및 대상 시스템 모두에 설치되어야 합니다.
localhost에서 다른 포트로 소스를 변경하려면 delegate_to를 지정해야 합니다.
원격 사용자별로 파일에 액세스할 수 있으므로 사용자 권한을 처리해야 합니다.
sudo를 사용하는 경우 항상 대상 호스트 위치의 전체 경로를 제공해야 합니다. 그렇지 않으면 파일이 원격 사용자 홈 디렉토리에 복사됩니다.
하드 링크와 관련된 Linux rsync 제한 사항도 여기에 적용됩니다.
연결 실패의 경우 깨진 상태를 피하기 위해 -delay-updates를 강제 실행합니다.
동기화 모듈의 예는 다음과 같습니다.
```
---
- hosts: host-remote tasks:
- name: sync from sync_folder
synchronize:
src: /var/tmp/sync_folder dest: /var/tmp/
```
여기에서 /var/tmp/sync_folder 폴더의 파일을 원격 시스템의 /var/tmp 폴더로 전송합니다.


### 28. Ansible firewalld 모듈은 어떻게 작동합니까?

Ansible firewalld는 호스트 시스템의 방화벽 규칙을 관리하는 데 사용됩니다. 이것은 포트에서 서비스를 허용/차단하기 위한 Linux firewalld 데몬처럼 작동합니다. 크게 두 가지 개념으로 나뉜다

영역: 노출되는 서비스 또는 로컬 네트워크 인터페이스가 연결된 위치를 제어할 수 있는 위치입니다.
서비스: 일반적으로 호스트가 수신 대기할 수 있는 일련의 포트/프로토콜 조합(소켓)이며 하나 이상의 영역에 배치될 수 있습니다.
방화벽 설정의 몇 가지 예는 다음과 같습니다.
```
- name: permit traffic in default zone for https service
 ansible.posix.firewalld:
   service: https
   permanent: yes
   state: enabled
   
- name: do not permit traffic in default zone on port 8081/tcp
 ansible.posix.firewalld:
   port: 8081/tcp
   permanent: yes
   state: disabled
```
### 29. Ansible set_fact 모듈은 vars, vars_file 또는 include_var와 어떻게 다릅니까?

 Ansible에서 set_fact는 설정 모듈에서 발견한 가능한 사실과 마찬가지로 호스트별로 새 변수 값을 설정하는 데 사용됩니다. 이러한 변수는 플레이북의 후속 플레이에 사용할 수 있습니다. vars, vars_file 또는 include_var의 경우 미리 값을 알고 있는 반면, set_fact를 사용할 때는 필터를 사용하거나 다른 변수의 하위 부분을 가져오는 것과 같은 특정 작업을 사용하여 즉시 값을 준비한 후 값을 저장할 수 있습니다. 그 위에 팩트 캐시를 설정할 수도 있습니다.

set_fact 변수 할당은 키가 변수 이름이고 값이 변수에 대한 할당인 키 쌍 값을 사용하여 수행됩니다. 간단한 예는 아래와 같을 것입니다
```
- set_fact:
one_fact: value1
second_fact:
value2
```

### 30. 변수에서 작업 인수를 대량으로 설정하는 것이 안전하지 않은 경우는 언제입니까?

작업의 모든 인수는 일부 동적 실행 시나리오에서도 유용할 수 있는 사전 유형 변수일 수 있습니다. 그러나 Ansible은 보안 위험이 있으므로 경고를 표시합니다.
```
vars:
 usermod_args:
name: testuser
state: present
update_password: always
tasks:
- user: '{{ usermod_args }}'
```
위의 예에서 변수 usermod_args에 전달된 값은 손상된 대상 시스템의 호스트 사실에 있는 다른 악의적인 값으로 덮어쓸 수 있습니다. 이것을 피하려면

대량 변수 우선 순위는 호스트 사실보다 높아야 합니다.
변수와 팩트 값의 충돌을 피하기 위해 INJECT_FACTS_AS_VARS 구성을 비활성화해야 합니다.

### 31. Ansible 레지스터를 설명하라.

Ansible 레지스터는 작업 실행의 출력을 변수에 저장하는 데 사용됩니다. 이것은 각 원격 호스트의 출력이 다를 때 유용합니다. 레지스터 값은 플레이북 실행 전반에 걸쳐 유효하므로 set_fact를 사용하여 데이터를 조작하고 그에 따라 다른 작업에 입력을 제공할 수 있습니다.
```
- hosts: all tasks:
name: find all txt files in /home shell: "find /home -name *.txt" register: find_txt_files
debug:
var: find_txt_files
```
위의 예에서는 원격 호스트의 홈 폴더에서 모든 .txt 파일을 검색한 다음 find_txt_files에서 캡처하여 해당 변수를 표시합니다.


### 32. Ansible에서 작업을 위임하려면 어떻게 해야 합니까?

작업 위임은 다른 호스트를 참조하여 한 호스트에서 작업을 수행하려는 사용 사례가 있을 수 있으므로 Ansible의 중요한 기능입니다. delegate_to 키워드를 사용하여 이 작업을 수행할 수 있습니다. 

예를 들어 로드 밸런서 풀에서 노드를 관리하려면 다음을 수행할 수 있습니다.
```
- hosts: webservers
 serial: 5
 
 tasks:
- name: Take machine out of ELB pool
  ansible.builtin.command: /usr/bin/take_out_of_pool {{ inventory_hostname }}
  delegate_to: 127.0.0.1
  
- name: Actual steps would go here
  ansible.builtin.yum:
    name: acme-web-stack
    state: latest
    
- name: Add machine back to ELB pool
  ansible.builtin.command: /usr/bin/add_back_to_pool {{ inventory_hostname }}
  delegate_to: 127.0.0.1
```
또한 한 번에 실행되는 호스트 수를 제어하기 위해 직렬을 정의하고 있습니다. delegate_to 대신 사용할 수 있는 local_action이라는 또 다른 약식 구문이 있습니다. 
```
...
tasks:
   - name: Take machine out of ELB pool
     local_action: ansible.builtin.command /usr/bin/take_out_of_pool {{ inventory_hostname }}
...
```
그러나 위임할 수 없는 포함, add_host 및 디버그 작업과 같은 몇 가지 예외도 있습니다.


## 결론

Ansible은 IT 작업을 자동화하는 훌륭한 도구이며 업계에서 널리 사용되므로 모든 소프트웨어 개발자 또는 DevOps 팀의 누군가는 기본 사항을 알고 있어야 합니다. 또한 설정이 매우 쉽기 때문에 바로 시작할 수 있습니다. 이 질문은 인터뷰와 Ansible을 심층적으로 이해하는 데 도움이 되는 Ansible과 관련된 가장 중요한 개념을 다룹니다.