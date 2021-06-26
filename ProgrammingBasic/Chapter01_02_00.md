## Chapter04 C#  
### (1) C# Thread State 
  **① Unstarted**    
  - Thread 객체를 생성한 후 Thread.Start( ) 가 호출되기 전의 상태이다.

  **② Running** 
  - Thread 시작하여 동작중인 상태를 나타낸다. Unstarted 상태의 Thread.Start( )를 통해서 만들수 있다. 

  **③ Suspended** 
  - Thread의 일시 중단 상태를 나타낸다. Thread.Suspend( ) 를 통해서 만들 수 있으며 Suspended 상태의 Thread.Resume( ) 를 통해 다시 Running 상태로 만들 수 있다. 

  **④ WaitSleepJoin**
  - Thread가 Block된 상태를 나난탠다. Thread에 대해 Moniter.Enter( ), Thread.Sleep( ), Thread.Join( ) 을 호출하면 이 상태가 된다 

  **⑤ Aborted** 
  - Thread가 취소된 상태를 나타낸다. Thread.Abort( )를 호출하면 이 상태가 되는데, Aborted 상태가 된 Thread는 다시 Stopped 상태로 전환되어 완전히 중지 된다.

  **⑥ Stopped** 
  - 중지된 Thread의 상태를 나타낸다. Thread.Abort( )를 호출하거나 Thread가 실행 중의 Methd가 종료 되면 이 상태가 된다.

  **⑦ Background** 
  - Thread가 Backgroung로 동작하고 있음을 나타낸다. Foreground Thread는 하나라도 실행되고 있는 한 Procsss가 종료되지 않지만 Background Thread는 여러 개가 실행되고 있어도 Process에 영향을 미치지 않는다. 하지만 Process가 종료되면 Background Thread도 모두 종료된다. 
  - Thread.IsBackground 속성에 true 값을 입력함으로 Thread를 이상태로 만들 수 있다.

### (2) C# Thread State Flags
 - Thread 객체의 ThreadState 필드를 통해 상태를 확인할 때에는 반드시 비트 연산을 이용한다. 
```C#
namespace Thread01_05
{
    class Program
    {
        static void Main(string[] args)
        {
            PrintThreadState(ThreadState.Running);
            PrintThreadState(ThreadState.StopRequested);
            PrintThreadState(ThreadState.Background);
            PrintThreadState(ThreadState.Unstarted);
            PrintThreadState(ThreadState.Stopped);
            PrintThreadState(ThreadState.StopRequested);
            PrintThreadState(ThreadState.WaitSleepJoin);
            PrintThreadState(ThreadState.Suspended);
            PrintThreadState(ThreadState.Aborted);
            PrintThreadState(ThreadState.AbortRequested);
            PrintThreadState(ThreadState.Aborted | ThreadState.Stopped);
            
            Running          : 0
            StopRequested    : 1
            Background       : 4
            Unstarted        : 8
            Stopped          : 16
            WaitSleepJoin    : 32
            Suspended        : 64
            Aborted          : 256
            AbortRequested   : 128
            Stopped, Aborted : 272
        }
    }
}
```
### (3) C# Thread Running and IsAlive 
  **① ThreadState.Running**
  -  Thread.Start( ) 호출 후 bool형 bThreadRunning에는 true 값을 출력 한다. 
  -  Thread.Abort( ) 호출 후 bool형 bAbortedThreadRunning에는 false 값을 출력 한다.   
  -  Thread.Join( ) 호출 후 bool형 bJoinThreadRunning에는 false 값을 출력 한다.   
  
  **② Thread.IsAlive**
  -  Thread.Start( ) 호출 후 bool형 bThreadAlive에는 true 값을 출력 한다. 
  -  Thread.Abort( ) 호출 후 bool형 bAbortedThreadAlive에는 true 값을 출력 한다.   
  -  Thread.Join( ) 호출 후 bool형 bJoinThreadAlive에는 false 값을 출력 한다.   
  
```C#
namespace Thread01_06
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                Thread th01 = new Thread(LF_ThreadFunction);
                th01.Start();

                //using Running
                bool bThreadRunning = th01.ThreadState == ThreadState.Running;

                //using IsAlive    
                bool bThreadAlive = th01.IsAlive;

                Console.WriteLine($"Started ThreadState.Running : {bThreadRunning}");
                Console.WriteLine($"Started IsAlive : {bThreadAlive}");

                th01.Abort();

                //using Running
                bool bAbortedThreadRunning = th01.ThreadState == ThreadState.Running;

                //using IsAlive    
                bool bAbortedThreadAlive = th01.IsAlive;

                Console.WriteLine($"Aborted IsAlive : {bAbortedThreadAlive}");
                Console.WriteLine($"Aborted ThreadState.Running : {bAbortedThreadRunning}");
                
                th01.Join();
                
                //using Running
                bool bJoinThreadRunning = th01.ThreadState == ThreadState.Running;

                //using IsAlive    
                bool bJoinThreadAlive = th01.IsAlive;
                Console.WriteLine($"Join IsAlive : {bJoinThreadAlive}");
                Console.WriteLine($"Join ThreadState.Running : {bJoinThreadRunning}");
            }
            catch (ThreadAbortException ex)
            {
                Console.WriteLine(ex.StackTrace);
            }
        }

       private static void LF_ThreadFunction(object p_object)
       {
            Console.WriteLine($"Test : {p_object}");
       }
    }
}
```

  참조   
  > [이것이 C#이다](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=260230941)   
      
