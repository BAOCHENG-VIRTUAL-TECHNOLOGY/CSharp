# CSharp

[C# 语言参考 | Microsoft Learn](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/)

| 类型       |                                                              |                |
| ---------- | ------------------------------------------------------------ | -------------- |
| 值类型     | 概述<br />整型数值类型<br />浮点型数值类型<br />内置数值转换<br />bool<br />char<br />枚举类型<br />结构类型<br />Ref 结构类型<br />元组类型<br />可以为 null 的值类型 | \              |
| 引用类型   | 引用类型的功能<br />内置引用类型<br />记录 (record)<br />class<br />interface<br />可为空引用类型 | \              |
|            | 集合和数组                                                   | 集合<br />数组 |
| void       | \                                                            | \              |
| 内置类型   | \                                                            | \              |
| 非托管类型 | \                                                            | \              |
| 默认值     | \                                                            | \              |

# 值类型

## 概述

默认情况下，在分配中，通过将实参传递给方法并返回方法结果来复制变量值。对于值类型变量，会复制相应的类型实例。

```c#
using system;
public struct MutablePoint{
    public int X;
    public int Y;
    public MutablePoint(int x, int y)=>(X, Y)=(x,y);
    public override string ToString()=>$"({X},{Y})";
}
public class Program
{
    public static void Main()
    {
        var p1=new MutablePoint(1,2);
        var p2=p1;
        p2.Y=200;
        Console.WriteLine($"{nameof(p1)} after {nameof(p2)} is modified: {p1}");
        Console.WriteLine($"{nameof(p2)}: {p2}");
        MutateAndDisplay(p2);
        Console.WriteLine($"{nameof(p2)} after passing to a method: {p2}");
    }
    private static void MutateAndDisplay(MutablePoint p)
    {
        p.X=100;
        Console.WriteLine($"Point mutated in a method: {p}");
    }
}
// Expected output:
// p1 after p2 is modified: (1, 2)
// p2: (1, 200)
// Point mutated in a method: (100, 200)
// p2 after passing to a method: (1, 200)
```

对值类型变量的操作只影响存储在变量中的值类型实例。

---

如果值类型包含引用类型的数据成员，则在复制值类型实例时，只会复制对引用类型实例的引用。副本和原始值类型实例都具有对同一引用类型实例的访问权限。

```c#
using System;
using System.Collection.Generic;
public struct TaggedInteger
{
	public int Number;
	private List<string> tags;
	public TaggedInteger(int n)
	{
		Number = n;
        tags = new List<string>();
	}
    publci void AddTag(string tag)=>tags.Add(tag);
    public override string ToString()=>$"{Number}[{string.Join(", ", tags)}]";
}
public class Program
{
    public static void Main()
    {
        var n1 = new TaggedInteger(0);
        n1.AddTag("A");
        Console.WriteLine(n1);
        
        var n2=n1;
        n2.Number=7;
        n2.AddTag("B");
        
        Console.WriteLine(n1);
        Console.WriteLine(n2);
    }
}
```

# 引用类型

## 引用类型的功能

C# 中有两种类型：引用类型和值类型。引用类型的变量存储对其数据（对象）的引用，而值类型的变量直接包含其数据。对于引用类型，两种变量可引用同一对象；因此，对一个变量执行的操作会影响另一个变量所引用的对象。对于值类型，每个变量都具有其自己的数据副本，对一个变量执行的操作不会影响另一个变量（in、ref 和 out 参数变量除外）

| 下列关键字用于声明引用类型 |
| -------------------------- |
| class                      |
| interface                  |
| delegate                   |
| record                     |

| C# 提供的内置引用类型 |
| --------------------- |
| dynamic               |
| object                |
| string                |

