# C#

## 存取範圍層級

### public: 存取不受限制

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
