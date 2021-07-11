## Chapter02 C#  
### (1) C# Shallow Copy(얕은 복사)   
  ① class 선언   
  ② Instance source와 target을 생성하고 값을 할당     
  ③ 출력 
```C#
namespace ObjectCopy
{
    class ObjectCopy
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Shallow Copy");
            {
                ObjectCopy source = new ObjectCopy();
                source.iMyField1 = 10;
                source.iMyField2 = 20;

                ObjectCopy target = source;

                target.iMyField2 = 30;

                Console.WriteLine($"source.iMyField1 : {source.iMyField1} source.iMyField2 : {source.iMyField2,-1}");
                Console.WriteLine($"target.iMyField1 : {target.iMyField1} target.iMyField2 : {target.iMyField2,-1}");
                Console.ReadLine();
                //Shallow Copy
                //source.iMyField1 : 10 source.iMyField2 : 30
                //target.iMyField1 : 10 target.iMyField2 : 30
            {
        }
    }
}
```
- C#에서는 메모리에 저장되는 방식에 따라 Reference Type 과 Value Type이 있다. 
- class는 참조 형식이기 때문에 위와 같은 결과를 출력한다. 참조 형식은 Heap 영역에 객체를 할당하고 Stack에 있는 참조가 Heap영역에 할당된 메모리를 가리킨다. 
- source를 복사해서 받은 target은 Heap영역에 있는 실체 객체가 아닌, Stack에 있는 참조를 복사해서 받는다. 

### (2) C# Deep Copy(깊은 복사)  


```C#
namespace ObjectCopy
{
    class ObjectCopy
    {
        public ObjectCopy DeepCopy()
        {
            ObjectCopy newCopy = new ObjectCopy();
            newCopy.iMyField1 = this.iMyField1;
            newCopy.iMyField2 = this.iMyField2;

            return newCopy;
        }
        
        static void Main(string[] args)
        {
            Console.WriteLine("Deep Copy");
            {
                ObjectCopy source = new ObjectCopy();
                source.iMyField1 = 10;
                source.iMyField2 = 20;
                ObjectCopy target = source.DeepCopy();

                target.iMyField2 = 30;
                Console.WriteLine($"source.iMyField1 : {source.iMyField1} source.iMyField2 : {source.iMyField2}");
                Console.WriteLine($"target.iMyField1 : {target.iMyField1} target.iMyField2 : {target.iMyField2}");
                Console.ReadLine();
                //Deep Copy
                //source.iMyField1 : 10 source.iMyField2 : 20
                //target.iMyField1 : 10 target.iMyField2 : 30
            }
        }
    }
}
```
### (3) C# ICloneable.Clone( ) Method  
- System namespace에는 ICloneable이라는 Interface가 존재하는데 간략하게 설명하면 "class가 구현해야 하는 목록"이라고 할 수 있다.    
- Deep Copy 기능을 가진 class가 다른 class와 호환되도록 하고 싶다면 ICloneable을 상속하는 것이 유용하다.   
- ICloneable Interface는 Clone( ) Method 하나만 가지고 있다.    

 
  
```C#
 public class Program : ICloneable
    {
        public int iMyField1;
        public int iMyField2;

        public object Clone()
        {
            Program objectCopy = new Program();
            objectCopy.iMyField1 = this.iMyField1;
            objectCopy.iMyField2 = this.iMyField2;
            return objectCopy;
        }
        
        static void Main(string[] args)
        {
            Console.WriteLine("Shallow Copy");
            {
            
            Program source = new Program();
            source.iMyField1 = 10;
            source.iMyField2 = 20;

            Program target = source;

            target.iMyField2 = 30;

            Console.WriteLine($"source.iMyField1 : {source.iMyField1} source.iMyField2 : {source.iMyField2,-1}");
            Console.WriteLine($"target.iMyField1 : {target.iMyField1} target.iMyField2 : {target.iMyField2,-1}");
            Console.ReadLine();
            }

            Console.WriteLine("using Cloneable. Method() Deep Copy ");
            {
                Program source = new Program();
                source.iMyField1 = 10;
                source.iMyField2 = 20;
                Program target = (Program)source.Clone();

                target.iMyField2 = 40;
                Console.WriteLine($"source.iMyField1 : {source.iMyField1} source.iMyField2 : {source.iMyField2}");
                Console.WriteLine($"target.iMyField1 : {target.iMyField1} target.iMyField2 : {target.iMyField2}");
                Console.ReadLine();
                //Deep Copy
                //source.iMyField1 : 10 source.iMyField2 : 20
                //target.iMyField1 : 10 target.iMyField2 : 30

            }
        }
    }
```

  참조   
  > [이것이 C#이다](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=260230941)   
      
