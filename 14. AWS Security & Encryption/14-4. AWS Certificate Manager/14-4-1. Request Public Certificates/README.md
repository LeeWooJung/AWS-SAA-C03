# Request Public Certificates

AWS Certificate Manager (ACM)에서 Public Certificate를 요청하는 과정은 다음과 같이 이루어짐.

## 인증서 요청 시작

ACM 콘솔에 로그인한 후, "**Request a Certificate**" 버튼을 클릭하여 인증서 요청을 시작함.

## 인증서 유형 선택

"Request a public certificate"를 선택함. 이 옵션은 도메인 이름의 공용 SSL/TLS 인증서를 요청하는 것임.

## 도메인 이름 입력

인증서를 요청할 도메인 이름을 입력함. 

여러 도메인 이름을 입력할 수도 있음.

### Example

* **Fully Qualified Domain Name**

    ex) www.example.com

* **Wildcard Domain**

    ex) *.example.com

## 도메인 검증 방법 선택

도메인 소유권을 검증하기 위해 두 가지 방법 중 하나를 선택할 수 있음.

### DNS 검증

도메인 이름에 대한 DNS 설정(ex. Route53)에 **ACM에서 제공하는 CNAME 레코드를 추가**함. 

이 방법은 권장되며 **자동 갱신이 가능**함.

### Email 검증

도메인 이름의 **WHOIS 정보에 나열된 이메일 주소로 검증 이메일**을 보냄. 

이메일에 포함된 링크를 클릭하여 검증함.

## 검증 요청 제출
"Request" 버튼을 클릭하여 인증서 요청을 제출함.

## 도메인 검증

도메인 검증 방법에 따라 도메인 소유권을 검증함.

### DNS 검증

도메인의 DNS 설정에 ACM에서 제공한 CNAME 레코드를 추가함. 

DNS 변경 사항이 전파되면 ACM이 자동으로 도메인을 검증함.

### Email 검증

도메인 소유자에게 전송된 이메일의 링크를 클릭하여 검증 절차를 완료함.


## 인증서 발급

도메인 소유권이 성공적으로 검증되면 ACM은 인증서를 발급함.

Public Certificate의 경우 자동 갱신(automatic renewal)으로 등록됨.

**ACM은 자동으로 ACM-generated certificates를 만료 60일 전에 재생성**함.

**이 과정은 몇 분에서 몇 시간까지 걸릴 수 있음**.

## 인증서 사용

발급된 인증서는 ACM 콘솔에서 확인할 수 있으며, ELB, CloudFront, API Gateway 등 AWS 서비스에 배포할 수 있음.