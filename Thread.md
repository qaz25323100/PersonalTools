
> Process vs Thread  
> https://www.huanlintalk.com/2013/04/csharp-notes-multithreading-1.html  
> 執行序介紹  
> https://www.huanlintalk.com/2013/05/csharp-notes-multithreading-2.html
  
## C# 工作執行序WorkerThread(不帶參數)  
    class Program
    {
        static void Main(string[] args)
        {
            Thread a = new Thread(PrintNum);
            

            a.Start();
            

            for(int i=0;i<100;i++){
                Console.Write(".");
            }
        }

        static void PrintNum(){
            for(int i=0;i<100;i++){
                Console.WriteLine(i);
            }
        }
    }
    
## C# 工作執行序WorkerThread(帶參數)  
    
    class Program
    {
        static void Main(string[] args)
        {
            Thread a = new Thread(PrintNum);
            Thread b = new Thread(PrintNum);
            Thread c = new Thread(PrintNum);

            a.Start("a");
            b.Start("b");
            c.Start("c");

            for(int i=0;i<100;i++){
                Console.Write(".");
            }
        }

        static void PrintNum(object p){
            for(int i=0;i<100;i++){
                Console.WriteLine(p);
            }
        }
    }
### Thread有無參數(ThreadStart V.S ParameterizedThreadStart)
    public delegate void ThreadStart();  
    public delegate void ParameterizedThreadStart(object? obj);  

## Thread.Join()
    
等待a、b、c執行序跑完，才跑主程式  
  
    class Program
    {
        static void Main(string[] args)
        {
            Thread a = new Thread(PrintNum);
            Thread b = new Thread(PrintNum);
            Thread c = new Thread(PrintNum);

            a.Start("a");
            b.Start("b");
            c.Start("c");

            a.Join();
            b.Join();
            c.Join();

            for (int i = 0; i < 5; i++)
            {
                Console.Write(".");
            }
        }

        static void PrintNum(object p)
        {
            for (int i = 0; i < 5; i++)
            {
                Console.Write(p);
            }
        }
    }
  
Output  
  
    bbbbbaaaaaccccc.....

## Thread共享共同參數問題  

兩個執行序都有用到ShareState中的item這個變數...  
  
    class Program
    {
        static void Main(string[] args)
        {
            new ShareState().Run();
        }
    }

    public class ShareState{
        private int item = 0;

        public void Run(){
            var t1 = new Thread(AddItem);
            var t2 = new Thread(AddItem);

            t1.Start(300);
            t2.Start(100);
        }

        private void AddItem(object Delay){
            Console.WriteLine("["+Thread.CurrentThread.ManagedThreadId+"]");
            item++;

            Thread.Sleep((int)Delay);
            Console.WriteLine("["+Thread.CurrentThread.ManagedThreadId+"] Current Item:"+ item);
        }

    }
  
Output  
1.t1先進入AddItem執行item++，延遲了300ms  
2.t1此時延遲的當下，t2也執行了AddItem也執行了item++，並執行延遲100ms  
3.t2延遲完，執行WriteLine，爾後，t1延遲完，執行WriteLine  
  

    [5]
    [6]
    [6] Current Item:2
    [5] Current Item:2

## 鎖(Lock)  

為解決上述共享變數問題，因此透過互斥鎖(exclusive lock)  
迫使各執行緒存取共享變數時乖乖排隊，亦即令它們同步化（synchronization）。  

    class Program
    {
        static void Main(string[] args)
        {
            new ShareState().Run();
        }
    }

    public class ShareState
    {
        private int item = 0;

        private object locker = new Object(); // 用於獨佔鎖定的物件
        public void Run()
        {
            var t1 = new Thread(AddItem);
            var t2 = new Thread(AddItem);

            t1.Start(300);
            t2.Start(100);
        }

        private void AddItem(object Delay)
        {
            Console.WriteLine("[" + Thread.CurrentThread.ManagedThreadId + "]");

            lock (locker)
            {
                item++;

                Thread.Sleep((int)Delay);
                Console.WriteLine("[" + Thread.CurrentThread.ManagedThreadId + "] Current Item:" + item);
            }
        }

    }
  Output
    
    [7]
    [6]
    [7] Current Item:1
    [6] Current Item:2
