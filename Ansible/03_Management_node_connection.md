# 관리 노드 접속
## SSH 접속 방법
- 패스워드 인증
- **키 쌍 인증**

## 권한 상승(Pricielege Escalation)
- su(x)
- **sudo**

`/etc/sudoers`
```
%wheel  ALL=(ALL)       ALL
```

- %wheel: wheel 그룹
- ALL : 모든 시스템에서
- (ALL) : 모든 사용자로
- ALL : 모든 명령어

`/etc/sudoers.d/vagrant`
```
%vagrant ALL=(ALL) NOPASSWD: ALL
```

- NOPASSWD: 패스워드 묻지 않음 (passwordless sudo)

## ansible 옵션
- -u REMOTE_USER, --user REMOTE_USER : SSH 접속 계정(기본: 현재 사용자)
- -k, --ask-pass : 옵션 사용 SSH 패스워드 인증
	- 옵션 사용하지 않으면 --> SSH 키 인증

| ansible의 기본 인증 방법: SSH 키 인증

### 권한 상승 옵션
- -b, --become : 권한 상승
	- 옵션 사용하지 않으면 --> 권한상승 하지 않음
- --become-method <sudo|su>
	- sudo: 기본값
	- su
- --become-user : 어떤 사용자?
	- root: 기본값
- -K, --ask-become-pass : sudo 패스워드 묻기
	- 옵션 사용하지 않으면 --> Passwordless sudo

### 설정 파일
```
[defaults]
remote_user=<SSH_USER>
ask_pass=<True|False>
host_key_checking=<True|False>

[privilege_escalation]
become=<True|False>
become_ask_pass=<True|False>
become_method=<sudo|su>
become_user=<SUDO_USER>
```

- ask_pass 기본값: false
- host_key_checking 기본값: true
- become 기본값: false
- become_ask_pass 기본값: false
- become_method 기본값: sudo

### ansible-config 명령
- ansible-config list : 설정 가능한 모든 항목 표시
- ansible-config dump : 모든 설정의 기본 값 및 변경 값 표시
- ansible-config view : 현재 적용되는 설정 파일의 내용 표시