

# 설계주제

사물인터넷 표준 프로토콜 CoAP에서의 보안 프로토콜 Tiny-DTLS 적용

# 키워드

사물인터넷,  보안,  무선  센서  네트워크,  CoAP,   DTLS,  TinyDTLS,   OpenMote-
CC2538, OpenBattery, OpenBase, Raspberry Pi, Ultrasonic sensor


# problem statement

1)   제한된 네트워크에서 사용하는 표준 프로토콜인 CoAP은 보안에   취약하
다.

2) CoAP은 transport layer에서 UDP를 사용하므로 보안을 위하여 DTLS 프 로토콜을 고려할 수 있으나 IoT 통신의 제한적인 리소스 때문에 실질적 구현이 어렵다.

# 설계결과물
1)   센서로부터 센서 값을 받아 올 수 있는 라즈베리파이   환경
2) CoAP + tinydtls 통신을 simulation 할 수 있는 서버와 클라이언트 프로 그램
3)   Client측에서 결과를 확인할 수 있는 JAVA  기반  API
4)	CoAP + TinyDTLS 코드가 올라간 OpenMote-CC2538
5)	라즈베리파이에 XBee dongle을 통해 연결한 Slip-radio  OpenMote

# 구현에 사용된 개발도구

## Hardware

1) OpenMote-CC2538 client side: 라즈베리파이와 센서쪽 openmote과의 무선통신을 위하여 slip-radio code를 openmote에 fusing한 후 XBee Dongle을 통해 라즈베리파이와 연결한 다. Slip-radio를 통해 라즈베리파이가 라우터로 동작할 수 있게 된다. 본 프로젝트에서는 channel를 25로 설정하였으며, MAC 프로토콜은 nullmac driver, RDC 프로토콜을 contikimac driver를 사용하였다.

2) OpenMote-CC2538 server side: 통신모듈에서 서버쪽 역할을 한다. 센서로부터 정보를 받 아들여 클라이언트를 통해 다른 서버 (센서)에게 정보를 전달한다.

3) OpenBase: OpenMote에서 실행하는 프로그램에 대한 디버깅환경을 제공한다.

4) Open Battery: OpenMote에 Power를 공급하고 내장되어 있는 센서 중 하나인 SHT21 온/ 습도 센서를 resource로 사용한다.

5) Raspberry Pi 2 B+: 기본적으로 통신 모듈에서 Client역할을 한다. 센서 쪽의 정보를 서로 주고 받도록 하는 중간다리 역할을 한다

6) JLink Debugger: OpenMote에 소스코드를 크로스-컴파일할 때 사용한다.

7) XBee Explorer Dongle: 라즈베리파이에 센서 쪽과 ZigBee 통신환경을 제공하기 위해 ZigBee 모듈을 부착하고 ZigBee 모듈 위에 OpenMote를 부착한다.

8) SmartRF06 Evaluation board: OpenMote의 메모리를 flash할 때 사용한다.

## Software

1) cetic/6lbr: 라즈베리파이를 IPv6라우터로 동작 가능하게 해주는 프로그램이다.

2) CoAP – libcoap : Open Source로 공개된 CoAP의 c라이브러리인 libcoap을 라즈베리파이의 App Layer에 위치시킨다.

3) TinyDTLS: eclipse/kapua/tinydtls: Dtls를 CoAP 프로토콜에 최적화 되도록 수정한 TinyDTLS 를 libcoap사이의 API쪽 코드수정을 통해 결합한다.

4) wheezy: 라즈베리파이에 설치한 OS이다.

5) SEGGER/JLinkGDBServer: OpenMote에 소스코드를 크로스-컴파일할 때 사용한다. 

6) Flash programmer 2: OpenMote의 메모리를 flash할 때 사용한다.

7) putty: 라즈베리파이 terminal 원격조정 프로그램이다. 학교 안 어디서든지 로컬네트워크 망에 연결되었을 때 라즈베리파이를 원격으로 조정하기 위하여 사용하였다.

8) xrdp: 라즈베리파이 GUI 원격조정 프로그램이다. 학교 안 어디서든지 로컬네트워크망에 연결되었을 때 라즈베리파이를 원격으로 조정하기 위하여 사용하였다.(특별히 GUI적 요소 가 필요한 경우)

9) wireshark: 통신 패킷을 캡쳐하는 프로그램이다. 개발한 CoAP + TinyDTLS 코드가 실행될 때 적절한 Handshake이후에 CoAP메시지를 잘 암호화하는지 테스트하기 위하여 wireshark를 사용하였다.

10) eclipse: 자바 GUI 프로그램에 대하여 그 코드에 대한 작업과 결과 테스트를 위하여 자바의 개발 툴인 eclipse를 사용하였다.

