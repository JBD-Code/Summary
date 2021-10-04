
## Oracle Query
### Scalar Sub Query 
**Scalar Sub Query**
- Scalar Sub Query 란 SELECT절에 오는 Sub Query로 한번에 결과를 1행씩 반환한다. 
- Scalar Sub Query 는 Query의 결과가 없을 경우에 NULL 값을 반환한다. 그래서 Salar Sub Query는 OUTER JOIN과 유사하다.
- JOIN등의 방법은 출력하고자 하는 Data의 양이 적을 경우 Scalar Sub Query보다 속도가 느리다. 그렇끼 때문에 주로 출력하고자 하는 Data의 양이 적을 경우에는 Scalar Sub Query를 많이 사용한다.  


**Scalar Sub Query의 동작 순서**
- Main Query를 수행한  후 Scalar Sub Query에 필요한 값을 제공한다. 
- Scalar Sub Query를 수행하기 위해 필요한 Data가 들어있는 블록을 메모리로 로딩한다. 
- Main Query에서 주어진 조건을 가지고 필요한 값을 찾는다. 그리고 이 결과를 입력값과 출력값으로 메모리 내 Query Execution Cache라는 곳에 저장한다. (입력값은 Main Query에 저장된 값, Scalar Sub Query 수행 후 나온 결과값)
- 다음 조건이 Main Query에서 Scalar Sub Query로 들어오면 해시 함수를 통해 해당값이 캐시에 존재하는지 찾고, 있으면 즉시 결과값을 출력하고 없으면 다시 블록을 엑세스해서 해당 값을 찾은 후 다시 메모리에 캐시해 둔다. 
- Scalar Sub Query가 빠른 이유는 Data가 메모리에 만들어져 있는 값을 찾아 오기 때문이다. 만약 모든 Data가 메모리에 없거나, 또는 Data의 양이 많을 경우는 Query Execution Cache에서 해당 Data를 찾는 시간이 더 걸리기 때문에 JOIN보다 속도가 더 걸리게 된다. 
 
