# IPv6

IPv6는 IPv4의 후발주자로 **IPv4가 제공하는 IP Address가 줄어듦에 따라 생성됨**.

IPv6는 3.4 x 10의 38승 만큼의 IP Address를 제공하기 위해 디자인됨.

## Format

IPv6의 Format은 다음과 같음.

> x.x.x.x.x.x.x.x

여기서 x는 hexadecimal 이며, **0000부터 FFFF**까지임.

* **Example**

    * 2001:db8:3333:4444:cccc:eeee:dddd:ffff
    * 2001:db8:: 은 뒤 6개의 Hexadecimal이 0임을 뜻함.
    * ::3234:FFFF 는 앞 6개의 Hexadecimal이 0임을 뜻함.

## in AWS

AWS에서 사용되는 **모든 IPv6** 주소는 **Public**이며 **Internet Routable**임.

Private Network에서 사용될 수 없음.

## in VPC

VPC와 subnet에서 **IPv4**는 **비활성화 될 수 없음**.

하지만, **IPv6**는 활성화/비활성화 될 수 있으며, **IPv4와 같이 사용될 수 있음**(dual-stack mode).

VPC 내부에서 생성된 EC2 인스턴스는 **최소 하나의 Private IPv4**와 **Public IPv6**를 가질 수 있음.

위와 같은 EC2 인스턴스는 **Internet Gateway**에서 **IPv4 또는 IPv6**를 이용하여 인터넷에 연결할 수 있음.

EC2 인스턴스는 무조건 IPv4를 할당받아야 하는데, **만약 VPC**에서 EC2 인스턴스가 생성되지 않는다면, **IPv6 문제가 아니라 할당할 IPv4가 없다는 의미**임. 따라서 이를 해결하기 위해 **새로운 IPv4 CIDR block**을 생성해야 함.

## Engress-only Internet Gateway

IPv6만 사용할 수 있음.

VPC에 존재하는 EC2 instances의 **Outbound Connection**만 허용함. 따라서 Public Internet에서는 **Engress-only Internet Gateway로 IPv6 연결을 하지 못함**.

Engress-only Internet Gateway를 생성하면, **Route Table**을 업데이트 해주어야함.