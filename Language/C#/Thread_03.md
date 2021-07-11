## Chapter06 C#  

### (1) Thread Synchronization     

- 애플리케이션을 구성하는 각 Thread는 여러가지 자원을 공유하는 경우가 많다.  
- 하나의 Thread가 어떤 자원을 사용하고 있는 중에 다른 Thread가 그 자원을 멋대로 사용하게 되는 경우가 있는데 이런 상황에서 Thread가 질서 정연하게 자원을 사용할 수 있도록 순서를 가지고 사용하게 하는 것을 **Synchronization**라고 한다.
- Thread Synchronization에서 가장 중요한 것은 자원을 한 번에 하나의 Thread가 사용하도록 보장하는 것이다.
- .Net에서는 Thread 동기화를 지원하기 위해서 **lock keywod**와 **Moniter class**를 제공한다.

### (2) lock Keyword 

- lock keyword로 감싸주면 Critical Section으로 변경이 가능하다. Critical Section이란 한번에 하나의 Thread만 사용할 수 있는 코드 영역을 의미한다. 
- Thread Synchronization를 설계할 때에는 Critical Section을 반드시 필요한 곳에만 사용하도록 하는 것이 중요하다.   

```C#
    class Counter
    {
        const int ILOOP_COUNT = 100;
        readonly object thisLock;
        private int _iCount;

        public int Get_Count
        {
            get { return _iCount; }
        }

        public Counter()
        {
            thisLock = new object();
            _iCount = 0;
        }
        
        public void LF_Increase()
        {
            int iTempCount = ILOOP_COUNT;

            while (iTempCount-- > 0)
            {
                lock (thisLock)
                {
                    _iCount++;
                }
                Thread.Sleep(1);
            }
        }
        
        public void LF_Decrease()
        {
            int iTempCount = ILOOP_COUNT;

            while (iTempCount-- > 0)
            {
                lock (thisLock)
                {
                    _iCount--;
                }
                Thread.Sleep(1);
            }
        }
    }
    
    class Program
    {
        static void Main(string[] args)
        {
            Counter counter = new Counter();

            Thread thIncrease = new Thread(new ThreadStart(counter.LF_Increase));
            Thread thDecrease = new Thread(new ThreadStart(counter.LF_Decrease));

            thIncrease.Start();
            thDecrease.Start();

            thIncrease.Join();
            thDecrease.Join();
            
            Console.WriteLine($"{counter.Get_Count}");
        }
    }

```

### (3) Motitor Class

 **① Monitor Class Synchronization Process**
- lock Keyword를 사용할 때 보다 더욱 세밀한 Multi Thread Synchronization이 가능하다.
- Motitor.Wait( ), Monitor.Pulse( )는 lock 블럭 안에서 호출해야 한다. 그렇게 하지 않고 호출하게 되면 CLR이 SynchronizationLockException을 발생 시킨다.
- Monitor.Wait( )를 호출하면 Thread를 SleepWaitJoin상태로 만들고 SleepWaitJoin 상태가 된 Thread는 동기화를 위해 가지고 있는 lock 내려놓고 Waiting Queue에 입력된다.
- 다른 Thread가 lock을 얻어 작업을 수행하고 작업을 수행하던 Thread가 Monitor.Pulse( ) 호출하면 Waiting Queue에서 첫번째 위치에 있는 Thread를 꺼내서 Ready Queue에 입력시킨다.
- Ready Queue에 입력된 Thread는 lock를 얻어서 Running 상태에 들어간다.
```C#
    class Counter
    {
        const int _LOOP_COUNT = 100;
        readonly object thisLock;
        private int _iCount;
        bool _bLockedCount = false;

        public int GET_Count
        {
            get
            {
                return _iCount;
            }
        }

        public Counter()
        {
            thisLock = new object();
            _iCount = 0;
        }

        public void LF_Increase()
        {
            int iTempLoopCount = _LOOP_COUNT;

            while (iTempLoopCount-- > 0)
            {
                lock (thisLock)
                {
                    while (_iCount < 0 || _bLockedCount == true)
                        Monitor.Wait(thisLock);

                    _bLockedCount = true;
                    _iCount++;
                    _bLockedCount = false;

                    Monitor.Pulse(thisLock);
                }
            }
        }

        public void LF_Decrease()
        {
            int iTempLoopCount = _LOOP_COUNT;

            while (iTempLoopCount-- > 0)
            {
                lock (thisLock)
                {
                    while (_iCount < 0 || _bLockedCount == true)
                        Monitor.Wait(thisLock);

                    _bLockedCount = true;
                    _iCount--;
                    _bLockedCount = false;

                    Monitor.Pulse(thisLock);
                }
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Counter counter = new Counter();
            Thread thIncrease = new Thread(new ThreadStart(counter.LF_Increase));
            Thread thDecrease = new Thread(new ThreadStart(counter.LF_Decrease));

            thIncrease.Start();
            thDecrease.Start();

            thIncrease.Join();
            thDecrease.Join();
            Console.WriteLine($"{counter.GET_Count}");
            Console.ReadLine();
        }
    }
```

**② Thread.Sleep( )과 Monitor.Wait( ) 차이점**
- Thread.Sleep( )과 Monitor.Wait( )는 Thread를 SleepWaitJoin상태로 만들지만 Thread.Sleep( )은 Monitor.Pulse( )에 의해서 깨어날 수 없다.
- Thread.Sleep( )이 Running 상태가 되기 위해서는 매개변수로 입력한 시간이 경과 되거나, Interrupt( ) 호출을 받아야 한다. 


 
