## Computer Architecture Part01 
## Chapter01 
### 1-1 조직과 구조       
- 컴퓨터 시스템을 설명하는데 있어서 컴퓨터 구조(Computer architecture)와 컴퓨터 조직(Computer organization)을 구분해야 한다. 
- 컴퓨터 구조(Computer architecture)
  - 프로그램의 논리적 수행에 직접적인 영향을 주는 시스템의 특성을 말한다. 
  - 명령어 세트, 여러가지 데이터 표현에 사용되는 비트의 수, I/O 방식 및 주소 지정 기억 장치에 대한 기술 
- 컴퓨터 구조(Computer organization)
  - 구조적 특이사항들을 구현하기 위한 연산 유닛과 상호연결되는 방식을 말한다. 
  - 하드웨어의 제어 신호, 컴퓨터와 주변기기 사이의 인터페이스 및 기억장치 제조 기술 

### 1-2 조직과 기능 
- 기능 
  - 컴퓨터가 수행할 수 있는 기본적이 기능은 다음의 네가지로 분류된다.
  - 데이터 처리(Data processing)
    - 컴퓨터는 데이터 처리를 할 수 있어야 한다. 데이터는 여러가지 방식에 의해서 표현되고 처리된다. 
  - 데이터 저장(Data storage)
    - 데이터 저장도 필수적인 기능이다. 컴퓨터는 지나나가는 데이터를 처리하지만,  그 과정을 위해서 필요한 데이터들을 내부에 일시적으로 저장 가능해야 한다.   
  - 데이터 이동(Data movement)  
    - 컴퓨터와 외부 사이에 데이터를 이동 시킬 수 있어야 한다. 데이터가 컴퓨터와 직접 연결된 장치들로부터 들어오고 나가는 것을 입출력(I/O)이라고 하며 그 장치들을 주변장치(Peripheral)이라고 한다. 또한 장거리에 위치한 원격장치들과 데이터를 주고 받는 것을 데이터 통신(Data communocation)이라고 한다.  
  - 제어 (Control)
    - 앞의 세가지 기능들에 대한 제어가 필요한다. 제어는 컴퓨터에게 명령어들(Instructions)을 제공해주는 사용자에 의해 이루어진다. 
- 조직 
  - 컴퓨터는 임의의 방법으로 외부 환경과 상호 작용하는 하나의 개체(Entity)이다. 
  - 컴퓨터 내부조직 
    - 중앙처리장치(Central Processing Unit:CPU)
      - 산술논리연산장치(Aruthmetic and Login Unit:ALU) 
      - 제어유닛(Control Unit)
      - 레지스터(Register)
      - CPU상호연결(Interconnection)
    
    - 주기억장치(Main memory)
    - 입출력장치(I/O)
    - 시스템 상호연결 

참조   
  > [컴퓨터 시스템 구조론](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=1734625289)   
   

