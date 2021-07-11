## Chapter08 C#  
### (1) Thread Pool 과 CPU

- C#이 발표된 2000년대 초 CPU구조의 중요한 변화가 시작, CPU의 속도가 GHz에 이르면서 CPU의 한계에 이르렀고, CPU의 속도를 개선시키는 대신에 CPU의 Core를 증가시키는 쪽으로 CPU의 개발 방법을 선회했다. CPU Single Core의 경우 속도가 높은 버전으로 CPU를 업그레이드 하면 그에 따라 소프트웨어의 성능도 자연스럽게 좋아졌지만, CPU Multi Core의 경우는 여러 개의 Core가 동시에 작업할 수 있도록 병렬 처리 기법과 비동기 처리 기법이 필수가 되었다.
- **병렬(Parallel)처리**란 하나의 작업을 여러 작업자가 나누어서 처리한 뒤에 다시 하나의 결과물을 만드는 것을 의미하고 **비동기(Asynchronous)처리** 는 작업  A를 시작한 후 A의 결과가 나오는 동안에 B, C, D를 수행하다가 A가 작업이 끝나면 그 결과를 받아서 처리하는 방식을 의미한다.

### (2) Thread Pool

- .Net의 Thread Class 를 이용하여 Thread를 하나씩 만들어 사용하는 것이 아니라 이미 존재하는 Thread Pool에서 사용 가능한 작업 Thread를 할당받아 상용하는 방식이 존재, 이는 다수의 Thread를 계속 생성해서 사용하는 것보다 효율적이다. 시스템에 존재하는 Thread Pool에 있는 Thread를 사용하기 위한 방법은 아래와 같다.
    - Thread Pool Class
    - Asynchronous delegate
    - Task Class
    - Task <T> Class
    - BackgroundWorker

    ```csharp
    class ThreadPool
    {
        static void Main(string[] args)
        {
            ThreadPool.QueueUserWorkItem(LF_Calc);
            ThreadPool.QueueUserWorkItem(LF_Calc, 10.0);
            ThreadPool.QueueUserWorkItem(LF_Calc, 20.0);

            Task.Factory.StartNew(new Action<object>(LF_Run), null);
            Task.Factory.StartNew(new Action<object>(LF_Run), "1st");
            Task.Factory.StartNew(new Action<object>(LF_Run), "2st");
            Console.ReadLine();
        }
        static void LF_Run(object data)
        {
            Console.WriteLine($"{(data == null ? "NULL" : data)}");
        }
        static void LF_Calc(object radius)
        {
            if (radius == null)
            {
                return;
            }
            double r = (double)radius;
            double area = r * r * 3.14;
            Console.WriteLine($"R :{r} Area: {area}");
        }
    }
    ```



### (3) Thread Task

- Task Class, Task<T> Class는 .Net4.0부터 도입
- Thread Pool로 부터 Thread를 가져와서 비동기 작업을 한다.
- Task 관련 Class 들과 Parallel Class를 합쳐서 **TPL(Task Parallel Library)** 이라고 부르는데 기본적으로 다중 CPU 병렬 처리를 염두에 두고 만들었다.
- Task Class 사용을 위해서 흔히 사용 되는 방법은 Task.Factory.StartNew( )를 사용하여 실행하고자 하는 Method에 대한 Delegate를 지정하는 것이다.  즉 Task.StartNew() 는 Thread를 생성과 동시에 실행하는 방식이고, 실행하지 않고 Task객체를 만들기 위해서는 Task( ) 생성자를 사용하여 Method Delegate를 지정한다.

```csharp
class ThreadPool
{
    static void Main(string[] args)
    {
        Task.Factory.StartNew(new Action<object>(LF_Run), null);
        Task.Factory.StartNew(new Action<object>(LF_Run), "1st");
        Task.Factory.StartNew(new Action<object>(LF_Run), "2st");
        Console.ReadLine();
    }
    static void LF_Run(object data)
    {
        Console.WriteLine($"{(data == null ? "NULL" : data)}");
    }
}
```

```csharp
class ThreadTask
{
    static void Main(string[] args)
    {
        Task taskOne = new Task(new Action(LF_Run));
        Task taskTwo = new Task(() =>
        {
            Console.WriteLine("Long Query");
        });

        taskOne.Start();
        taskTwo.Start();
        
        taskOne.Wait();
        taskTwo.Wait();
        
        Console.ReadLine();
    }
   
	  static void LF_Run()
    {
        for (int i = 0; i < 100; i++)
        {
            Console.WriteLine($"taskThread : {i}");
        }

        Console.WriteLine("Long Running Method");
    }
}
```
참조   
  > [이것이 C#이다](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=260230941)   
  > [Thread Pool](https://docs.microsoft.com/ko-kr/dotnet/standard/threading/the-managed-thread-pool)   
  > [예제로 배우는 C# 프로그래밍](https://www.csharpstudy.com/Threads/threadpool.aspx)
  
