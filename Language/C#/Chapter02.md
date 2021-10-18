## Chapter01 C#  

### (1) DLL(Dynamic Link Library)
- DLL은 Dynamic Link Library의 약자로 일반적으로 확장자가 DLL인 파일로 Windows에서 사용되는 공유 Library이다. 
- DLL은 '동적 링크'방식으로 이는 링크시에 실행파일엘 결합되는 것이 아닝라 프로그램 실행 시에 DLL도 함께 프로그램의 메모리 공간으로 읽어와서 호출될 주소 등을 적적하레 바뿌는 것을 말한다. 일단 읽어온 함수는 프로그램 내부함수 처럼 호출될 수 있다. 
- DLL은 실행파일과 다른 파일이므로 필요한 시점에 메모리로 읽어오고 불필요하면 메모리에서 내릴 수 있다. 
### (2) DLL의 장단점 
- 여러 프로그램에서 동시에 사용할 수 있다. 정적링크 방식은 자신이 가진 코드를 자기혼자서 사용하지만 동적 링크 방식은 하나의 DLL로 존재하여 다른 프로그램에게 라이브러리를 제공해준다. 
- 실행 파일은 DLL에 있는 함수를 Import하게 되는 것이 DLL은 실행파일에게 함수를 Export해주는 것이다. 
- 

          
  참조   
  > [이것이 C#이다](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=260230941) 
  > [MSDN DLL](https://docs.microsoft.com/ko-kr/troubleshoot/windows-client/deployment/dynamic-link-library)     
      
