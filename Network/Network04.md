## Network Chapter04
### Network Device 

**(1) NIC(Network Interface Card)**
- PC와 PC, PC와 Network를 연결하는 장치로, 정보 전송시 정보가 케이블을 통해 전송될 수 있도록 정보 형태를 변경한다.  

**(2) Hub**
 - **OSI Physical Layer**에서 동작하는 장비
 - Hub는 Multi Port Repeater로 한 Port에 들어온 Data를 다른 Port로 뿌려주는 역할을 하는 장비다.
 - Hub는 내부 연결통로를 공유하는 방식이다. 
 - Ethernet Hub 
    - 10Mphs Hub 
    - 100Mphs Hub  
 - Token Ring Hub
 - Dummy Hub 
   - Network에 흐르는 모든 Data를 단순히 연결하는 기능만 한다. 
   
 - Switching Hub  
   - Network상 흐르는 Data의 유무 및 흐름을 제어하면서 각각의 노드가 Hub의 최대 대역폭을 사용할 수 있게 하는 지능형 Hub로 최근의 사용하는 Hub는 모든 여기에 해당한다.  

**(3) Switch**
 - **OSI DataLink Layer**에서 동작하는 장비
 - Switch는 내부에 Memory를 가지고 있어서 각 Port에 연결되어 있는 PC들의 MAC Address가 여기에 기록되어 있고, PC A가 D로 신호를 보내면 그 신호는 D로만 전달되고 다른 PC에는 신호를 보내지 않는다. 즉 송신지와 수신지를 구분해 해당 목적지로만 신호를 전달한다. 
 - Switch는 Port별로 상대 Port로 향하는 독립적인 통로를 가지고 있다.  

**(4) Router**
 - **OSI Physical Layer**에서 동작하는 장비 
 - Network상 특정 출발지에서 특정 도착지 까지 여러 갈래의 길이 있는데 이러한 길을 찾아내고, Internet 회선을 여러 대가 사용 가능 하도록 나눠주는 역할을 한다. 

**(5) Repeater**
 - **OSI Physical Layer**에서 동작하는 장비
 - 근거리 통신망을 구성하는 Segement를 확장, 서로 연결해 주는 장비다. 
 - 신호를 수신하여 신호를 증폭시켜서 다음 구간으로 재전송하는 장치를 의미하며, 전자기장의 확산, 케이블의 손실로 인한 신호 감쇠를 보상해주기 때문에 Repeater를 사용하면 먼거리까지 Data 전달이 가능하다.  
 
**(6) Gateway**
 - **OSI Transport Layer**에서 동작하는 장비 
 - PC Network에서 서로 다른 통신망, Protocol을 사용하는 Network간의 통신을 가능하게 하는 장치이다.
 - Session, Presentation, Application Layer등을 연결하여 Data, Address, Protocol등의 변환을 수행한다. 
 
