## Numpy Chapter01
### Numpy
**(1) Numpy** 
- 행렬 연산이나 대규모 다차원의 배열을 편리하게 처리할 수 있도록 지원하는 Python library이다. 
- Numpy는 데이터 구조외에도 수치계산을 위해 효율적으로 구현된 기능을 제공한다. 

**(2) Numpy 특징** 
- N차원의 배열 객체 
- 기본적으로 array 단위로 데이터를 관리한다. 
- 큰 규모의 데이터 연산을 빠르게 수행한다. (반복문 없이 배열에 대한 처리 지원)
- 정교한 브로드캐스팅을 지원한다. 

```Python 
   import numpy as np 
```

**(3) Numpy의 차원** 
- Scalar : 하나의 데이터 값으로만 존재하는 것 
- Vector : 숫자들의 배열 (1D array) 
- Matrix : 숫자들의 2D array (rows : 행, Column : 열 )
- Tensor : 2D array 이상의 배열 
```Python
   arr_vector = np.array([1, 2, 3,])
 

```



참조   
  > [제주 하간디 이신 데이터들 Python으로 몬딱 분석해불게](https://ridibooks.com/books/2773000032?_s=search&_q=%EC%A0%9C%EC%A3%BC+%EB%8D%B0%EC%9D%B4%ED%84%B0+%EB%B6%84%EC%84%9D&_rdt_sid=search&_rdt_idx=0)  
