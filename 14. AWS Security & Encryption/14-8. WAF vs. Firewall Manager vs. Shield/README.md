# WAF vs. Firewall Manager vs. Shield

AWS WAF, AWS Firewall Manager, AWS Shield는 모두 보안을 강화하기 위한 서비스지만, 각각의 기능과 사용 목적이 다름.

## AWS WAF (Web Application Firewall)

**웹 애플리케이션을 다양한 웹 기반 공격으로부터 보호**함 (예: SQL 인젝션, 크로스 사이트 스크립팅(XSS)).

### Use case

웹 애플리케이션 **앞에 배치하여 악의적인 트래픽을 차단**함.

Resource에 대한 **세분화**된 보호를 원할 때는 WAF만 사용하는 것이 좋음.

### 특징

사용자 정의 가능한 규칙을 통해 **HTTP/S 트래픽을 필터링**함. 

IP 블로킹, 요청 제한, 사용자 정의 요청 필터링이 가능함.

## AWS Shield

DDoS(Distributed Denial of Service) 공격으로부터 보호함.

### Use case

주요 애플리케이션과 데이터의 가용성을 유지하기 위해 **DDoS 공격을 방어**함.

### 특징

* **Shield Standard**

    기본 DDoS 보호로 모든 AWS 고객에게 무료로 제공됨.

* **Shield Advanced**

    추가 비용이 들며, 더 강력한 DDoS 보호와 24/7 DDoS 대응 팀 지원, 비용 보호 등이 포함됨.

## AWS Firewall Manager

**여러 AWS 계정에 걸쳐 중앙에서 보안 정책을 관리하고 배포**함.

### Use case

조직 전체에 일관된 보안 규칙을 적용하고 관리함.

### 특징

**AWS Organizations와 통합되어, 여러 계정에 대해 WAF 규칙, 보안 그룹 규칙, DDoS 보호를 중앙에서 관리**함.


-----------------------

각각의 서비스가 다루는 보안 측면이 다르기 때문에, 이들을 결합하여 사용하면 종합적인 보안 보호를 제공할 수 있음.

## AWS WAF와 AWS Shield 결합

### 웹 애플리케이션 보호

AWS WAF를 사용하여 웹 애플리케이션에 대한 특정 공격을 차단하고, AWS Shield를 통해 대규모 DDoS 공격을 방어함.

e-commerce 사이트, 금융 서비스 애플리케이션 등, 높은 가용성과 보안을 요구하는 웹 애플리케이션에 적합함.

## AWS WAF와 AWS Firewall Manager 결합

AWS Firewall Manager를 사용하여 여러 계정에 걸쳐 **AWS WAF 규칙을 중앙에서 관리하고 배포**함.

대규모 조직이 **여러 계정에서 일관된 웹 애플리케이션 방어 규칙을 유지**하고자 할 때 적합함.

## AWS Shield와 AWS Firewall Manager 결합

AWS Shield Advanced를 사용하여 DDoS 공격을 방어하고, **AWS Firewall Manager를 통해 DDoS 보호 정책을 여러 계정에 걸쳐 관리**함.
