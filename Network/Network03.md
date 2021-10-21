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
 
 
**(2) Physical Layer**
- 전기적, 기계적 케이블로 Data를 전송하는 역할만 할 뿐 어떤 Data를 전송하는지 알 수 없다. 

**(3) DataLink Layer**
- Physical Layer을 통해 송수신되는 Data의 오류와 흐름을 관리하여 안전한 Data 전달을 도와주는 역할을 한다. 

**(3) Network Layer**
- Data를 목적지까지 가장 빠르고 안전하게 전달하고 경로 설정, 주소 결정, 경로에 따라 Packet를 전달하는 역할을 한다. 

**(4) Transport Layer** 
- 사용자들이 신뢰성 있는 Data를 주고 받는 역할을 한다. 
- 오류검출, 복구, 흐름제어, 중복 검사등을 수행한다. 
- Data 전송을 위하여 PORT 번호가 사용된다. 

**(5) Session Layer** 
- 응용프로세스가 통신을 관리하기 위한 방법을 정의하는 역할을 한다.

**(6) Presentation Layer** 
- Data를 어떻게 표현할지 정하는 계층으로, 송신자에서 온 Data를 해석하기 위한 Application Layer Data의 부호화 변화, 수신자의 Data의 압축을 풀 수 있는 방식으로 된  Data 압축을 한다. 
- Data의 암호화 , 복호화 
 
**(7) Application Layer**
- 응용프로그램과 통신프로그램 간의 인터페이스를 제공한다. 

