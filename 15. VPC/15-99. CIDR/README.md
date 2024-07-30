# CIDR (IPv4)

CIDR(Classless Inter-Domain Rouding)는 IP Address를 할당하는 방법.

일반적으로 **AWS networking**과 **Security Groups**에서 사용됨.

## 구성요소

### Base IP

XX.XX.XX.XX 에 속한 IP를 표현함.

총 32bit의 길이를 가짐.

각 단위별로 8bit씩 표현하고 있음.

EX) 10.0.0.0, 192.168.0.0 등.

### Subnet Mask

IP에서 **몇 개의 Bit**가 바뀔수 있는지 정의함.

/**Digit** : 32 - Digit 개의 Bit만 변화할 수 있음을 의미.

* **Example**

    /0 : 32bit 모두 변화할 수 있음을 의미.

    /24 : 마지막 8bit만 변화할 수 있음을 의미.

    /32 : 마지막 0bit만 변화할 수 있음을 의미.

다음과 같이 치환이 가능함.

* /8 = 255.0.0.0
* /16 = 255.255.0.0
* /24 = 255.255.255.0
* /32 = 255.255.255.255

## Example

* XX.YY.ZZ.WW/**32** : XX.YY.ZZ.WW 하나의 IP를 의미함.

* 0.0.0.0/**0** : 모든 IP 주소를 의미함.

* 192.168.0.0/**26** : 192.168.0.0 ~ 192.168.0.63 까지의 총 64개의 IP 주소를 의미함.

## Private IP

**Internet Assigned Numbers Authority**에서는 IPv4 IP 주소의 일부를 **private**(LAN)를 사용할 수 있도록 허락함.

* 10.0.0.0 ~ 10.255.255.255 (10.0.0.0/8) : Big Network에서 사용가능한 Private IP 범위

* 172.16.0.0 ~ 172.31.255.255(172.16.0.0/12) : AWS의 기본 **VPC** IP 범위

* 192.168.0.0 ~ 192.168.255.255(192.168.0.0/16) : Home Network IP 범위

나머지는 Public Internet의 IP 범위임.