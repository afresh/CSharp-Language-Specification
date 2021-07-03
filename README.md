# C# 编码规范




[1 前言](#user-content-1-%E5%89%8D%E8%A8%80)

[2 代码风格](#user-content-2-%E4%BB%A3%E7%A0%81%E9%A3%8E%E6%A0%BC)

　　[2.1 文件](#user-content-21-%E6%96%87%E4%BB%B6)

　　[2.2 结构](#user-content-22-%E7%BB%93%E6%9E%84)

　　　　[2.2.1 缩进](#user-content-221-%E7%BC%A9%E8%BF%9B)

　　　　[2.2.2 空格](#user-content-222-%E7%A9%BA%E6%A0%BC)

　　　　[2.2.3 换行](#user-content-223-%E6%8D%A2%E8%A1%8C)

　　　　[2.2.4 语句](#user-content-224-%E8%AF%AD%E5%8F%A5)

　　[2.3 命名](#user-content-23-%E5%91%BD%E5%90%8D)

　　[2.4 注释](#user-content-24-%E6%B3%A8%E9%87%8A)

　　　　[2.4.1 单行注释](#user-content-241-%E5%8D%95%E8%A1%8C%E6%B3%A8%E9%87%8A)

　　　　[2.4.2 多行注释](#user-content-242-%E5%A4%9A%E8%A1%8C%E6%B3%A8%E9%87%8A)

　　　　[2.4.3 摘要注释](#user-content-243-%E6%91%98%E8%A6%81%E6%B3%A8%E9%87%8A)

　　　　[2.4.4 细节注释](#user-content-244-%E7%BB%86%E8%8A%82%E6%B3%A8%E9%87%8A)






## 1 前言


本文档的目标是使 C# 代码风格保持一致，容易被理解和被维护，应尽量遵循本文档的约定。





## 2 代码风格






### 2.1 文件


##### [建议] 文件使用无 `BOM` 的 `UTF-8` 编码。

解释：

UTF-8 编码具有更广泛的适应性。BOM 在使用程序或工具处理文件时可能造成不必要的干扰。

##### [建议] 在文件结尾处，保留一个空行。




### 2.2 结构



#### 2.2.1 缩进


##### [强制] 使用 `tab` 做为一个缩进层级，不允许使用空格。



##### [强制] `switch` 下的 `case` 和 `default` 必须增加一个缩进层级。

示例：

```C#
// good
switch (strProcCode)
{
    //TODO: 业务逻辑（申请、同意、拒绝、运行中撤销、同意后撤销）
    case "PROC0001": //请假
        tuple = AskForLeaveLogic.Approval(ref input);
        break;
    case "PROC0101": //申请寝室长
        tuple = SuSheLogic.DormitoryLeader(ref input);
        break;
    case "PROC0102": //申请留校
        tuple = SuSheLogic.StayDormitory(ref input);
        break;
}

// bad
switch (strProcCode)
{
//TODO: 业务逻辑（申请、同意、拒绝、运行中撤销、同意后撤销）
case "PROC0001": //请假
    tuple = AskForLeaveLogic.Approval(ref input);
    break;
case "PROC0101": //申请寝室长
    tuple = SuSheLogic.DormitoryLeader(ref input);
    break;
case "PROC0102": //申请留校
    tuple = SuSheLogic.StayDormitory(ref input);
    break;
}
```

#### 2.2.2 空格



##### [强制] 二元运算符两侧必须有一个空格，一元运算符与操作对象之间不允许有空格。

示例：

```C#
var a = !arr.Count;
a++;
a = b + c;
```

##### [强制] `if / for / while / switch / try / catch` 关键字后，必须有一个空格。

示例：

```C#
// good
if (condition)
{
}

while (condition)
{
}

// bad
if(condition)
{
}

while(condition)
{
}
```

##### [强制] 方法声明、方法调用中，方法名和 `(` 之间不允许有空格。

示例：

```C#
// good
public static APOutput CreateProcessInstance(APInput input) {
}

var output = ProcessLogic.CreateProcessInstance(input);

// bad
public static APOutput CreateProcessInstance (APInput input) {
}

var output = ProcessLogic.CreateProcessInstance (input);
```

##### [强制] `,` 和 `;` 前不允许有空格。如果不位于行尾，`,` 和 `;` 后必须跟一个空格。

示例：

```C#
// good
CallFunc(a, b);

// bad
CallFunc(a , b) ;
```

##### [强制] 在方法调用、方法声明、括号表达式、属性访问、`if / for / while / switch / catch` 等语句中，`()` 和 `[]` 内紧贴括号部分不允许有空格。

示例：

```C#
// good

CallFunc(param1, param2, param3);

Save(list[indexes[i]]);

needIncream && (variable += increament);

if (num > list.Count)
{
}

while (len--)
{
}


// bad

CallFunc( param1, param2, param3 );

Save( list[ indexes[ i ] ] );

needIncreament && ( variable += increament );

if ( num > list.Count )
{
}

while ( len-- )
{
}
```

##### [强制] 行尾不得有多余的空格。


#### 2.2.3 换行


##### [强制] 每个独立语句结束后必须换行。

##### [强制] 用作代码块起始的左花括号 `{` 前必须换行。

示例：

```C#
// good
if (condition)
{
}

while (condition)
{
}

public static APOutput CreateProcessInstance(APInput input)
{
}

// bad
if (condition) {
}

while (condition) {
}

public static APOutput CreateProcessInstance(APInput input) {
}
```

##### [强制] 每行不得超过 `120` 个字符。

解释：

超长的不可分割的代码允许例外，比如复杂的正则表达式。长字符串不在例外之列。


##### [强制] 运算符处换行时，运算符必须在新行的行首。

示例：

```C#
// good
if (user.IsAuthenticated()
    && user.IsInRole('admin')
    && user.HasAuthority('add-admin')
    || user.HasAuthority('delete-admin'))
{
    // Code
}

var result = number1 + number2 + number3
    + number4 + number5;


// bad
if (user.IsAuthenticated() &&
    user.IsInRole('admin') &&
    user.HasAuthority('add-admin') ||
    user.HasAuthority('delete-admin'))
{
    // Code
}

var result = number1 + number2 + number3 +
    number4 + number5;
```

##### [建议] 不同行为或逻辑的语句集，使用空行隔开，更易阅读。

示例：

```C#
// 仅为按逻辑换行的示例，不代表SetValue的最优实现
public static void SetValue(JObject obj, string key, JToken value) {
    if (obj == null) {
        return;
    }

    obj[key] = value;
}
```

##### [建议] 对于 `if...else...`、`try...catch...finally` 等语句，推荐使用在 `}` 号后添加一个换行 的风格，使代码层次结构更清晰，阅读性更好。

示例：

```C#
if (condition)
{
    // some statements;
}
else
{
    // some statements;
}

try
{
    // some statements;
}
catch (ex)
{
    // some statements;
}
```



#### 2.2.4 语句


##### [强制] 在 `if / else / for / do / while` 语句中，即使只有一行，也不得省略块 `{...}`。

示例：

```C#
// good
if (condition)
{
    CallFunc();
}

// bad
if (condition) CallFunc();
if (condition)
    CallFunc();
```





### 2.3 命名


##### [强制] `private` 修饰的 `变量` 使用 `camel命名法`，并加 `下划线`。

示例：

```C#
private int _count = 0;
```

##### [强制] `private static` 修饰的 `变量` 使用 `camel命名法`，并加 `下划线`。

示例：

```C#
private static int _count = 0;
```

##### [强制] `private readonly` 修饰的 `变量` 使用 `camel命名法`，并加 `下划线`。

示例：

```C#
private readonly int _count = 0;
```

##### [强制] `private static readonly` 修饰的 `变量` 使用 `Pascal命名法`。

示例：

```C#
private static readonly int Count = 0;
```

##### [强制] 只要有 `public` 修饰的 `变量` 就使用 `Pascal命名法`。

示例：

```C#
public int Count = 0;
```

##### [强制] `局部变量` 使用 `camel命名法`。

示例：

```C#
var count = 0;
```

##### [强制] `类中的常量` 使用 `Pascal命名法`。

示例：

```C#
private const int Count = 0;
```

##### [强制] `全局常量` 使用 `全部字母大写，单词间下划线分隔` 的命名方式。

示例：

```C#
public const SYNC_COUNT = 0;
```

##### [强制] `方法` 使用 `Pascal命名法`。

示例：

```C#
public static void Sync()
{
}
```

##### [强制] 方法的 `参数` 使用 `camel命名法`。

示例：

```C#
public static void Sync(int count)
{
}
```


##### [强制] `类` 使用 `Pascal命名法`。

示例：

```C#
public class Logic
{
}
```

##### [强制] `枚举变量` 使用 `Pascal命名法`，`枚举的属性` 使用 `Pascal命名法` 或 `全部字母大写，单词间下划线分隔` 的命名方式。

示例：

```C#
/// <summary>
/// 审批状态
/// </summary>
public enum APProcessStatus
{
    /// <summary>
    /// 新创建
    /// </summary>
    NEW = 0,
    /// <summary>
    /// 运行中
    /// </summary>
    RUNNING = 1,
    /// <summary>
    /// 取消
    /// </summary>
    CANCELED = 2,
    /// <summary>
    /// 被终止
    /// </summary>
    TERMINATED = 3,
    /// <summary>
    /// 完成
    /// </summary>
    COMPLETED = 4
}
```

##### [强制] `命名空间` 使用 `Pascal命名法`。

示例：

```C#
namespace WebYKT.Model.Enums
{
}
```

##### [强制] 由多个单词组成的缩写词，在命名中，根据当前命名法和出现的位置，所有字母的大小写与首字母的大小写保持一致。

示例：

```C#
public static string XMLParser(string strXML)
{
}

public static void InsertXML(string strXML)
{
}

var httpRequest = new HTTPRequest();
```

##### [强制] `类名` 使用 `名词`。

示例：

```C#
public class Logic
{
}
```

##### [建议] `方法名` 使用 `动宾短语`。

示例：

```C#
public static void InsertXML(string strXML)
{
}
```

##### [建议] `async` 修饰的 `方法名` 加后缀 `Async` 。

示例：

```C#
public static async Task InsertXMLAsync(string strXML)
{
}
```

##### [建议] `bool` 类型的变量使用 `is` 或 `has` 开头。

示例：

```C#
var isReady = false;
var hasMoreCommands = false;
```




### 2.4 注释


#### 2.4.1 单行注释


##### [强制] 必须独占一行。`//` 后跟一个空格，缩进与下一行被注释说明的代码一致。

#### 2.4.2 多行注释


##### [建议] 避免使用 `/*...*/` 这样的多行注释。有多行注释内容时，使用多个单行注释。


#### 2.4.3 摘要注释


##### [强制] 为了便于代码阅读，以下内容必须包含以 `<summary>` 形式的摘要注释中。

解释：

1. 类
2. 方法或方法
3. 类属性
4. 事件
5. 全局变量
6. 常量

```C#
/// <summary>
/// 请求
/// </summary>
/// <param name="strUri">地址</param>
/// <returns>返回内容</returns>
public static string Request(string strUri)
{
    // ……
}
```



#### 2.4.4 细节注释


对于内部实现、不容易理解的逻辑说明、摘要信息等，我们可能需要编写细节注释。

##### [建议] 细节注释遵循单行注释的格式。说明必须换行时，每行是一个单行注释的起始。

示例：

```C#
public static string Request(string strUri)
{
    // 这里对具体内部逻辑进行说明
    // 说明太长需要换行
    for (...) {
        ....
    }
}
```

##### [强制] 有时我们会使用一些特殊标记进行说明。特殊标记必须使用单行注释的形式。下面列举了一些常用标记：

解释：

1. TODO: 有功能待实现。此时需要对将要实现的功能进行简单说明。
2. #region #endregion: 注释其中间的代码段，或者折叠中间的代码块。注意#region和#endregion的上下换行。

```C#
#region 说明

// ……

#endregion
```



