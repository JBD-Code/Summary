## Network Chapter01
### Modbus
- 자동화 디바이스 간 통신을 위해 개발된 산업용 Protocol이다. 
- 다양한 현대의 네트워크에서 간단하고 안정적이며, 효율적인 통신을 위해 개발되었다.
- Master(Client) - Slave(Server)구조를 따른다. 이 구조하에서는 Master는 Slave에 요청을 보내고 응답을 기다린다. 
- Master은 정보의 흐름을 전적으로 제어할 수 있으며 Multi Drop Serial Network에 유용하다. 
- Master에는 주로 산업용 HIIMI 기기, PC가 위치하고 Slave에는 TCPPORT, PLC(Programmable Logic Controller)가 위치한다.     

**(1) Modbus ADU**
 - Modbus의 Response의 요청은 여러층으로 된 데이터 세트이다. 첫번째 계층은 **A**pplication **D**ata **U**nit로 대부분의 사람들이 **ADU**를 Modbus의 유형으로 생각한다. **ADU**의 유형에는 ASCII, RTU, TCP/IP가 있다.  
 - TCP는 소프트웨어에서 Modbus의 요청과 응답을 효율적으로 처리하고, 각 요청에 대한 전용 연결과 식별자를 통해 보다 효율적인 네트워킹을 구현하는 현대식 포맷이다. RTU와 ASCII는 조금 더 오래된 시리얼 ADU 포맷으로 차이점은 RTU는 Binary 형식으로 데이터를 표현하며, ASCII는 ASCII 문자로 요청을 보낸다.
   
**(2) Modbus Frame**
- Modbus의 ADU안에는 Modbus의 핵심인 **P**rotocol **D**ata **U**nit 가 존재한다. 

- 각 PDU에는 Function Code와 Data가 존재한다. 범용 Modbus(RTU, ACSII)와 Mobbus TCP의 Frame 구조는 전체적으로 비슷하지만 다른 부분이 존재한다.  
- **Mobbus RTU, ASCII Frame 구조**  
   - Addition address 
  - Functuion code 
  - Data 
  - Error check  
   
- **Modbus TCP Frame 구조**
  - MBAP Header 
    - Transaction ID
    - Protocol ID 
    - Length 
    - Unit ID
  - Fucntion Code
  - Data   
 
**(3) MBAP Header**
 - Transaction ID : Master이 최초 0x0000값 부터 통신시작 시 1씩 증가시키며 Slave는 그 값을 그대로 복사해서 사용한다. 응답에 대해 한쌍으로 작업이 이루어졌는지를 확인하는 부분이다. 
 - Protocol ID : Protocol의 ID를 나타내며 Mobbus-TCP는 0x0000 의 고정값을 사용한다. 
 - Length : Length 필드위치에서 Frame 마지막까지의 길이를 나타낸다. 
 - Unit ID : TCP/IP가 아닌 통신선로의 연결되어 있는 Slave를 구분하는 정보이다. TCPport는 0x01로 고정이다. 

**(4) Function Code**
- Function Code는 Modbus에서 제공하는 명령어 집합 Code이다. Function Code를 이용하여 Slace memory(Coil, Register)에 값을 읽어오거나 쓸 수 있는 Service이다. 
- 실제적으로 0~127사이의 값을 사용하고 있지만, TCPport에서는 1, 2, 4, 5, 6, 15, 16값을 지원한다.
