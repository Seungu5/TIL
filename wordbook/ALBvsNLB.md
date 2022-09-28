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

 


















------- 
NLB (Network LoadBalancer) 
이름에서 알 수 있듯이 NLB는 L4 계층, 네트워크 계층에서 동작한다.
 
특징

휘발성 처리 초당 수백만개 처리 가능
로드 밸런서에 대한 고정 IP 주소 지원

 
ALB (Application LoadBalancer)
L7 계층, 즉 애플리케이션 계층에서 동작하는 로드밸런서이다. 
 
특징 

path-based(경로 기반) 라우팅이 지원된다


ALB는 애플리케이션 계층에서 동작하므로, 해당 요청의 path까지 참고하여 path 별 라우팅이 가능하다. 이는 특정 path로 들어오는 경우에는 다른 서버로 라우팅 시켜주어야 할때 유용하게 사용할 수 있다.예를 들어, Delivery라는 서비스를 리팩토링 한다고 가정해보자.서비스의 안정성을 위해 특정 path 별로 라우팅을 하고 싶어,기존에 모두 delivery 서비스로 들어오던 요청 중 /register path로 들어오는 요청만 새로 리팩토링한 서버로 전달하고 싶다. 이런 경우에 ALB의 path 라우팅 기능을 이용하여 기존 deliery 서버로 들어오는 요청 중 /register로 들어오는 요청만 리팩토링한 새 서비스로 전달할 수 있다.이러한 특징 때문에 마이크로서비스 구조에서 path별로 각 마이크로서비스로 라우팅이 필요한 api gw는 alb를 사용한다고 한다.ALB는 애플리케이션 계층에서 동작하므로, 해당 요청의 path까지 참고하여 path 별 라우팅이 가능하다. 이는 특정 path로 들어오는 경우에는 다른 서버로 라우팅 시켜주어야 할때 유용하게 사용할 수 있다.


HTTP 헤더의 호스트 필드를 기반으로 라우팅 지원한다. 단일 로드밸런서를 이용해 요청을 여러 도메인으로 라우팅이 가능하다.
표준 및 사용자 지정 HTTP 헤더와 메서드, 쿼리 매개 변수, 소스 IP 주소와 같은 요청의 필드를 기반으로 라우팅을 지원한다.
한 URL에서 다른 URL로 요청 리디렉션을 지원한다.
HTTP 응답 반환을 커스텀 할 수 있다.
X-Forwarded-For를 사용하여 클라이언트 IP 주소를 캡처하여 액세스 로그에 출력이 가능하다.

nlb에 비해 7계층까지 확인하는 alb의 기능이 더 많다.
그러나, nlb는 network 계층까지만 확인하므로 alb 보다 빠르다. 따라서 단순한 라우팅이 필요하고, 트래픽이 극도로 많은 경우에는 alb 보다는 nlb를 사용하는 것이 적합하다.
alb는 path-based routing이 가능하므로 path를 확인하여 특정 서버로 라우팅을 시켜주어야 하는 경우에 적합하다 (api gw)
