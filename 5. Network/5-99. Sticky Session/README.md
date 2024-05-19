# Sticky Sessions (Sesson Affinity)

## Sticky Session

## 설명

로드 밸런서를 통해 여러 대의 서버로 분산된 트래픽을 처리할 때 사용되는 기능. 이와 같은 **Sticky session을 사용하려면 클라이언트가 쿠키를 지원**해야 함.

* **정의**  
스티키 세션은 클라이언트가 처음 접속한 서버에만 고정되어, 그 서버만 해당 사용자의 요청을 처리하는 방식.
* **예시**  
사용자가 웹 애플리케이션에 접속하면 로드 밸런서는 해당 사용자를 처리할 서버를 선택함.  
이후 해당 사용자의 모든 요청은 처음 접속한 서버로만 전달됨.  
예를 들어, User1이 1번 서버에 세션을 생성하면 이후 User1의 모든 요청은 1번 서버로만 보내짐.
* **장점**  
    - 세션을 여러 곳에서 공유할 필요가 적어짐.
* **단점**  
    - 부하 해결 지연  
    **부하가 즉각적으로 해결되지 않음**. 특정 서버에 과부하가 발생하면 다른 서버로 요청을 분산시키는 로드 밸런서의 역할이 필요함.

스티키 세션은 특정 상황에서 유용하지만, 트래픽 분산과 세션 관리를 고려할 때 주의해야 함.  
만약 정합성 이슈를 해결하고 가용성과 트래픽 분산을 확보하려면 세션 클러스터링(Session Clustering) 방식을 고려할 수 있음. 세션 클러스터링은 여러 서버 간에 세션을 동일하게 유지하도록 설정하여 세션 문제를 해결함.

## Session vs. Cookie

* **쿠키**  
    - 쿠키는 서버의 자원을 전혀 사용하지 않음.
    - 쿠키는 클라이언트 측에 저장됨.
    - 변질되거나 스니핑 당할 우려가 있어 보안에 취약함.
    - 만료기간이 있지만, 클라이언트 측에 파일로 저장되기 때문에 브라우저를 종료 해도 정보 유지 가능.
    - 만료기간 까지 쿠키 유지 가능.
    - 클라이언트 측에 저장되기 때문에 속도 면에서 우수함.
* **세션**  
    - 세션은 서버의 자원을 사용.
    - 보안 면에서 세션이 쿠키 보다 우수
    - 만료기간이 있지만, 브라우저가 종료되면 만료기간에 상관 없이 삭제됨.
    - 서버 측에서 처리되기 때문에 속도 면에서 느림.

## 사용

* [Classic Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-1.%20Classic%20Load%20Balancer(deprecated))
    - Cookie가 Stickiness를 위해 사용되며 만료 기간이 존재함.
* [Application Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-2.%20Application%20Load%20Balancer)
    - Cookie가 Stickiness를 위해 사용되며 만료 기간이 존재함.
* [Network Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-3.%20Network%20Load%20Balancer)
    - NLB는 Cookie를 사용하지 않음.

## Application-based Cookies

* **정의**  
    - 클라이언트가 처음 접속한 서버에만 고정되어, 그 서버만 해당 사용자의 요청을 처리하는 방식.
* **동작 방식**  
    - 클라이언트가 처음 요청을 보내면 로드 밸런서는 해당 요청을 처리할 서버를 선택하고, 쿠키를 생성.
    - 이 쿠키는 어떤 원본 서버로 요청을 전달할지를 인코딩.
    - 이후 동일한 클라이언트가 같은 로드 밸런서에 요청을 보낼 때, 쿠키에 인코딩된 원본 서버로 요청이 전달.
    - 이 쿠키의 지속 기간 동안과 원본 서버가 정상적인 상태인 동안에만 해당 서버로 요청이 전달.
    - 쿠키가 만료되거나 원본 서버가 비정상 상태가 되면 새로운 원본 서버가 선택되고 사용됨.
* **기본 지속 시간**  
    - 모든 쿠키 기반 세션은 기본적으로 23시간임. 사용자 정의 세션 **TTL**을 설정할 수도 있음.
* **보안**  
    - HTTPS를 사용하고 있을 때, 세션 쿠키는 안전하며, **HttpOnly**는 항상 활성화되어 크로스 사이트 스크립팅 공격을 방지함.
* **종류**
    - Custom Cookie  
        - Target에 의해 생성됨
        - 각 Target group에 의해 개별적으로 특정지을 수 있는 이름으로 설정되어야 함.
        - AWSALB, AWSALBAPP, AWSALBTG는 ELB에 의해 사용되므로 이름에 들어가면 안됨.
    - Application Cookie
        - Load Balancer에 의해 생성됨.
        - Cookie의 이름은 AWSALBAPP임.

## Duration-based Cookies

* **정의**  
로드 밸런서가 세션 지속성을 위해 특정 기간을 정의하는 쿠키를 발급함.
* **동작 방식**  
    - 클라이언트 요청을 받을 때마다 해당 쿠키가 존재하는지 확인함.
    - 지정된 기간이 경과하고 쿠키가 만료되면 세션은 더 이상 고정되지 않음.
* **생성**
    - Load Balancer에 의해 생성됨.
    - Cookie의 이름은 AWSALB(Application Load Balancer), AWSELB(Classic Load Balancer)임.