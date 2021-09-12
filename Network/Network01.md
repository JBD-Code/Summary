## Network Chapter01
### Modbus
- 자동화 디바이스 간 통신을 위해 개발된 산업용 Protocol
- 다양한 현대의 네트워크에서 간단하고 안정적이며, 효율적인 통신을 위해 개발되었다.

**(1) Modbus ADU**
 - Master - Slave 구조를 따른다. 이 구조하에서는 Master는 Slave에 요청을 보내고 응답을 기다린다. 
 - Master은 정보의 흐름을 전적으로 제어할 수 있으며 Multi Drop Serial Network에 유용하다. 
 - Modbus의 Response의 요청은 여러층으로 된 데이터 세트이다. 첫번째 계층은 **A**pplication **D**ata **U**nit로 대부분의 사람들이 **ADU**를 Modbus의 유형으로 생각한다. **ADU**의 유형에는 ASCII, RTU, TCP/IP가 있다.  
 - TCP는 소프트웨어에서 Modbus의 요청과 응답을 효율적으로 처리하고, 각 요청에 대한 전용 연결과 식별자를 통해 보다 효율적인 네트워킹을 구현하는 현대식 포맷이다. RTU와 ASCII는 조금 더 오래된 시리얼 ADU 포맷으로 차이점은 RTU는 Binary 형식으로 데이터를 표현하며, ASCII는 ASCII 문자로 요청을 보낸다.

**(1) Modbus PDU**
- Modbus의 ADU안에는 Modbus의 핵심인 **P**rotocol **D**ata **U**nit 가 존재한다. 
- 각 PDU에는 Function Code와 Data가 존재한다. 
