# AWS 면접 질문

AWS는 Amazon에서 제공하는 클라우드 컴퓨팅 서비스입니다. AWS를 사용하면 애플리케이션과 서비스를 구축, 테스트, 배포 및 관리할 수 있습니다. 이 모든 작업은 데이터 센터와 Amazon에서 관리하는 하드웨어를 통해 수행됩니다. AWS는 IaaS(Infrastructure-as-a-Service), PaaS(Platform-as-a-Service) 및 SaaS(Software-as-a-Service) 제품의 조합을 제공합니다.

AWS를 사용하여 네트워킹 및 장치 관리와 함께 처리 능력, 스토리지 용량 및 분석으로 무장할 수 있는 가상 머신을 생성할 수 있습니다. AWS는 선불 비용을 방지하고 월별 사용량에 따라 지불하는 종량제 모델을 제공합니다.

## AWS 기본 면접 질문

### 1. EC2란 무엇입니까?

EC2, OS 수준 제어가 가능한 클라우드의 가상 머신. 이 클라우드 서버는 원할 때마다 실행할 수 있으며 온프레미스 서버와 마찬가지로 클라우드에 자체 서버를 배포해야 하고 하드웨어 및 업데이트 선택을 완전히 제어하려는 경우에 사용할 수 있습니다. 기계.

### 2. 스노우볼이란?

SnowBall은 AWS 환경 내부 및 외부에서 테라바이트 규모의 데이터를 전송할 수 있는 작은 애플리케이션입니다.

### 3. CloudWatch란 무엇입니까?

CloudWatch를 사용하면 EC2, RDS 인스턴스 및 CPU 사용률과 같은 AWS 환경을 모니터링할 수 있습니다. 또한 다양한 메트릭에 따라 경보를 트리거합니다.

### 4. Elastic Transcoder란 무엇입니까?

Elastic Transcoder는 다양한 해상도의 태블릿, 스마트폰, 노트북과 같은 다양한 장치를 지원하기 위해 비디오의 형식과 해상도를 변경하는 데 도움이 되는 AWS 서비스 도구입니다.

### 5. VPC는 ​​무엇을 이해합니까?

VPC는 Virtual Private Cloud의 약자입니다. 네트워킹 구성을 사용자 지정할 수 있습니다. VPC는 클라우드의 다른 네트워크와 논리적으로 격리된 네트워크입니다. 이를 통해 개인 IP 주소 범위, 인터넷 게이트웨이, 서브넷 및 보안 그룹을 가질 수 있습니다.

### 6. DNS 및 로드 밸런서 서비스는 어떤 유형의 클라우드 서비스에 속합니까?

DNS 및 Load Balancer는 IaaS-Storage Cloud Service의 일부입니다.

### 7. Amazon S3에서 사용할 수 있는 스토리지 클래스는 무엇입니까?

Amazon S3에서 사용할 수 있는 스토리지 클래스는 다음과 같습니다.

아마존 S3 표준
Amazon S3 표준-간헐적 액세스
Amazon S3 감소 중복 스토리지
아마존 빙하

### 8. T2 인스턴스가 무엇인지 설명하십시오.

T2 인스턴스는 적당한 기준 성능과 워크로드에 필요한 대로 더 높은 성능으로 버스트하는 기능을 제공하도록 설계되었습니다.

### 9. AWS의 키 페어란 무엇입니까?

키 쌍은 가상 머신에 대한 보안 로그인 정보입니다. 인스턴스에 연결하기 위해 공개 키와 개인 키가 포함된 키 쌍을 사용할 수 있습니다.

### 10. VPC당 얼마나 많은 서브넷을 가질 수 있습니까?

VPC당 200개의 서브넷을 가질 수 있습니다.

### 11. 다양한 유형의 클라우드 서비스를 나열하십시오.

다양한 유형의 클라우드 서비스는 다음과 같습니다.

서비스로서의 소프트웨어(SaaS)
서비스로서의 데이터(DaaS)
서비스로서의 플랫폼(PaaS)
서비스로서의 인프라(IaaS)

# 고급 AWS 질문

### 12. S3가 무엇인지 설명하십시오.

S3는 Simple Storage Service의 약자입니다. S3 인터페이스를 사용하여 웹의 어느 곳에서나 시간에 관계없이 원하는 양의 데이터를 저장하고 검색할 수 있습니다. S3의 경우 지불 모델은 "종량제"입니다.

### 13. Amazon Route 53은 어떻게 고가용성과 짧은 지연 시간을 제공합니까?

Amazon Route 53은 다음을 사용하여 고가용성과 짧은 지연 시간을 제공합니다.

