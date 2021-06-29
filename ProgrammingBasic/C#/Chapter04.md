## Chapter04 C#  
### (1) C# Thread
  **① Thread 정의**    
  - 오늘날 운영체제는 여러 프로세스를 동시에 실행할 수 있는 능력을 갖추고 있다 . 
  - Process 는 실행 파일이 실행되어 메모리에 적재된 인스턴스이다.    
  - word.exe가 실행파일이라면 이 실행 파일에 담겨있는 데이터와 코드가 메모리에 적재 되어서 동작하는 것이 Process이다. 
  - Process는 반드시 하나 이상의 Thread로 구성되는데, Thread는 운영체제가 CPU 시간을 할당하는 기본 단위 이다.   

  **② Multi Thread의 장점**    
  - 사용자 대화형 프로그램에서 Multi Thread를 이용하면 응답성을 높일 수 있다.
  - Multi Process 방식에 비해서 Milti Thread 방식이 자원의 공유가 쉽다.
  - Process를 띄우기 위해서는 메모리와 자원을 할당하는 작업 (CPU 사용 시간)등의 비용이 비싼편 이지만 Thread를 띄울 때에는 이미 Process에 할당된 메모리와 자원을 그대로 사용하므로 메모리와 자원을 할당하는 비용을 지불하지 않아도 된다.

  **③ Multi Thread의 단점** 
  - Multi Thread 구조의 Sofrware는 구현하기가 까다롭고, 테스트 역시 쉽지 않다.    
  - Multi Process 기반의 Sofrware는 여러 개의 자식 Process 중 하나에 문제가 생기면 자식 Process 하나가 죽는 것 이상으로 영향이 확산되지 않지만, Multi Thread 기반의 Software에서는 자식 Thread 중 하나에 문제가 생기면 전체 Process에 영향을 미친다.
  - Thread를 너무 많이 사용하면 성능이 저하된다. Thread가 CPU를 사용하기 위해서는 작업간 전환(Context Switching)을 해야하는데 이 작업간의 전환이 적지 않은 비용을 소모한다.


### (2) C# Thread의 생성과 종료 
 - Thread Instance를 생성한다. 생성자의 인수로 Thread가 실행할 Method를 넘긴다.   
 - Thread.Start( ) Method를 호출하여 Thread를 시작한다.   
 - Thread.Join( ) Method를 호출하면 Thread가 완전히 정지할 때 까지 대기하고, Join( ) Method 가 반환되고 나면 프로그램의 흐름은 Main Thread로 합쳐진다. 
```C#
namespace Thread01
{
    class Program
    {
        static void DoSomething()
        {
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"DoSomething : {i}");
                Thread.Sleep(10);
            }
        }
        static void Main(string[] args)
        {
            Thread th01 = new Thread(new ThreadStart(DoSomething)); //Ready
            Console.WriteLine("Start Thread");
            th01.Start(); //Start
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"Main : {i}");
                Thread.Sleep(10);
            }
            Console.WriteLine("Wating until thread stops");
            th01.Join(); //
            Console.WriteLine("Finished");
            Console.ReadLine();
        }
    }
}
```

### (3) C# Thread의 임의 종료 
 - 사용자가 작업관리자 등을 이용해서 Process를 임의로 종료시키는 것은 가능하지만, Process안에서 동작하는 Thread는 그렇게 종료시킬 수 없다.   
 - 실행 중인 있는 Thread를 종료시키려면 Abort( ) Method를 호출해야 한다. 
 - Abort( ) Method 호출한다고 Thread가 즉시 종료되지 않는다. Thread 객체에 Abort( ) Method를 호출하면 CLR은 해당 Thread가 실행 중이던 코드에 ThredAbortException을 발생시킨다.
   이 예외를 catch하는 코드가 있으면 이 예외를 처리한 다음 finally 블록까지 실행한 후에 해당 Thread는 완전히 종료되기 때문에 Abort() Method를 호출할 때는 이 처리 시간을 
   염두에 두어야 한다. 
 - Multi Thread의 환경에서 Abort( ) Method를 사용하지 않는 것이 좋다. 한 Thread가 동기화를 위해 어떤 자원을 독점하고 난 후에 그 자원을 해제하지 못한 채 Abort( ) Method를 호출당해 임의로 종료되면 그 자원에 접근하고자 하는 다른 Thread는 움직일 수 없는 상태가 된다. 

```C#
namespace Thread01
{
    class SideTask
    {
        int _iCount;
        public SideTask(int p_iCount)
        {
            this._iCount = p_iCount;
        }
        public void KeepAlive()
        {
            try
            {
                while (_iCount > 0)
                {
                    Console.WriteLine($"{_iCount--} left");
                    Thread.Sleep(10);
                }
                Console.WriteLine("_iCount : 0");
            }
            catch (ThreadAbortException ex )
            {
                Console.WriteLine(ex);
                Thread.ResetAbort();
            }
            finally
            {
                Console.WriteLine("Clearing resouece");
            }
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            //Thread th01 = new Thread(() => DoThread(3));
            //th01.Start();    
            SideTask task = new SideTask(100);
            Thread th01 = new Thread(new ThreadStart(task.KeepAlive));
            th01.IsBackground = false;
            Console.WriteLine("Starting thread");
            th01.Start();
            Thread.Sleep(100);
            Console.WriteLine("Aborting thread");
            th01.Abort();
            Console.WriteLine("Wating utill thread stops");
            th01.Join();
            Console.WriteLine("Finished");
            Console.ReadLine();
                
        }
        static void DoThread(int p_index)
        {
            Console.WriteLine($"start {p_index} a DoThread");
            for (int i = 0; i < 100; i++)
            {
                Console.WriteLine($"DoThread {p_index} : {i}");
            }
            Console.WriteLine($"DoThread {p_index} is terminated ");
        }
    }
}
```


  참조   
  > [Microsoft Thread](https://docs.microsoft.com/ko-kr/dotnet/api/system.threading.thread?view=net-5.0)   
  > [이것이 C#이다](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=260230941)           
