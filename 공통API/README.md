# API 인증 및 예외처리

## 개요

* 사전 준비 사항
	> 디지털트윈 OpenAPI를 사용하려면 먼저 디지털트윈 개발자 센터에서 애플리케이션을 등록하고 API KEY를 발급받아야 합니다. API KEY는 인증된 어플리케이션인지 확인하는 수단이며, 애플리케이션이 등록되면 발급됩니다. API KEY는 디지털트윈 OPENAPI를 호출할때 HTTP 요청 파라미터에 포함해서 전송해야 API를 호출할 수 있습니다. 현재 디지털트윈 개발자 센터가 오픈되지 않은 관계로 오프라인으로 연락을 주시거나 정식 오픈이전까지는 테스트 API KEY를 사용하시면 됩니다.

	```
	테스트 API KEY는 아래와 같습니다.	
	테스트 API KEY : c81cc262-1ecd-463c-8485-8be46408eb99
	```

* 디바이스 KEY 발급
	> 최초 사용자 단말에 어플리케이션 설치시 디바이스정보를 등록하고 디바이스 KEY를  발급받아야 합니다. 디바이스 KEY는 인증된 디바이스인지 확인하는 수단이며, 디바이스가 등록되면   발급됩니다. 디바이스 KEY는 디지털트윈 OPENAPI를 호출할때 HTTP 요청 파라미터에 포함해서 전송해야 하며 디지털트윈내에 행태분석, 통계목적, 디바이스의  카메라 시야각등의 물리적인 정보를 취득하여 맞춤정보를 제공하는데 이용됩니다.

* REST방식의 URL 요청 예시
	```
	https://api.xrstudio.co.kr/v1/tiles?level=19&longitude=127.153885&latitude=35.81518&key={디바이스KEY}
	```

* Pub/Sub방식의 TOPIC 예시
	```
	topic : /cameras/{디바이스 KEY}
	```
	
## 디바이스 KEY 발급
* 소개
	> 최초 프로그램 설치시 어플리케이션, 디바이스별로 디바이스 KEY를 획득하여 타 API의 인증에 사용할 수 있도록 디바이스 KEY를 저장해놓습니다.

* 요청 URL
	```
	https://api.xrstudio.co.kr/v1/devices HTTP1.1 / POST
	```
* 요청파라미터

|파라미터|선택|설명|유효값|
|----|----------------|-----------------|-----------|
|os|O/1|운영체제|window / android / ios 등|
|agent|O/1|구동 플랫폼|Mozilla/5.0 / steam vr 등|
|model|O/1|단말기 모델명|SM-G970N 등|
|fov|O/1|카메라 시야각|0.0~180.0|
|apikey|M/1|발급받은 API KEY||

* 응답결과(JSON)

|Name|Accessor Type(s)|Component Type(s)|Description|
|----|----------------|-----------------|-----------|
|`POSITION`|`"VEC3"`|`5126`&nbsp;(FLOAT)|XYZ vertex position displacements|
|`NORMAL`|`"VEC3"`|`5126`&nbsp;(FLOAT)|XYZ vertex normal displacements|
|`TANGENT`|`"VEC3"`|`5126`&nbsp;(FLOAT)|XYZ vertex tangent displacements|

* 테스트 디바이스 KEY 
	```
	13d4640d-a62c-4ea1-9dad-2b6690627fd3
	```
	