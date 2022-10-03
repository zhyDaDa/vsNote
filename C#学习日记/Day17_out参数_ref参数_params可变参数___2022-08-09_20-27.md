---
title: DayDay17_out参数_ref参数_params可变参数___2022-08-09_20-27
date: 2022-08-09T20:27:04+08:00
tags:
    - C井学习笔记
    - study
---
目录
- [引入练习](#引入练习)
- [***out***参数](#out参数)
- [***out***练习](#out练习)
- [***ref***参数](#ref参数)
- [***params***可变参数](#params可变参数)

## 引入练习
- 求数组的最大值, 最小值, 总和, 平均值
- 由于返回*多个同类型*的值, 所以返回数组
```
static void Main(string[] args) //Main函数
{  //代码从这里走起
    int[] numbers = { 1, 2, 3, 4, 5, 6 };
    int[] res = GetMaxMinSumAvg(numbers);
    Console.WriteLine("最大值: {0}\n最小值: {1}\n总和: {2}\n平均值: {3}", res[0], res[1], res[2], res[3]);
}
/// <summary>
/// 输入整数数组, 返回一个数组
/// 元素依次是: 最大值, 最小值, 总和, 平均数
/// </summary>
/// <param name="numbers">数组</param>
/// <returns>数组</returns>
public static int[] GetMaxMinSumAvg(int[] numbers)
{
    int[] res = new int[4];
    res[0] = numbers[0];
    res[1] = numbers[0];
    res[2] = 0;
    for (int i = 0; i < numbers.Length; i++)
    {
        if (numbers[i] > res[0])    //修改最大值
        {
            res[0] = numbers[i];
        }
        if (numbers[i] < res[1])    //修改最小值
        {
            res[1] = numbers[i];
        }
        res[2] += numbers[i];
    }
    res[3] = res[2] / numbers.Length;
    return res;
}
```
> 但是, 如果要返回多个不同类型的值的时候, 返回数组就不行  
> 此时, 考虑使用***out***参数


## ***out***参数
- ***out***参数侧重于在一个方法中返回多个不同类型的值
- **注意**:
  + 在`main函数`中可以不给那四个值赋值, 因为函数为其赋值
  + 实参形参前面都要记得带上***out***关键字


- 引入练习中使用***out***

```
static void Main(string[] args) //Main函数
{  //代码从这里走起
    int[] numbers = { 1, 2, 3, 9, 5, -6 };
    int max = 0;
    int min = 0;
    int sum = 0;
    int avg = 0;
    GetMaxMinSumAvg(numbers, out max, out min, out sum, out avg);
    Console.WriteLine("最大值: {0}\n最小值: {1}\n总和: {2}\n平均值: {3}", max, min, sum, avg);
}
/// <summary>
/// 计算一个整数数组的 最大值, 最小值, 总和, 平均数
/// </summary>
/// <param name="numbers">要求的数组</param>
/// <param name="max">多余返回的最大值</param>
/// <param name="min">多余返回的最小值</param>
/// <param name="sum">多余返回的总和</param>
/// <param name="avg">多余返回的平均值</param>
public static void GetMaxMinSumAvg(int[] numbers, out int max, out int min, out int sum, out int avg)
{
    max = numbers[0];
    min = numbers[0];
    sum = 0;
    for (int i = 0; i < numbers.Length; i++)
    {
        if (numbers[i] > max)    //修改最大值
        {
            max = numbers[i];
        }
        if (numbers[i] < min)    //修改最小值
        {
            min = numbers[i];
        }
        sum += numbers[i];
    }
    avg = sum / numbers.Length;
}
```

## ***out***练习
- 会提示错误原因的登录系统, 当然是要用方法的那种
```
static void Main(string[] args) //Main函数
{  //代码从这里走起
    Console.WriteLine("输入用户名");
    string name = Console.ReadLine();
    Console.WriteLine("请输入密码");
    string pwd = Console.ReadLine();
    string msg;
    bool b = IsLogin(name, pwd, out msg);
    Console.WriteLine("登录结果为: {0}\n登录信息: {1}", b, msg);

}
/// <summary>
/// 判断用户名和密码是否正确
/// </summary>
/// <param name="name">用户名</param>
/// <param name="pwd">密码</param>
/// <param name="msg">提示信息</param>
/// <returns>登陆成功返回true</returns>
public static bool IsLogin(string name, string pwd, out string msg)
{
    if (name =="admin" && pwd == "666666")
    {
        msg = "登陆成功";
        return true;
    }
    else if (name == "admin")
    {
        msg = "密码错误";
        return false;
    }
    else if (pwd == "666666")
    {
        msg = "用户名错误";
        return false;
    }
    else
    {
        msg = "未知错误";
        return false;
    }
}
```
- 模仿***TryParse***

```
public static bool MyTryParse(string s, out int result)
{
    result = 0;
    try
    {
        result = Convert.ToInt32(s);
        return true;
    }
    catch
    {
        return false;
    }
}
```

## ***ref***参数
- ***ref***参数能够将一个变量带入方法中进行改变, 改变完成后, 再将改变后的参数导出方法  
- **注意**: ***ref***参数要求在方法外必须为其赋值, 而方法内可以不赋值
> 弹幕里多次提到"指针", 我理解为*内存地址*

- 使用方法来交换两个int类型的变量

```
static void Main(string[] args) //Main函数
{  //代码从这里走起
    int n1 = 20;
    int n2 = 99;
    SwitchTwoInt(ref n1, ref n2);
    Console.WriteLine(n1 + "\n" + n2);
}

public static void SwitchTwoInt(ref int n1, ref int n2)
{
    n1 = n1 - n2;
    n2 = n1 + n2;
    n1 = n2 - n1;
}
```

## ***params***可变参数
- ***params***可变参数能将实参列表中跟**可变参数数组类型**一致的元素都当做数组的元素去处理  
- **注意**: ***params***可变参数**必须**是形参列表中最后一个参数

```
static void Main(string[] args) //Main函数
{  //代码从这里走起
    int sum1 = GetSum(21, 323, 3, 13, 2123, 21, 4);
    int[] nums = { 21, 323, 3, 13, 2123, 21, 4 };
    int sum2 = GetSum(nums);
    Console.WriteLine(sum1);
    Console.WriteLine(sum2);
}
public static int GetSum(params int[] nums)
{
    int sum = 0;
    for (int i = 0; i < nums.Length; i++)
    {
        sum += nums[i];
    }
    return sum;
}
```