11) californium-scandium: californium은 CoAP 프로토콜과 그와 관련된 여러 라이브러리를 java로 구현한 프로젝트이다. californium의 subproject중 하나인 scandium은 DTLS1.2가 구현 되어 CoAP를 암호화 해주는 역할을 한다. 본 프로젝트에서 구현한 CoAP + TinyDTLS 코드가 표준에 맞게 잘 구현 되었는지 판단하기 위하여 일반 상용화된 라이브러리인 californium-scandium의 코드를 이용하여 테스트하였다. 또한, 서버인 OpenMote와 통신하는 client program으로 사용하였다.


# 팀원으로서의 역할

- Centos 설치하여 개발환경 구축 라즈베리파이에 6lbr 환경 설정을 하였다.

- OpenMote, OpenBattery, OpenBase 세팅
 
- JLink Debbuger, JLink GDB Server 설치 및 구동
 
- SmartRF06 Evaluation Board를 사용한 Flash programmer 2 사용


# 구현 환경 그림

![](http://i.imgur.com/veUxhZi.png)

(1) 라즈베리파이 위에 운영체제인 RASPBIAN을 설치하고 6LoWPAN Border Router 로 동작하게 하기 위하여 Slip-radio를 퓨징한 OpenMote를 XBee dongle을 통해 라즈베 리파이와 연결시킨다. 

(2) Server로는 OpenMote에 CoAP과 TinyDTLS 코드를 퓨징한 후, 배터 리에 연결시켜 사용한다. Client로는 Californium/Scandium에서 제공하는 client program 을 이용한다. 

(3) 6lbr로 동작하는 라즈베리파이는 aaaa:: 네트워크를 통하여 server와 CoAP 통신을 할 수 있다. 6lbr은 자신의 네트워크 영역에 있는 모든 노드를 인식하여, 6lbr sensor page에 나타낸다.

(4) 통신순서는 먼저, client program에서 server인 OpenMote로 resource를 요청한다. [Figure 4.1]에 나타난 것과 같이 CoAP부터 하위 계층으로 encapsulation을 하여 암호화 된 메시지를 생성한다. 그리고 aaaa:: 네트워크로 패킷을 전송한다. Server는 패킷을 수신 한 후 decapsulation하여 복호화 된 메시지를 읽고, 요구한 resource를 반환한다.


# 참고논문 

-	RFC 7252 – The Constrained Application Protocol, Z.Shelby, K.Hartke, C.Bormann, IETF, June 2014.

-	RFC 6347 – Datagram Transport Layer Security Version 1.2, E.Rescorla, N.Modadugu, IETF, January 2012.

-	draft-ietf-core-block-17 – Block-wise transfers in CoAP, C.Bormann, Z.Shelby, CoRE Working Group, March 2015.

-	draft-ietf-core-observe-16 – Observing Resources in CoAP, K.Hartke, CoRE Working Group, December 2014.

-	IETF CoAP 기반 센서 접속 프로토콜 기술 동향, 고석갑, 박일균, 손승철, 이병탁, 한국 전자통신연구원, 2013.

-	IoT in Five days, Antonio Linan Colina, Alvaro Vives, Marco Zennaro, Antoine Bagula, Ermanno Pietrosemoli, ICTP, March 2015.

-	Lightweight DTLS implementation in CoAP-based Internet of Things, Vishwas Lakkundi, Keval Singh, ADCOM, September 2014.

-	CC2538 Powerful Wireless Microcontroller System-On-Chip for 2.4-GHz IEEE 802.15.4, 6LoWPAN, and ZigBee Applications, Texas Instruments, April 2015.

-	How to port openwsn - prof. jong won Lee, HGU, December 2015. 

# 참고 웹사이트

-	Raspberry Pi OS https://www.raspberrypi.org/downloads/ 

-	Scandium https://github.com/eclipse/californium.scandium 

-	Californium https://github.com/eclipse/californium

-	Libcoap https://sourceforge.net/projects/libcoap/ 

-	6lbr source code https://github.com/cetic/6lbr

-	6lbr 설치 방법 및 모드 설정과 사용 방법 https://github.com/cetic/6lbr/wiki/ 

-	6lbr 설치 방법 http://processors.wiki.ti.com/index.php/Cc26xx_sw_examples

-	tinydtls source code in 6lbr https://github.com/cetic/tinydtls

-	tinydtls source code https://sourceforge.net/projects/tinydtls/

-   openmote build and putty configuration http://www.openmote.com/blog/getting-started-with-contiki-and-openmote.html

-   CoAP과 TinyDTLS build http://sunmaysky.blogspot.kr/2015/11/how-to-build-dtls-example-for.html


# 동영상 링크

[http://developest.tistory.com/4](http://developest.tistory.com/4)

