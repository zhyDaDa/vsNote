---
   tags:
      - C#
      - 编程
      - 学习笔记
---

## 主要内容
- 安装了vs
- 熟悉VisualStudio
- 两行代码
- - -

## 熟悉VisualStudio
- **解决方案**包含多个**项目**, 项目又包含多个**类文件**
- 项目中最要紧的是program\.cs文件
- \.cs文件被统称为**类文件**
> **解决方案**就是"公司"  
> **项目**就是"部门"  
> **类文件**就是"员工"  
  
- 代码区
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
//以上是引用命名空间
namespace _01_My_First_Demo //项目名称&命名空间
{
    class Program //被class修饰, 说明是个类
    {
        static void Main(string[] args) //方法or函数 程序的主入口
        {  //代码从这里走起

        }
    }
}
```
> 所谓**引用命名空间**其实就是定语
>> "淘宝"=>"网上项目"=>"客户类"  
>> "京东"=>"网上项目"=>"客户类"
>
> 其中两个"客户类"毫无关联, 前面的定语就是**引用命名空间**

> **方法**就是**函数**  
> **main函数**就是程序的**主入口**

+ 在解决方案中
  - **\.suo**是不可以操作的
  - **\.sln**叫做*解决方案文件*, 包含着解决方案的信息  
+ 在项目文件夹中
  - **.csproj**是*项目文件*, 包含项目信息

## 两行代码
```
Console.WriteLine("I'm zhyDaDa");
Console.ReadKey();
```
- Console.WriteLine("输出内容");
- Console.ReadKey(); 暂停 (约等于bat中的pause)
- - -
# 总结
- 大致代码样式get
- 以及应用命名空间的概念