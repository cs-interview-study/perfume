## 📝 글 소개

면접 기출에 등장하는 TCP/IP를 공부하기 위해 작성한 글이다. 나처럼 CS 지식이 거의 없는 사람도 이해할 수 있도록 최대한 쉽게 정리하려고 노력했다. 신뢰성 있는 정보를 전달하기 위해 책을 참조했고, 참고한 도서들은 하단에 적어두었다.

## 💬 시작하기 앞서

누군가에게 소포를 보내려면 어떻게 해야 할까? 아마 포장한 소포를 우체국에 들고 가서 운송장을 붙여야 할 것이다. 소포는 "올바른 운송장"이 있어야 목적지에 도착한다는 게 사회구성원들이 합의한 약속(규칙)이기 때문이다. 네트워크에서도 서로 문제없이 통신하기 위한 규칙이 있다. 이 규칙을 **프로토콜**이라 부른다. 

인터넷에는 많은 프로토콜이 있는데, 그중 핵심적인 두 가지가 **IP**와 **TCP**다. 

### 📂 패킷

> IP는 인터넷 프로토콜(Internet Protocol)의 줄임말로, 개별 패킷의 형식을 지정하고 패킷을 전송하는 방법을 정의한다. _- <1일 1로그 100일 완성 IT 지식> 300p_



벌써 어려운 말이 등장했다. 패킷이 뭘까? 패킷은 **데이터의 묶음 단위**로, **한번에 전송할 데이터의 크기**를 말한다. 컴퓨터들은 서로 데이터를 주고 받을 때 데이터를 통째로 보내지 않고 패킷 단위로 분할해서 보낸다. 큰 데이터를 그대로 보내면 그 데이터가 네트워크의 대역폭을 너무 많이 차지해서 다른 패킷의 흐름을 막을 위험이 있기 때문이다.

그럼 IP는 어떻게 개별 패킷의 형식을 지정하고 패킷을 전송하는 방법을 정의한다는 걸까? 이 질문에 대답하기 위해선 먼저 **캡슐화**라는 개념을 알아야 한다.

### 📂 캡슐화

데이터를 보내려면 데이터의 앞부분에 전송하는데 필요한 정보를 추가해야 한다. 소포를 보낼 때 운송장을 붙이는 것처럼 말이다. 이 정보를 헤더라고 하는데, 이처럼 데이터에 헤더를 붙여 보내는 걸 **캡슐화**라고 한다. 왜 이런 이름이 붙었는지는 아래 그림을 보면 알 수 있다. 

