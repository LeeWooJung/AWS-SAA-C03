# Import Public Certificate

**ACM 외부에서 생성한 Certificate**를 Import 해오는 것을 의미함.

ACM 외부에서 생성한 것을 가져오는 것이기 때문에 **자동 Renewal할 수 없음**. 만료 이전에 다시 새로운 Certificate를 Import해야함.

ACM은 Certificate의 **만기 이전에 매일 만기 Event**를 전송함. 이는 **만기 45일전**부터 시작함.

* 45일과 같은 **구성**을 수정할 수 있음.

* ACM에서 생성하는 Event는 **EventBridge**로 전송됨.

**AWS Config**에서 **acm-certificate-expiration-check**와 같은 Managed Rule을 사용하여 Certificate의 만기를 확인할 수 있음. 이 때, **만기 전 날짜에 대한 구성**을 수정할 수 있음.