---
title: DayDay17_out参数_ref参数_params可变参数___2022-08-09_20-27
date: 2022-08-09T20:27:04+08:00
tags:
    - C#学习笔记
    - study
---
目录
- [引入练习](#引入练习)
- [***out***参数](#out参数)

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