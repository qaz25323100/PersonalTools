
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

## Thread共享共同參數  

兩個執行序都有用到ShareState中的item這個變數...  
程式中為了模擬實際情況，t1延遲時間及t2延遲時間不盡相同  
  
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
            item++;

            Thread.Sleep((int)Delay);
            Console.WriteLine("["+Thread.CurrentThread.ManagedThreadId+"] Current Item:"+ item);
        }

    }  
  
Output  
  
    [6] Current Item:2
    [5] Current Item:2
