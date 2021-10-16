## Chapter01 C#  

### (1) C# LINQ
 - LINQ는 Language INtegrated Query의 약자로 C#3.0에 소개된 기능이다. 
 - LINQ는 간단한 수식(Expression)을 사용하여 Datasource 혹은 Collection으로 부터 Data 질의 기능에 사용된다. 
 - 어떤 Data를 대상으로 하는가에 따라 여러 종류로 나눌 수 있다. 
   - .NET Object를 대상으로 하는 LINQ to Objects
   - XML을 대상으로 하는 LINQ to XML 
   - SQL DB를 대상으로 하는 LINQ to SQL
 - Data 질의란 무엇인가? 
   - From   : 어떤 데이터 집합에서 찾을 것인가? 
   - Where  : 어떤 값의 데이터를 찾을 것인가? 
   - Select : 어떤 항목을 찾을 것인가?          

### (2) LINQ FROM 
 - 모든 LINQ Query Expression은 from절로 시작된다. 
 - QUERY의 대상이 될 Data Source와 Data Source안에 들어있는 각 요소 Data를 나타낸는 Range Variable를 FROM에서 지정해야한다. 
 - FROM절의 Data Source은 아무 형식이나 사용할 수 없고 IEnumerable<T> Interface를 상속하는 형식이어야 하는데 Collections Object들은 IEnumerable<T>를 상속하기 때문에 이들은 모두 FROM절에서  Data Source로 사용할 수 있다. 
 - Range Variable는 Query Variable라고도 하는데, Foreach문의 반복 변수로 생각하면 이해하기 쉽다. 
```CSharp
   //arrNum은 Data Source
   int [] arrNum = {1, 2, 3, 4, 5, 6, 7} ; 
   
   //n은 Range Variable 
   var result = from n in arrNum 
                where n % 2 == 0
                order by n 
                select n;
```
```CSharp
   class Program
   {
        static void Main(string[] args)
        {
            int[] arrayNum = new int[] { 1, 2, 3, 4, 5, 6, 12, 8, 99 };
            LF_Search_Multiple_Of_Three(arrayNum);
            LF_Search_Even(arrayNum);
            Console.ReadLine();
        }
        private static void LF_Search_Multiple_Of_Three(int[] p_iArray)
        {
            var numQuery = from num in p_iArray
                           where (num % 3) == 0
                           select num;
            foreach (var num in numQuery)
            {
                Console.WriteLine($"Num : {num}");
            }
        }

        private static void LF_Search_Even(int[] p_iArray)
        {
            var numQuery = from num in p_iArray
                           where (num % 2) != 0
                           select num;
            foreach (var num in numQuery)
            {
                Console.WriteLine($"Num : {num}");
            }
            Console.WriteLine();
        }
    } 
```
### (3) LINQ WHERE 
 - where절은 Filter역할을 한다. 
 - Data Source에서 뽑아낸 Range Variable가 가져야 하는 조건을 where 연산자에 인수로 입력하면 LINNQ는 해당 조건이 부합하는 Data만을 걸러낸다.

### (4) LINQ ORDERBY 
 - orderby 연산자는 Data의 정렬을 수행하는 연산자이다.  
 - ascending을 명시하면 오름차순, descending을 명시하면 내림차순으로 정렬이 된다. ascending을 생략해도 orderby 연산자는 기본적으로 오름차순으로 Data를 정렬한다.
 
### (5) LINQ SELECT   
 - select 절은 최종 결과를 추출하는 Query의 마침표 역할을 한다. 
 
  참조   
  > [이것이 C#이다](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=260230941)   
      
