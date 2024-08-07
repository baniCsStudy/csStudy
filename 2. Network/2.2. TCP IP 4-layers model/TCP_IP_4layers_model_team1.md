# TCP/IP 4계층과 OSI 7계층
인터넷 프로토콜 스위트 : 컴퓨터들이 서로 정보를 주고받는데 쓰이는 프로토콜의 집합. tcp/ip 4계층 혹은 OSI 7계층으로 설명함.  
다른 계층이 변경되어도 서로 영향을 받지 않는다.

## TCP/IP 4계층
- 애플리케이션 계층 (FTP / HTTP / SSH / SMTP / DNS)
- 전송계층 (TCP / UDP / QUIC)
- 인터넷 계층 (IP / ARP / ICMP)
- 링크계층 (이더넷)

## OSI 7계층
- 애플리케이션 계층
- 프레젠테이션 계층
- 세션 계층
- 전송 계층
- 네트워크 계층
- 데이터 링크 계층
- 물리 계층



### 애플리케이션 계층
FTP / HTTP / SSH / SMTP / DNS 등 응용 프로그램이 사용됨.
웹서비스, 이메일 등 서비스가 실질적으로 사용자에게 제공되는 층
> - FTP : 장치와 장치간 파일전송
> - SSH : 보안되지 않은 네트워크에서 서비스를 보호하기 위해 암호화
> - HTTP : 웹 사이트 프로토콜
> - SMTP : 전자메일 전송 프로토콜
> - DNS : 도메인 이름 - IP 주소 매핑(ip주소가 바뀌더라도 www.naver.com으로 접속이 가능)

### 전송 계층
TCP/UDP가 있음.  
송신자 - 수신자 연결하는 통신서비스 제공  
애플리케이션 계층 - 인터넷 계층사이의 중계역할
- TCP : 패킷사이 순서 보장, 수신여부 확인, '가상회선 패킷 교환방식' 사용 (연결지향 프로토콜을 사용해 신뢰성 구축)
- UDP : 패킷 순서 보장 안함, 수신여부 확인 안함, '데이터그램 패킷 교환 방식' 사용(단순히 데이터만 주고받음)
> 가상회선 패킷교환은 모든 패킷이 특정 회선을 따라 순서대로 이동  
> 데이터그램 패킷교환은 각 패킷이 독립적으로 최선의 경로로 이동

- TCP 연결  
*3-웨이 핸드셰이크 : TCP 신뢰성확보를 위해 진행
  1) 클라이언트가 자신의 ISN을 서버로 송신
  2) 서버의 ISN, 클라이언트의 ISN + 1을 클라이언트에게 송신
  3) 서버의 ISN + 1을 서버에 송신
  > ISN(Initaial Sequence Number) : 통신을 처음 연결할때 얻는 임의의 시퀀스 넘버

- TCP 연결 해제
*4-웨이 핸드셰이크
  1) 클라이언트가 FIN으로 설정된 세그먼트 발송 -> 서버응답 대기(FIN_WAIT_1)
  2) 서버가 ACK라는 승인 세그먼트 발송 -> 클라이언트는 다시 대기(FIN_WAIT_2)
  3) 서버가 FIN이라는 세그먼트 발송
  4) 클라이언트는 서버로 ACK 발송 -> 클라이언트는 TIME_WAIT상태가 됨 -> 서버는 CLOSED 상태가 됨 -> 일정시간 대기후 연결이 닫히고 양측 모두 연결해제
  > 지연 패킷이 발생하는것을 대비하고 두 장치의 연결이 닫혔는지 확인하기 위해 TIME_WAIT상태로 대기가 필요

### 인터넷 계층
장치로 부터 받은 네트워크 패킷을 IP주소로 지정된 목적지로 전송  
IP, ARP, ICMP 등이 있음.

### 링크 계층
실질적으로 데이터를 전달(전선, 광섬유, 무선 등)

### 계층간 데이터 송수신
애플리케이션 계층에서 전송계층으로 요청을 보낼떄 캡슐화가 진행됨  
수신측의 링크계층으로 부터 애플리케이션 계층까지 다시 비캡슐화를 진행함.

- 캡슐화 : 상위계층의 헤더, 데이터를 하위계층의 데이터에 포함시키고 -> 해당계층의 헤더를 삽입  
 전송계층은 전송계층의 헤더를 붙히고  
 인터넷 계층은 전송계층의 헤더를 데이터에 포함시킨뒤 인터넷 계층의 헤더를 추가로 붙힘(패킷화)
 링크계층은 다시 프레임헤더, 프레임 트레일러를 붙힘(프레임화)
- 비캡슐화 : 위 과정이 반대로 진행됨.

- PDU : 네트워크의 한 계층에서 다른 계층으로 데이터가 전달될 때의 덩어리 단위(Protocol Data Unit)




