# 입력 변수

> https://www.terraform.io/language/values/variables

```
variable "image_id" {
  type = string
}

variable "availability_zone_names" {
  type    = list(string)
  default = ["us-east-1a"]
}
```

- type:
	- 일반 타입
		- string
			- "app_server"
		- number
			- 1
			- 1.0
		- bool
			- true
			- false
	- 복합 타입
		- list / tuple
			- [a, b, c]
		- map / object
			- `{a = abc, b = xyz}`
- default: 기본 값
- description: 설명

```
variables abc {
  type = list(string)
  # ["a", "b"]
  type = list(number)
  # [1, 2]
}
```

## 변수 값 할당

### -var 옵션

``` bash
terraforn plan -var "instance_name=xyz"
```

### terraform.tfvars 파일
`terraform.tfvars`
```
instance_name = "xyz"
```