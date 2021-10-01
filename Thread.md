
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
** 
    public delegate void ThreadStart();  
    public delegate void ParameterizedThreadStart(object? obj);  
**