전 세계적으로 분산된 서버 - Amazon은 글로벌 서비스이므로 전 세계적으로 DNS 서버가 있습니다. 전 세계 어디에서나 쿼리를 생성하는 모든 고객은 짧은 대기 시간을 제공하는 로컬 DNS 서버에 도달하게 됩니다.
종속성 - Route 53은 중요한 애플리케이션에 필요한 높은 수준의 종속성을 제공합니다.
최적의 위치 - Route 53은 가장 가까운 데이터 센터에서 요청을 보내는 클라이언트로 요청을 처리합니다. AWS는 전 세계에 데이터 센터를 보유하고 있습니다. 데이터는 요구 사항과 선택한 구성에 따라 전 세계 여러 지역에 위치한 여러 데이터 센터에 캐시될 수 있습니다. Route 53을 사용하면 필요한 데이터가 있는 모든 데이터 센터의 모든 서버가 응답할 수 있습니다. 이렇게 하면 가장 가까운 서버가 클라이언트 요청을 처리할 수 있으므로 처리하는 데 걸리는 시간이 줄어듭니다.

### 14. Amazon S3에 요청을 보내려면 어떻게 해야 합니까?

Amazon S3는 REST 서비스이며 기본 Amazon S3 REST API를 래핑하는 AWS SDK 래퍼 라이브러리 또는 REST API를 사용하여 요청을 보낼 수 있습니다.

### 15. AMI에는 무엇이 포함됩니까?

AMI에는 다음이 포함됩니다.

인스턴스의 루트 볼륨에 대한 템플릿입니다.
인스턴스를 시작하기 위해 AMI를 사용할 수 있는 AWS 계정을 결정하는 시작 권한.
인스턴스가 시작될 때 인스턴스에 연결할 볼륨을 결정하는 블록 디바이스 매핑입니다.

### 16. 다양한 유형의 인스턴스는 무엇입니까?

다음은 인스턴스 유형입니다.

컴퓨팅 최적화
메모리 최적화
스토리지 최적화
가속 컴퓨팅
범용
### 17. 가용 영역과 리전 간의 관계는 무엇입니까?

AWS 가용 영역은 Amazon 데이터 센터가 위치한 물리적 위치입니다. 반면 AWS 리전은 가용 영역 또는 데이터 센터의 모음 또는 그룹입니다. 

이 설정은 AWS 리전 내의 다른 데이터 센터에 VM을 배치할 수 있으므로 서비스의 가용성을 높이는 데 도움이 됩니다. 한 지역에서 데이터 센터 중 하나에 장애가 발생해도 클라이언트 요청은 동일한 지역에 있는 다른 데이터 센터에서 계속 처리됩니다. 따라서 이 배열은 데이터 센터가 다운되더라도 서비스를 사용할 수 있도록 도와줍니다.

### 18. Amazon VPC를 어떻게 모니터링합니까?

다음을 사용하여 Amazon VPC를 모니터링할 수 있습니다.

클라우드워치
VPC 흐름 로그

### 19. 비용에 따라 다른 유형의 EC2 인스턴스는 무엇입니까?

비용에 따른 세 가지 유형의 EC2 인스턴스는 다음과 같습니다.

온디맨드 인스턴스 - 이 인스턴스는 필요할 때 준비됩니다. 새로운 EC2 인스턴스가 필요하다고 느낄 때마다 온디맨드 인스턴스를 생성할 수 있습니다. 단기간에는 저렴하지만 장기간 복용하면 그렇지 않습니다.

스팟 인스턴스 - 이러한 유형의 인스턴스는 입찰 모델을 통해 구입할 수 있습니다. 이는 온디맨드 인스턴스보다 비교적 저렴합니다.

예약 인스턴스 - AWS에서는 1년 정도 예약할 수 있는 인스턴스를 생성할 수 있습니다. 이러한 유형의 인스턴스는 장기적으로 인스턴스가 필요할 것임을 미리 알고 있을 때 특히 유용합니다. 이러한 경우 예약 인스턴스를 생성하여 비용을 크게 절약할 수 있습니다.

### 20. EC2 인스턴스를 중지하고 종료하면 무엇을 이해합니까?

EC2 인스턴스를 중지한다는 것은 일반적으로 개인용 컴퓨터에서 하는 것처럼 인스턴스를 종료하는 것을 의미합니다. 이렇게 하면 인스턴스에 연결된 볼륨이 삭제되지 않으며 필요할 때 인스턴스를 다시 시작할 수 있습니다.

반면에 인스턴스를 종료하는 것은 인스턴스를 삭제하는 것과 같습니다. 인스턴스에 연결된 모든 볼륨이 삭제되며 나중에 필요한 경우 인스턴스를 다시 시작할 수 없습니다.

### 21. AWS에서 제공하는 최신 DB의 일관성 모델은 무엇입니까?

