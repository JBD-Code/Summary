## Network Chapter05
### Network Switch 

**(1) Switch**
  - Hub의 확장된 개념으로 기본 기능은 Hub와 동일하지만, Packet의 충돌이 일어나지 않도록 Packet의 목적지로 지정할 Port로 직접 전송한다. 

 > **Switching**   
  > Switch에서 Packet의 목적지 주소를 기준으로 보내는 곳과 받는 곳을 계산하여 해당 Port로 1:1로 연결하는 것을 Switching이라고 한다. 
  > Switching은 정보 전달의 수단과 회선의 효율적 운용을 위해 I/O 상태를 감시하며 전송로에 장애 발생시에 현재 상태에서 예비 상태로 전환한다.
 
 - Switch의 특징 
    - Packet을 보내는 노드와 받는 노드를 1:1로 연결해주기 때문에 충돌이 발생하지 않고 빠른 속도로 전송이 가능하다. 
    - 두 개의 노드가 통신을 하는 동안에 다른 노드들도 서로 간의 통신이 가능하며 Ethernet에서 높은 효율을 갖는다. 
    - 노드의 수가 증가해도 속도의 저하가 일어나지 않으며, Packet의 감청이 어려운 구조이므로 보안성이 높다.  
 
 - Switch의 장점 
    - 완전한 2중화와 Fault-Tolerant  구성이 가능하며 대역폭 비용이 낮아진다. 
    - Traffic 제어가 상대적으로 높으며, Port당 속도가 일정하게 보장된다. 
    - 여러 노드에서 동시 통신할 때 속도 저하가 없고, 성능이 보장된다. 
    - 전이중 통신 모드로 Network상의 불필요한 Packet의 흐름을 막으며, 충돌이 발생하지 않아 빠른 속도로 전송이 가능하다. 
    - 각 DTE는 Switch는 몰라도 Data전송에는 상관없으며 많은 부가 기능이 있다.    

> **DTE**   
  > Data Terminal Equopment로 Data의 단말 장치를 의미한다.(PC, Router) 

- Switch의 구분 
  - 어떤 주소를 가지고 Switching 하는 가에 따라서 L2, L3, L4 Switch로 구분된다. 
  - L2 Switch : MAC Address 
  - L3 Switch : Protocol Address 
  - L4 Switch : Session Protocol   
 
**(2) L2 Switch** 
- L2 Switch의 특징  
  - Switch Packet가 왔을 때 그것의 목적지가 어딘지를 보고 그 목적지로 보내주는 역할만 한다.
  - IP Address를 이해할 수 없으므로 Routing이 불가능하다.(Routing이란 것이 외부와 연결되므로 IP Address를 알아야 한다.)
  - L2 Switch는 가장 흔히 볼수 있는 Switch 방식이므로 다른 방식에 비해서 저렴하다. 
  - Packet의 MAC Address를 읽어 Switching을 하고 MAC의 OSI 7Layer Model의 2계층에 해당하기 때문에 L2 Switch라고 한다. 
  - Bridge는 어떤 Port에서 받은 Data를 다른 Port로 전송만 하지만, L2 Switch Hub는 여러 개의 Port중 특정 Port로만 전송한다. 

- L2 Switch의 동작원리
   - 다른 Switch 처럼 Processor, Memory, Firmware가  담겨있는 FLASH ROM으로 구성된다. 
   - 전원이 들어오면 L2 Switch는 각 Port 별로 연결되어 있는 노드의 상태를 확인한다. 
   - 각 노드의 MAC Address를 알아내서 이것을 Memory에 적재하게 되고 , Packet가 전달될 때 이 정보를 바탕으로 Switching를 하게 된다. 
   
**(3) L3 Switch **
 
**(4) L4 Switch**
 

