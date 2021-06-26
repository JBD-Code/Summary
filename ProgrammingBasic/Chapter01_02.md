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
  - Multi Process 기반의 Sofrware는 여러 개의 자식 Process 중 하나에 문제가 생기면 그 자식 Process 하나가 죽는 것 이상으로 영향이 확산되지 않지만, Multi Thread 기반의 Software에서는 자식 Thread 중 하나에 문제가 생기면 전체 Process에 영향을 미친다.
  - Thread를 너무 많이 사용하면 성능이 저하된다. Thread가 CPU를 사용하기 위해서는 작업간 전환(Context Switching)을 해야하는데 이 작업간의 전환이 적지 않은 비용을 소모한다.


### (1) C# Thread의 생성과 종료 
① Thread Instance를 생성한다. 생성자의 인수로 Thread가 실행할 Method를 넘긴다.   
② Thread.Start() Method를 호출하여 Thread를 시작한다.   
③ Thread.Join() Method를 호출하면 Thread가 완전히 정지할 때 까지 대기하고, Join() Method 가 반환되고 나면 프로그램의 흐름은 Main Thread로 합쳐진다. 
```C#
class SideTask
{
    int iCount ;

    public SideTask(int p_iCount)
    {
        iCount = p_iCount;
    }

    public void KeepAlive()
    {
        try
        {
            while (iCount > 0)
            {
                Console.WriteLine($"{iCount--} left");
                Thread.Sleep(10);
            }
            Console.WriteLine("Count : 0");
        }
        catch (ThreadAbortException exAbort)
        {
            Console.WriteLine(exAbort);
            Thread.ResetAbort();
        }
        finally 
        {
            Console.WriteLine("Clearing Resource");
        }
    }
}

class Program
{
  static void Main(string[] args)
  {
      SideTask cSideTask = new SideTask(20);
      Thread th01 = new Thread(new ThreadStart(cSideTask.KeepAlive));
      th01.IsBackground = false;

      Console.WriteLine("Starting Thread");
      th01.Start();
      Thread.Sleep(100);

      Console.WriteLine("Aborting Thread");
      th01.Abort();
      Console.WriteLine("Wating until thread Stop");
      th01.Join();

      if (th01.ThreadState == ThreadState.Aborted)
      {
          Console.WriteLine("Thread Stop");
      }
      else if (th01.ThreadState == ThreadState.Stopped)
      {
          Console.WriteLine("Thread Cancel");
      }
      Console.WriteLine("Finished");
      Console.ReadLine();
  }
}
```


  참조   
  > [Microsoft Delegate](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/delegates/)   
  > [이것이 C#이다](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=260230941)           