최종 일관성 - 데이터가 결국 일관성을 유지하지만 즉각적이지 않을 수 있음을 의미합니다. 이렇게 하면 클라이언트 요청을 더 빨리 처리할 수 있지만 초기 읽기 요청 중 일부가 오래된 데이터를 읽을 수 있습니다. 이러한 유형의 일관성은 데이터가 실시간일 필요가 없는 시스템에서 선호됩니다. 예를 들어, Twitter의 최근 트윗이나 Facebook의 최근 게시물이 몇 초 동안 표시되지 않으면 허용됩니다.

강력한 일관성 - 모든 DB 서버에서 데이터가 즉시 일관성을 유지하는 즉각적인 일관성을 제공합니다. 따라서. 이 모델은 데이터를 일관성 있게 만들고 이후에 요청을 다시 제공하기 시작하는 데 시간이 걸릴 수 있습니다. 그러나 이 모델에서는 모든 응답에 항상 일관된 데이터가 있음이 보장됩니다.

### 22. CloudFront에서 지역 타겟팅이란 무엇입니까?

지역 타겟팅을 사용하면 사용자의 지리적 위치를 기반으로 맞춤형 콘텐츠를 생성할 수 있습니다. 이를 통해 사용자와 더 관련이 있는 콘텐츠를 제공할 수 있습니다. 예를 들어, 지역 타겟팅을 사용하여 인도에 있는 사용자에게는 지방 단체 선거와 관련된 뉴스를 표시할 수 있지만 미국에 있는 사용자에게는 표시하고 싶지 않을 수 있습니다. 마찬가지로, 야구 토너먼트와 관련된 뉴스는 미국에 거주하는 사용자에게 더 관련성이 있고 인도에 거주하는 사용자에게는 관련성이 낮을 수 있습니다.

### 23. AWS IAM의 장점은 무엇입니까?

AWS IAM을 사용하면 관리자가 다양한 사용자 및 그룹에 세분화된 수준의 액세스를 제공할 수 있습니다. 서로 다른 사용자 및 사용자 그룹은 생성된 서로 다른 리소스에 대해 서로 다른 수준의 액세스가 필요할 수 있습니다. IAM을 사용하면 특정 액세스 수준으로 역할을 생성하고 사용자에게 역할을 할당할 수 있습니다. 

또한 연동 액세스라고 하는 IAM 역할을 생성하지 않고도 리소스에 대한 액세스를 사용자 및 애플리케이션에 제공할 수 있습니다.

### 24. 보안 그룹이 무엇을 이해합니까?

AWS에서 인스턴스를 생성할 때 퍼블릭 네트워크에서 해당 인스턴스에 액세스할 수도 있고 원하지 않을 수도 있습니다. 또한 해당 인스턴스를 다른 네트워크가 아닌 일부 네트워크에서 액세스할 수 있기를 원할 수 있습니다.

보안 그룹은 인스턴스에 대한 액세스를 제어할 수 있는 일종의 규칙 기반 가상 방화벽입니다. 액세스를 허용하거나 거부할 포트 번호, 네트워크 또는 프로토콜을 정의하는 규칙을 만들 수 있습니다.

### 25. 스팟 인스턴스와 온디맨드 인스턴스란 무엇입니까?

AWS가 EC2 인스턴스를 생성할 때 일부 컴퓨팅 용량 및 처리 능력 블록이 사용되지 않은 채로 남아 있습니다. AWS는 이러한 블록을 스팟 인스턴스로 릴리스합니다. 스팟 인스턴스는 용량이 사용 가능할 때마다 실행됩니다. 애플리케이션을 실행할 수 있는 시점과 애플리케이션이 중단될 수 있는 시점에 대해 유연하다면 좋은 옵션입니다.

반면 온디맨드 인스턴스는 필요할 때 생성할 수 있습니다. 이러한 인스턴스의 가격은 고정되어 있습니다. 이러한 인스턴스는 명시적으로 종료하지 않는 한 항상 사용할 수 있습니다.

### 26. 연결 드레이닝을 설명합니다.

연결 드레이닝은 업데이트되거나 제거될 서버가 현재 요청을 처리할 수 있도록 하는 AWS에서 제공하는 기능입니다. 

연결 드레이닝이 활성화된 경우 로드 밸런서는 나가는 인스턴스가 특정 기간 동안 현재 요청을 완료하도록 허용하지만 새 요청을 보내지는 않습니다. 연결 드레이닝이 없으면 나가는 인스턴스가 즉시 꺼지고 해당 인스턴스에서 보류 중인 요청에 오류가 발생합니다.

### 27. 상태 저장 및 상태 비저장 방화벽이란 무엇입니까?

