# Load Balancer란

하나의 인터넷 서비스가 발생하는 트래픽이 많을 때 여러 대의 서버가 분산 처리하여 서버의 로드율 증가, 부하량, 속도 저하 등을 고려하여 적절히 분산 처리하여 해결해주는 서비스입니다.
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbYQhca%2Fbtq5NHgpXM9%2Fu7rf6EZ0LudXUb9paMfuVk%2Fimg.png)

## AWS ALB, NLB 비교

ALB와 NLB의 차이점은 다음과 같습니다.


## ALB

ALB는 L7단의 로드 밸런서를 지원합니다.

ALB는 HTTP/HTTPS 프로토콜의 헤더를 보고 적절한 패킷으로 전송합니다.


ALB는 IP 주소가 변동되기 때문에 Client에서 Access 할 ELB의 DNS Name을 이용해야 합니다.

ALB는 L7단을 지원하기 때문에 SSL 적용이 가능합니다.
## NLB

NLB는 L4단의 로드 밸런서를 지원합니다.

NLB는 TCP/IP 프로토콜의 헤더를 보고 적절한 패킷으로 전송합니다.

NLB는 IP + 포트번호를 보고 스위칭합니다.

NLB는 할당한 Elastic IP를 Static IP로 사용이 가능하여 DNS Name과 IP주소 모두 사용이 가능합니다.

NLB는 SSL 적용이 인프라 단에서 불가능하여 애플리케이션에서 따로 적용해 주어야 합니다.
 

# 번외

ALB에 고정IP 적용
- alb는 기본적으로 IP가 변경되기 때문에 고정 IP를 가질 수 있는 NLB를 앞에 둠으로서 적용이 가능합니다.

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FA09kA%2Fbtq5NcAQNiS%2FatKfa5af6lVij3kcxvFWd1%2Fimg.png)

위의 그림처럼 앞에 NLB를 두지만 CloudWatch와 Lambda함수를 이용하여 ALB의 IP가 변경되는 시점마다 변경된 IP에 맞게 설정해주는 작업이 추가적으로 필요합니다.

위의 내용 링크
https://aws.amazon.com/ko/blogs/korea/using-static-ip-addresses-for-application-load-balancers/


ALB와 NLB의 속도 차이
- NLB의 장점 중 하나는 클라이언트의 요청에 대해서 낮은 대기 시간으로 높은 처리가 가능하다는 것입니다.

NLB는 network 계층까지만 확인하기 때문에 7 계층인 ALB보다 빠릅니다.

또한 기존 ELB사용 시에 짧은 시간 내 스파크 성 트래픽 발생에 대한 대응이 어려웠으나 NLB를 사용함으로 ELB의 단점을 해소할 수 있습니다.

마지막으로 단순한 라우팅이 필요하고, 트래픽이 극도로 많은 경우에는 ALB 보다는 NLB를 사용하는 것이 적합하다고 할 수 있습니다.


 

## ALB/NLB Target Group

### ALB

Target Group을 Instance ID로 지정

ALB는 인스턴스에 대한 연결이 로드 밸런서에서 설정되므로 웹 서버 액세스 로그에는 로드 밸런서의 IP 주소가 캡처됩니다. 

따라서 Client의 IP를 얻기 위해서는 X-Forwarded-For헤더를 사용합니다.

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbvYe0K%2Fbtq5FVgNtM6%2FQJCQtd4ACHBzCv3afQHTf0%2Fimg.png)

X-Forwarded-For 요청 헤더는 자동으로 추가되어 HTTP 또는 HTTPS 로드 밸런서를 사용할 때 클라이언트의 IP 주소를 식별하는 데 도움을 줍니다. 로드 밸런서가 클라이언트와 서버 간의 트래픽을 가로채기 때문에 서버 액세스 로그에 로드 밸런서의 IP 주소만 포함됩니다. 클라이언트의 IP 주소를 확인하려면 X-Forwarded-For 요청 헤더를 사용하십시오


### NLB

Target Group을 Instance ID로 지정

Instance ID로 지정한 Target Group의 경우 DSR(Direct Server Return) 방식으로 동작하여 Response 시에 EC2 Instance는 직접 Client에게 패킷을 전달합니다.

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcknkqA%2Fbtq5KQMrZv6%2Fzvur3skutK0LakeA5IkHL1%2Fimg.png)

따라서 Server단에서 Client의 ip를 확인할 수 있습니다.


Target Group을 IP로 지정

IP로 지정한 Target Group의 경우 기존 방식대로 Request/Response가 모두 LB를 경유하기 때문에 아웃바운드 통신이 되지 않는 Private 구간에서도 NLB를 이용하여 서비스가 가능합니다.


![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFpAZ8%2Fbtq5L44lYcu%2FvIGZj1Y0jffczwkEYGmqa1%2Fimg.png)

따라서 Server단에서 LoadBalancer의 ip를 확인할 수 있습니다.

 

