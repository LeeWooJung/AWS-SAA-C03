# [RDS Proxy](https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/UserGuide/rds-proxy.html)

## RDS Proxy

* **Amazon RDS Proxy**는 Amazon Relational Database Service (RDS)와 Amazon Aurora를 위한 고가용성 및 확장성을 제공하는 데이터베이스 중간 계층 서비스.  
* RDS Proxy는 **애플리케이션과 데이터베이스 간의 연결을 관리**하고, **연결 풀링과 트랜잭션 관리** 기능을 통해 데이터베이스의 성능과 효율성을 향상시킴.  

### 기능

1. **연결 풀링**(Connection Pooling)  
    * RDS Proxy는 데이터베이스 연결을 풀링하여 **애플리케이션의 연결 요청을 효율적으로 처리**.  
    * 이는 데이터베이스 서버의 연결 설정 및 해제 부담을 줄여주고 성능을 향상시킴.

2. **트랜잭션 관리**(Transaction Management)  
    * RDS Proxy는 **트랜잭션을 관리**하고 트랜잭션 중단 시 안전하게 복구함.  
    * 이를 통해 애플리케이션의 복잡한 트랜잭션 논리를 간소화할 수 있음.

3. **자동 장애 조치**(Automatic Failover)  
    * RDS Proxy는 데이터베이스 인스턴스 장애 시 자동으로 대체 인스턴스로 장애 조치를 수행.  
    * 이는 고가용성을 보장하고 애플리케이션의 다운타임을 최소화함.

4. **보안(Security)**  
    * RDS Proxy는 AWS Identity and Access Management (IAM) 및 데이터베이스 인증을 지원하여 보안성을 강화함.  
    * 또한, 연결을 암호화하여 데이터 전송의 안전성을 보장.

5. **세션 캐싱**(Session Caching)  
    * RDS Proxy는 **세션 캐싱**을 통해 애플리케이션의 세션 상태를 유지하고, **세션 재사용**을 통해 성능을 최적화함.

### 장점

1. **성능 향상**  
    * 다수의 애플리케이션 요청을 효율적으로 처리함으로써 데이터베이스 성능을 향상시킴.  
    * 이는 연결 오버헤드를 줄이고, 데이터베이스 리소스를 최적화함.

2. **고가용성**  
    * 자동 장애 조치 기능을 통해 고가용성을 제공하며, 데이터베이스 장애 시 애플리케이션의 연속성을 보장.

3. **비용 절감**  
    * **연결 풀링**과 **세션 캐싱**을 통해 데이터베이스 인스턴스의 부하를 줄이고, 비용 효율적인 운영을 가능하게 함.

4. **보안 강화**  
    * IAM 통합 및 데이터 암호화를 통해 애플리케이션과 데이터베이스 간의 보안성을 강화함.

### Public Access

* Amazon RDS Proxy는 보안 및 최적 성능을 위해 **기본적으로 퍼블릭 액세스를 지원하지 않음**.  
* 이는 RDS Proxy가 VPC(가상 사설 클라우드) 내에서만 액세스 가능하도록 설정된다는 의미.  
* 이러한 설정은 데이터베이스 프록시를 외부 인터넷에 노출하지 않음으로써 보안을 강화함.

### RDS Proxy 특징

1. **VPC 내부 액세스**  
    * RDS Proxy는 **VPC 내부에서 실행**되며, VPC 내의 애플리케이션 및 리소스에서만 접근이 가능.  
    * 이를 통해 외부 공격으로부터 데이터베이스를 보호.

2. **보안 그룹**  
    * RDS Proxy는 보안 그룹을 통해 인바운드 및 아웃바운드 트래픽을 제어.  
    * 보안 그룹 규칙을 설정하여 특정 IP 주소나 서브넷에서만 접근을 허용할 수 있음.

3. **IAM 통합**  
    * AWS Identity and Access Management (IAM)를 통해 RDS Proxy에 대한 액세스를 제어할 수 있음.  
    * 이를 통해 특정 IAM 역할이나 사용자에게만 프록시 접근 권한을 부여할 수 있음.

4. **프라이빗 서브넷 배포**:
    * RDS Proxy는 프라이빗 서브넷에 배포할 수 있으며, 이를 통해 외부 인터넷 접근을 차단할 수 있음.  
    * **VPN이나 Direct Connect를 통해서만 접근하도록 설정할 수 있음**.

### Use Case

1. **서버리스 애플리케이션**  
    * AWS Lambda와 같은 서버리스 환경에서 데이터베이스 연결 수요가 급증할 때 RDS Proxy를 사용하여 효율적으로 관리함.

2. **다중 사용자 애플리케이션**  
    * 대규모 사용자 기반을 가진 애플리케이션에서 다수의 연결 요청을 효율적으로 처리하여 성능을 최적화함.

3. **고가용성이 필요한 애플리케이션**  
    * 데이터베이스 장애 시에도 애플리케이션의 연속성을 유지하고자 할 때 사용함.

## Conclusion

**Amazon RDS Proxy**는 **데이터베이스 연결 관리, 성능 최적화, 고가용성 보장, 보안 강화** 등의 기능을 제공하여 RDS 및 Aurora 환경에서 애플리케이션의 안정성과 효율성을 크게 향상시킴.  
이를 통해 데이터베이스 운영의 복잡성을 줄이고, 비용 효율적인 데이터베이스 관리를 가능하게 함.

## Architecture Example

![RDS Proxy example Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/50905d35-5768-4aee-b52e-f6ab8424b63b)