상태 저장 방화벽은 정의된 규칙의 상태를 유지 관리하는 방화벽입니다. 인바운드 규칙만 정의하면 됩니다. 정의된 인바운드 규칙에 따라 아웃바운드 트래픽이 자동으로 흐르도록 허용합니다. 

반면에 상태 비저장 방화벽에서는 인바운드 및 아웃바운드 트래픽에 대한 규칙을 명시적으로 정의해야 합니다. 

예를 들어 포트 80의 인바운드 트래픽을 허용하는 경우 상태 저장 방화벽은 포트 80으로의 아웃바운드 트래픽을 허용하지만 상태 비저장 방화벽은 허용하지 않습니다.

### 28. AWS에서 파워 유저 액세스란 무엇입니까?

관리자 사용자는 AWS 리소스의 소유자와 유사합니다. 그는 리소스를 생성, 삭제, 수정 또는 볼 수 있으며 AWS 리소스에 대한 권한을 다른 사용자에게 부여할 수도 있습니다.

고급 사용자 액세스는 사용자 및 권한을 관리할 수 있는 기능 없이 관리자 액세스를 제공합니다. 즉, 고급 사용자 액세스 권한이 있는 사용자는 리소스를 생성, 삭제, 수정 또는 볼 수 있지만 다른 사용자에게 권한을 부여할 수는 없습니다.

### 29. 인스턴스 스토어 볼륨과 EBS 볼륨이란 무엇입니까?

인스턴스 스토어 볼륨은 인스턴스가 작동하는 데 필요한 임시 데이터를 저장하는 데 사용되는 임시 스토리지입니다. 인스턴스가 실행되는 동안 데이터를 사용할 수 있습니다. 인스턴스가 꺼지는 즉시 인스턴스 스토어 볼륨이 제거되고 데이터가 삭제됩니다.

반면 EBS 볼륨은 영구 저장소 디스크를 나타냅니다. EBS 볼륨에 저장된 데이터는 인스턴스가 꺼진 후에도 사용할 수 있습니다.

### 30. AWS의 복구 시간 목표 및 복구 시점 목표는 무엇입니까?

복구 시간 목표 - 서비스 중단과 서비스 복원 사이에 허용 가능한 최대 지연입니다. 이는 서비스를 사용할 수 없는 허용 가능한 시간 창으로 해석됩니다.

복구 시점 목표 - 마지막 데이터 복구 시점 이후 허용 가능한 최대 시간입니다. 이는 마지막 복구 지점과 서비스 중단 사이에 있는 허용 가능한 데이터 손실량으로 해석됩니다.

### 31. Amazon S3에 100MB가 넘는 파일을 업로드하는 방법이 있습니까?

예, AWS의 멀티파트 업로드 유틸리티를 사용하면 가능합니다. 멀티파트 업로드 유틸리티를 사용하면 더 큰 파일을 독립적으로 업로드되는 여러 파트로 업로드할 수 있습니다. 이러한 부분을 병렬로 업로드하여 업로드 시간을 줄일 수도 있습니다. 업로드가 완료되면 부품이 단일 개체 또는 파일로 병합되어 부품이 생성된 원본 파일이 생성됩니다.

### 32. EC2 인스턴스가 실행 중이거나 중지된 상태에서 프라이빗 IP 주소를 변경할 수 있습니까?

아니요, EC2 인스턴스의 사설 IP 주소는 변경할 수 없습니다. EC2 인스턴스가 시작되면 부팅 시 프라이빗 IP 주소가 해당 인스턴스에 할당됩니다. 이 개인 IP 주소는 전체 수명 동안 인스턴스에 연결되며 변경할 수 없습니다.

### 33. Autoscaling에서 수명 주기 후크의 용도는 무엇입니까?

수명 주기 후크는 자동 확장에 사용되어 축소 또는 확장 이벤트에 추가 대기 시간을 둡니다.

### 34. 사용자의 비밀번호에 대해 설정할 수 있는 정책은 무엇입니까?

사용자의 비밀번호에 대해 설정할 수 있는 정책은 다음과 같습니다.

비밀번호의 최소 길이를 설정할 수 있습니다.
사용자에게 비밀번호에 하나 이상의 숫자나 특수 문자를 추가하도록 요청할 수 있습니다.
대문자, 소문자, 숫자 및 영숫자가 아닌 문자를 포함한 특정 문자 유형의 요구 사항 할당.
자동 암호 만료를 적용하고, 이전 암호의 재사용을 방지하고, 다음 AWS 로그인 시 암호 재설정을 요청할 수 있습니다.
사용자가 암호 만료를 허용한 경우 AWS 사용자가 계정 관리자에게 연락하도록 할 수 있습니다.