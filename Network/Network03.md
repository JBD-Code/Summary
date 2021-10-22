## Network Chapter03
### OSI 7 계층 
**(1) OSI(Open System Interconnections)**
 - 통신에 관한 국제 표준 기구 ISO에서 통신이 일어나는 과정을 7단계로 나누었다.
 - 7개의 단계별로 표준화 하여 효율성을 높이기 위해서 사용한다. 
 - Data의 흐름이 한 눈에 보이고, 여러 회사의 장비를 사용해도 네트워크가 문제없이 작동한다.   
 
 |Layer|Layer NAME|DATA UNIT|PROTOCOL|DEVICE|
 |:----:|:------|:----|------|----------|
 |7|Application Layer|Data|HTTP, SMTP, FTP|
 |6|Presentation Layer|Data|JPG, MPEG, AFP, PAP|
 |5|Session Layer|Data|NET BIO, SSH|
 |4|Transport Layer|Segments|TCP, UDP|GATEWAY|
 |3|Network Layer|Packet|IP, RIP ARP, ICMP| ROUTER|
 |2|DataLink Layer| Frame|Etherent, PPP, HDLC|BRIDGE, SWITCH|
 |1|Physical Layer | Bit|RS-232, RS-449|HUB, REPEATER|
 
 - 송신 측에서 하위 계층으로 이동할 때 각 계층 Protocol에서 정의한 Header를 추가한다.
 - 수신 측에서 상위 계층으로 이동할 때 순차적으로 Header 정보를 처리하고 제거한다. 
 
**(2) Physical Layer**
- 전기적, 기계적 케이블로 Data를 전송하는 역할만 할 뿐 어떤 Data를 전송하는지 알 수 없다. 

**(3) DataLink Layer**
- Physical Layer을 통해 송수신되는 Data의 CRC 기반의 오류제어와 흐름제어를 통해서 Point to Point간 신뢰성 있는 전송을 보장, 안전한 Data 전달을 도와주는 역할을 한다. 
- **MAC Address를 가지고 통신을 하게된다**.   

**(3) Network Layer**
- Data를 목적지까지 가장 빠르고 안전하게 전달(Routing)하고 경로 설정, 주소 부여한다.
- 여러 개의 노드를 거칠 때마다 경로에 따라 Packet을 전달하는 역할을 한다.  
- Segmentation/Desegmentation, Internetworking등을 수행한다. 
- Data를 연결하는 다른 Network를 통해 전달함으로 인터넷이 가능하게 만드는 계층이다. 
 
**(4) Transport Layer** 
- 통신을 활성화하기 위한 계층이다. Port를 열어서 응용프로그램들이 전송을 할 수 있게 한다. 
- End to End의 사용자들이 신뢰성 있는 Data를 주고 받는 역할을 한다. 
- 오류검출, 복구, 흐름제어, 중복 검사등을 수행한다. 
- Data 전송을 위하여 Port 번호가 사용된다. 

**(5) Session Layer** 
- Data가 통신하기 위한 논리적인 연결을 의미하며 Session 설정, 유지, 종료 전송 중단시 복구 등의 기능을 한다. 
- Duplex(동시 송수신), Half-Duplex(반이중), Full-Duplex(전이중)방식의 통신과 함께 Check Pointing, 유후, 종료, 다시 시작등의 과정을 수행한다. 

**(6) Presentation Layer** 
- 코드 간의 번역을 담당하며, 사용자 시스템에서 Data의 형식상 차이를 다루는 부담을 Application Layer로 부터 덜어준다. 
- EBCDIC -> ASCII Encoding  
- Data의 암호화 , 복호화 
 
**(7) Application Layer**
- 응용프로그램과 통신프로그램 간의 인터페이스를 제공한다. 

