# C#

## 存取範圍層級

**類別預設的存取修飾詞是 internal**
**類別成員預設的存取修飾詞是 private**

### public: 存取不受限制

#### Example 1.  

如把public 改為protected或private會出現 **'Circle.radius' 由於其保護層級之故，所以無法存取。**

    class Program
    {
        static void Main(string[] args)
        {
            Circle c = new Circle();
            
            Console.WriteLine(c.radius);
        }
    }
    class Circle
    {
        public int radius=3;
    }
    
    // Output: 3

### protected: 存取僅限於此類別或衍生類別執行個體存取。

#### Example 1.
a.radius會出現錯誤，**無法經由類型 'Circle' 的限定詞，來存取保護的成員 'Circle.radius'; 限定詞必須是類型 'Program' (或從其衍生的類型)**  

而b.radius不會出現錯誤，因為**它是Circle的衍生類別**

    class Program:Circle
    {
        static void Main(string[] args)
        {
            var a = new Circle();
            var b = new Program();
            
            //Console.WriteLine(a.radius);
            b.radius = 3;
        }
    }
    class Circle
    {
        protected int radius=123;
    }

#### Example 2.

如把protected改為private會出現 **'Circle.radius' 由於其保護層級之故，所以無法存取。**

    class Program:Circle
    {
        static void Main(string[] args)
        {
            var a = new Program();
            var b = new Program();
            
            Console.WriteLine(a.radius);
            b.radius = 3;
        }
    }
    class Circle
    {
        protected int radius = 123;
        protected int area = 123;
    }
    
    // Output: 123
  
### private: 存取僅限於此類別主體或結構主體內。

因radius宣告為private存取權限，因此需透過public方法GetRadius()進行存取。  
  
    class Program
    {
        static void Main(string[] args)
        {
            var a = new Program();
            
            Console.WriteLine(a.GetRadius());
        }
    }
    class Circle
    {
        private int radius=123;
        public int GetRadius() => this.radius;
    }

### internal: 存取範圍是相同組件(Assembly)都可以使用，internal可以在同一個dll內存取。




## const 跟 static readonly 差別

const 是編譯時賦予值，static readonly 是執行時賦予值

## Async and Await

c# 5.0所推出的功能，避免再存取網頁或檔案時，可以先處理非相關業務，避免等待時間過久

![image](https://user-images.githubusercontent.com/7361217/132455051-fe85aa63-66d0-4d42-9cc2-f83f48104097.png)


# Dotnet Core

https://blog.darkthread.net/blog/add-mvc-to-razor-project/

Startup.cs
> https://www.strathweb.com/2020/02/asp-net-core-mvc-3-x-addmvc-addmvccore-addcontrollers-and-other-bootstrapping-approaches/

## Filter

https://blog.johnwu.cc/article/ironman-day14-asp-net-core-filters.html

## 待分類

https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/mvc/controllers/filters/3.1sample/FiltersSample/Filters
