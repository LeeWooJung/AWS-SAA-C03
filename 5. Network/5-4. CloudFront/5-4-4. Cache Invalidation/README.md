# [CloudFront Cache Invalidation](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html)

## Cache Invalidation

* AWS CloudFront의 **Cache Invalidation**은 CDN(Content Delivery Network) 엣지 로케이션에 캐시된 객체를 삭제하는 기능임.  
* 이 기능은 **새로운 콘텐츠를 사용자에게 빠르게 제공하거나, 업데이트된 콘텐츠가 배포되었을 때 이를 즉시 반영**하기 위해 사용됨.

* **캐시**  
CloudFront는 엣지 로케이션에 콘텐츠를 캐시하여 사용자에게 빠른 응답을 제공함.
* **Invalidation**  
특정 객체 또는 객체 그룹을 캐시에서 삭제하여 CloudFront가 **오리진 서버에서 새로운 버전을 가져오도록 강제**함.

## Cache Invalidation 사용 시기

* **콘텐츠 업데이트**  
기존 콘텐츠를 수정하거나 새로운 버전을 배포할 때.
* **정책 변경**  
접근 권한이나 콘텐츠의 유효 기간과 같은 정책이 변경될 때.
* **오류 수정**  
캐시된 콘텐츠에 오류가 있어 즉시 교체가 필요할 때.

## Cache Invalidation의 종류

* **단일 객체**  
    * 특정 파일을 지정하여 캐시에서 삭제함.
* **와일드카드 패턴**  
    * 특정 패턴에 맞는 여러 객체를 한 번에 삭제함.  
    * 예를 들어, images/*는 모든 이미지 파일을 삭제함.

## Cache Invalidation의 동작 방식

* **Invalidation 요청 생성**  
CloudFront 콘솔, CLI 또는 API를 사용하여 Invalidation 요청을 생성함.
* **요청 처리**  
CloudFront는 각 엣지 로케이션에서 해당 객체를 찾아 캐시에서 삭제함.
* **새로운 요청 처리**  
삭제된 객체에 대한 새로운 사용자 요청이 들어오면, CloudFront는 오리진 서버에서 최신 버전을 가져와 캐시함.

## 비용

* **무료 할당량**  
매달 1,000개의 Invalidation 요청이 무료로 제공됨.
* **추가 비용**  
무료 할당량을 초과하면 Invalidation 요청당 추가 비용이 발생함.

## 캐시 만료와의 비교
* **Cache Invalidation**  
수동으로 특정 객체를 캐시에서 삭제하는 것.
* **캐시 만료**(Time-to-Live, TTL)  
객체의 유효 기간이 끝나면 자동으로 캐시에서 삭제됨. 설정된 TTL이 만료되면 CloudFront는 오리진에서 최신 객체를 가져옴.