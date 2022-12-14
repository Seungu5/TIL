# 구성파일

Terraform Configure File

- `.tf`
- `.tf.json` : json 형식

인코딩 : Unicode
디렉토리 : 현재 작업 디렉토리 위치에 따라서 해당 디렉토리의 `.tf`, `.tf.json` 모두 읽어서 실행

## 구성 파일
```
<BLOCK TYPE> <BLOCK LABEL> ... {
	ARGUMENT
	KEY = VALUE
}
```

### 테라폼 블록
```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.27"
    }
  }

  required_version = ">= 0.14.9"
}
```

- aws: 프로바이더의 이름
- source: 프로바이더의 종류
- version: 프로바이더의 버전
	- 4.10: 특정 버전
	- ~> 3.12: 특정 버전 이상
		- 3.12: 최소 버전

### 프로바이더 블록
```
provider "aws" {
  profile = "default"
  region  = "us-east-1"
}
```

- provider "aws": terraform 블록 이름 매칭
- profile: aws 자격증명 파일의 프로필
	- region

## 리소스 블록
```
resource "RESOURCE_TYPE" "NAME" {
  ARGUMENT = VALUE
}
```

- RESOURCE_TYPE: 리소스 종료
- NAME: 리소스 이름(테라폼에서 구분 하기 위한 이름)
- ARGUMENT: 인자/속성

## 실행 순서

### 초기화

``` bash
terraform init
```

프로바이더 플러그인 설치
- 최초로 프로바이더 설치
- 프로바이더 버전 업데이트

### 포멧팅
``` bash
terraform fmt
```

- 새로운 파일 작성
- 기존 파일 변경

### 유효성 검증
``` bash
terraform validate
```

### 계획
``` bash
terraform plan
```

### 적용
``` bash
terraform apply
```

### 제거
``` bash
terraform destroy
```

### 상태 확인
- `terraform.tfstate`: 현재상태
- `terraform.tfstate.backup`: 직전 상태

``` bash
terraform show
terraform state list
terraform state show aws_instance.app_server
```

### 상태 재 동기화
``` bash
terraform refresh
```

## 리소스 생성 순서
- 의존 관계가 없는 리소스는 병렬로 실행
- 의존 관계가 있는 경우 의존 관계에 따라서 순서가 정해지게 됨

### 명시적 의존성
```
resource "aws_instance" "app_server" {

  depends_on = [
    aws_s3_bucket.app_bucket
  ]
}
```

> https://www.terraform.io/language/meta-arguments/depends_on