![](https://images.velog.io/images/perfumellim/post/92af2617-3dc3-4c3f-b915-6c02b89323fc/capsule-002.jpg)

IP 헤더에는 다양한 정보들이 포함된다. ID, 출발지 IP 주소, 목적지 IP 주소, 서비스 유형, 전체 패킷 길이 등등... 이처럼 데이터에 IP 헤더가 추가되어 캡슐화된 것을 IP 패킷이라고 한다. 즉 IP는 캡슐화를 통해 개별 패킷의 형식을 지정하고 패킷을 전송하는 방법을 정의한다.


자, 이제 사전 개념 정리는 끝났다. 본격적으로 TCP/ IP에 대해 알아보자.



## ✨ IP: 인터넷 프로토콜

IP는 **'신뢰성 없는' '비연결형'** 패킷 전송 서비스를 제공한다. 

### 🔹 비연결형

각 IP 패킷이 자립적이며, 다른 IP  패킷과 관계가 없음을 뜻한다. IP에는 상태를 관리하거나 기억하는 기능이 없다. 

### 🔹 신뢰성 없는

신뢰성이 없다는 말이 우리가 흔히 사용하는 의미와는 조금 거리가 있다. 여기서 신뢰성 없다는 뜻은 패킷이 잘 전송되는 것을 보장하지 않는다는 뜻이다. IP는 목적지까지 데이터를 잘 전달하기 위한 행위만 한다. 전송 속도에 대해 아무런 보장을 하지 않으며, 정보가 도착할 것이라는 약속조차 하지 않는다. 그래서 IP 데이터 전송을 'best effort'(전달만 하는 최선의 서비스) 방식이라고 한다. 

### 🔹 IP 주소

데이터를 보내려면 소포를 보낼 때와 마찬가지로 목적지 주소가 있어야 한다. 네트워크에서 각 네트워크를 식별할 수 있는 주소가 바로 IP 주소다. IP 주소의 구조에 관한 자세한 내용은 여기서 다루지 않겠다. 

### 🔸 정리

정리하자면 IP는 데이터를 주고 받을 때 주소를 지정해주고, 해당 주소까지 어떻게 데이터를 전달할지 경로를 지정하는 프로토콜이다. 이 소포가 제대로 도착하는지, 제시간에 도착하는지는 신경쓰지 않는다. 이 다음부터는 TCP의 몫이다.



## ✨ TCP: 전송 제어 프로토콜


### 🔹 전송 계층

![](https://images.velog.io/images/perfumellim/post/7a4767b7-5090-428e-91b3-033a8224848a/tcpip.png)

이미지 출처: https://hongchangsub.com/networkprotocol/

이게 뭐지? 하고 당황할 필요 없다. 인터넷 프로토콜에는 이런 식으로 계층이 있고, 각 계층은 바로 위에 있는 프로토콜에 서비스를 제공한다는 것만 이해하면 된다. 

앞서 말했듯이 IP는 신뢰성이 없다. 대신 IP보다 상위 계층에 있는 TCP, UDP 등이 신뢰성 있는 통신을 만들어낸다. 즉, 전송 계층은 **목적지에 신뢰할 수 있는 데이터를 전송하기 위해** 필요하다.

전송 계층은 크게 두 가지 역할을 한다.

> **1. 오류를 점검하는 기능**
-> 목적지까지 데이터가 제대로 도착했는지 확인한다. 오류가 발생했을 경우 데이터를 재전송하도록 요청한다.
>
**2. 전송된 데이터의 목적지가 어떤 애플리케이션인지 식별하는 기능**
-> 해당 데이터가 어떤 애플리케이션에서 사용하는 데이터인지 판단한다.


### 🔹 연결형 통신과 비연결형 통신 (TCP vs UDP)

전송 계층은 크게 두 가지로 구분할 수 있다. 

신뢰할 수 있고 정확한 데이터를 전달하는 연결형 통신과,
효율적으로 데이터를 전달하는 비연결형 통신. 

연결형 통신은 상대편과 확인해 가면서 통신하는 방식이고, 비연결형 통신은 상대편을 확인하지 않고 일방적으로 데이터를 전송하는 방식이다. 

흔히 TCP와 함께 비교되는 UDP, 즉 **사용자 데이터그램 프로토콜(User Datagram Protocol)**이 바로 비연결형 통신에 사용되는 프로토콜이다. UDP는 동영상 재생처럼 양방향 흐름이 필요하지 않은 데이터 교환에 주로 사용된다. (화면이 버벅거리는 동영상을 시청한다고 상상해보자! 신뢰성보다 효율성이 중요한 이유다.)

UDP는 몇 가지 제한된 기능만 제공함으로써 패킷을 효율적으로 전송할 용도로 쓰인다. 하지만 제한된 용도만 유용하기 때문에 우리가 '인터넷'이라고 생각하는 대부분의 서비스는 TCP를 사용한다. TCP는 사용자에게 신뢰성 있는 양방향 스트림을 제공한다. 즉 데이터를 한쪽 끝에 넣으면 반대쪽 끝에서 나오며, 전송 지연이 적고 오류발생 확률은 낮다. 마치 한쪽 끝에서 반대쪽 끝까지 직접 선으로 연결된 것처럼 작동한다.


간단히 요약하자면 이렇다.

> TCP는 신뢰성과 정확성을 우선으로 하는 연결형 통신 프로토콜이다. - <모두의 네트워크> 160p




## 📣 TCP/ IP

앞에서 정의한 TCP와 IP의 개념을 정리해보자.

IP는 개별 패킷의 형식을 지정하고 패킷을 전송하는 방법을 정의한다. TCP는 이 IP 패킷을 신뢰성 있게 데이터 스트림으로 결합하고 서비스에 연결하는 방법을 정의한다. 그리고 이 두 프로토콜을 합쳐서 **TCP/IP**라고 부른다.

## 📚 참고도서

[1일 1로그 100일 완성 IT 지식](http://www.yes24.com/Product/Goods/105803863)

[모두의 네트워크](http://www.yes24.com/Product/Goods/61794014)