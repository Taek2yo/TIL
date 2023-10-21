# 네트워크의 기본 OSI 7계층
> 네트워크 프로토콜이 통신하는 구조를 7개의 계층으로 분리하여 각 계층간 상호 작동하는 방식을 정해 놓은 것. 서로 다른 컴퓨터 기기 간에 네트워크를 형성할 수 있도록 규정한 네트워크 모델 표준안.

<div style="width:100%; text-align:center;" >
<img src='https://github.com/Taek2yo/TIL/assets/110080748/46ee54f1-a1e5-4319-aebe-229e0e95d54e'/>
<p>출처 : 해시넷</p>
</div>

## 특징
### 데이터 캡슐화
> 데이터 캡슐화는 OSI 모델에서 데이터가 각 계층을 통과할 때, 각 계층이 데이터에 정보를 추가하는 과정을 의미한다. 이 정보는 헤더와 푸터로 표현되며, 각 계층 간의 효율적인 통신과 상호 운용성을 가능하게 한다. 이 과정은 데이터가 송신자에서 수신자로 이동하는 동안 계층 간의 협력과 데이터 제어를 보장한다.

| 계층         | 이름                            | 단위(PDU)        | 예시                                                     | 프로토콜(Protocols)                                     | 디바이스(Device)     |
|--------------|---------------------------------|-------------------|----------------------------------------------------------|---------------------------------------------------------|----------------------|
| 7            | 응용 계층 (Application Layer)  | Data              | 텔넷(Telnet), 구글 크롬, 이메일, 데이터베이스 관리 | HTTP, SMTP, SSH, FTP, Telnet, DNS, modbus, SIP, AFP, APPC, MAP |                    |
| 6            | 표현 계층 (Presentation Layer) | Data              | 인코딩, 디코딩, 암호화, 복호화                       | ASCII, MPEG, JPEG, MIDI, EBCDIC, XDR, AFP, PAP          |                    |
| 5            | 세션 계층 (Session Layer)       | Data              |                                                          | NetBIOS, SAP, SDP, PIPO, SSL, TLS, NWLink, ASP, ADSP, ZIP, DLC |                    |
| 4            | 전송 계층 (Transport Layer)     | TCP-Segment, UDP-datagram | 특정 방화벽 및 프록시 서버 | TCP, UDP, SPX, SCTP, NetBEUI, RTP, ATP, NBP, AEP, OSPF  | 게이트웨이          |
| 3            | 네트워크 계층 (Network Layer)   | Packet            | 라우터                                                  | IP, IPX, IPsec, ICMP, ARP, NetBEUI, RIP, BGP, DDP, PLP | 라우터             |
| 2            | 데이터링크 계층 (Data Link Layer) | Frame             | MAC 주소, 브리지 및 스위치                           | Ethernet, Token Ring, AppleTalk, PPP, ATM, MAC, HDLC, FDDI, LLC, ALOHA | 브릿지, 스위치      |
| 1            | 물리 계층 (Physical Layer)       | Bit               | 전압, 허브, 네트워크 어댑터, 중계기 및 케이블 사양, 신호 변경(디지털,아날로그) | 10BASE-T, 100BASE-TX, ISDN, wired, wireless, RS-232, DSL, Twinax | 허브, 리피터      |

## 물리계층(Physical Layer)

* 네트워크 데이터의 물리적 전송 매체를 정의하고, 전압, 중계기, 케이블 규격, 신호 변환과 같은 물리적 특성을 관리.

## 데이터링크 계층(Data-Link Layer)

* 물리적인 네트워크를 통해 데이터를 전송하고, 주소 지정을 제공한다. 또한 오류 제어와 흐름 제어를 수행하며 브리지 및 스위치와 같은 장비에서 작동.

## 네트워크 계층(Network Layer)

* 데이터의 라우팅을 관리하며, 여러 네트워크 간에 데이터를 전달한다. 이 계층은 IP 주소 할당 및 라우팅 결정을 처리하며 데이터를 논리적으로 주소를 지정한다.

## 전송 계층(Transport Layer)

* 데이터를 안전하게 전송하고, 오류를 검사하고 복구한다. 이 계층은 데이터의 신뢰성을 제공하며, 흐름 제어, 분할 및 재조립, 오류 제어를 담당하며 특정 방화벽 및 프록시 서버에서도 작동한다.

## 세션 계층(Session Layer)

* 두 컴퓨터 간의 세션을 설정, 유지, 종료하며, 통신 세션을 동기화하고 오류 복구를 수행한다. 또한 TCP/IP 세션을 관리하고 다중화 및 복구 작업을 처리한다.

## 표현 계층(Presentation Layer)

* 데이터를 읽을 수 있는 형식으로 변환하고, 데이터의 인코딩 및 디코딩, 암호화 및 복호화 작업을 수행한다. 예를 들어, 유니코드를 ASCII로 변환하거나 데이터를 암호화하여 안전하게 사용할 수 있게 한다. 

## 응용 계층(Application Layer)

* 사용자가 네트워크 자원에 접근하는 방법을 제공하며, 사용자가 실행하는 응용 프로그램들을 이 계층에 속한다. 이 계층은 사용자와 네트워크 사이의 인터페이스를 제공하며 텔넷, 브라우저, 이메일, 데이터베이스 관리 등의 서비스를 제공한다.


## TCP/IP 4계층
> TCP/IP 모델은 인터넷 통신을 위한 프로토콜이며, ARPANET과 인터넷의 발전과 함께 사용된 주요 프로토콜이다. 이 모델은 인터넷의 기반을 형성하며 다양한 컴퓨터 간 통신을 가능하게 하며, 응용 계층, 전송 계층, 인터넷 계층, 네트워크 액세스 계층으로 구성된다.

## OSI 7계층과 TCP/IP 4계층과 공통점과 차이점

### 공통점
<div style="width:100%; text-align:center;" >
<img src='https://github.com/Taek2yo/TIL/assets/110080748/ea850a78-5e13-4af4-9128-4b1e30ba30d6'/>
<p>출처 : 해시넷</p>
</div>

### 차이점
<div style="width:100%; text-align:center;" >
<img src='https://github.com/Taek2yo/TIL/assets/110080748/3bcc6460-6b8b-4880-a5e6-f512f7bc8c77'/>
<p>출처 : 해시넷</p>
</div>


#### 출처 및 참고

http://wiki.hash.kr/index.php/OSI_7_%EA%B3%84%EC%B8%B5

https://it-mengi.tistory.com/7