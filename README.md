# ExpressionEvaluator
A Simple Math and Pseudo C# Expression Evaluator in One C# File.

It is largely based on and inspired by the following resources [this post on stackoverflow](http://stackoverflow.com/questions/333737/evaluating-string-342-yield-int-18/333749), [NCalc](https://ncalc.codeplex.com/) and [C# Operators](https://msdn.microsoft.com/en-us/library/6a71f45d.aspx)

## Basic usage
```c#
string expression;
...
ExpressionEvaluator evaluator = new ExpressionEvaluator();
Console.Write(expression);
Console.Write(evaluator.Evaluate(expression));
```
Results with some expressions :
```
1+1
2

2 + 3 * 2
8

(2 + 3) * 2
10

Pi
3.14159265358979

Pow(2, 4)
16

Sqrt(2) / 3
0.471404520791032

"Hello" + " " + "World"
Hello World

Max(1+1, 2+3, 2*6, Pow(2, 3))
12

Array(2, $"Test { 2 + 2 } U", true).Length
3

Array(2, $"Test { 2 + 2 } U", true)[1]
Test 4 U

if(Array(2, $"Test { 2 + 2 } U", true)[2], "yes" , "no")
yes

"Hello\nWorld"
Hello
World

@"Hello\nWorld"
Hello\nWorld

Regex.Match("Test 34 Hello/-World", @"\d+").Value
34

int.Parse(Regex.Match("Test 34 Hello/-World", @"\d+").Value) + 2
36

3 / 2
1

3d / 2d
1.5

(float)3 / (float)2
1.5
```

## Standard constants (variables)

The evaluation of variables name is case insensitive so you can write it like you want to.

|Constant|Value|Type|
|---|---|---|
|null|C# null value|N/A|
|true|C# true value|System.Boolean|
|false|C# false value|System.Boolean|
|Pi|3.14159265358979|System.Double|
|E|2.71828182845905|System.Double|

## Custom variables

You can define your own variables

Examples : 
```C#
ExpressionEvaluator evaluator = new ExpressionEvaluator();
evaluator.Variables = new Dictionary<string, object>()
{
  { "x", 2,5 },
  { "y", -3.6 },
  { "myVar", "Hello World" }
  { "myArray", new object[] { 3.5, "Test", false}
};
```
```
x+y
-1.1

myVar + " !!!"
Hello World !!!

myArray.Length
3

myArray[0]
3.5

myArray[1].Length
4

myArray[2] || true
True
```

*Remark : custom variable evaluation is case insensitive*

## Standard Functions
The following functions are internally defined. (Most of these are System.Math Methods directly accessible)
The evaluation of functions names is case insensitive.

|Name|Description|Example|Result|
|---|---|---|---|
|**Abs**(double number)|Return a double that is the absolute value of number|`Abs(-3.2d)`|`3.2d`|
|**Acos**(double d)|Return a double value that is the angle in radian whose d is the cosine<br/>d must be betwteen -1 and 1|`Acos(-0.5d)`|`2.0943951023032d`|
|**Array**(object obj1, object obj2 ,...)|Return a array (System.Object[]) of all given arguments|`Array(1, "Hello", true)`|`new object[]{1, "Hello", true)`|
|**Asin**(double d)|Return a double value that is the angle in radian whose d is the sine<br/>d must be betwteen -1 and 1|`Asin(-0.2d)`|`0.304692654015398d`|
|**Atan**(double d)|Return a double value that is the angle in radian whose d is the tangent|`Atan(2.1)`|`1.1263771168938d`|
|**Atan2**(double x, double y)|Return a double value that is the angle in radian whose the tangente is the quotient of x and y<br/>|`Atan2(2.1d, 3.4d)`|`0.553294325322293d`|
|**Avg**(double nb1, double nb2 ,...)|Return a double value taht is the average value of all given arguments|`Avg(1, 2.5, -4, 6.2)`|`1.425d`|
|**Ceiling**(double a)|Return a double value that is the smallest integer greater than or equal to the specified number.|`Ceiling(4.23d)`|`5d`|
|**Cos**(double angle)|Return a double value that is the cosine of the specified angle in radian|`Cos(2 * Pi)`|`1d`|
|**Cosh**(double angle)|Return a double value that is the hyperbolic cosine of the specified angle in radian|`Cosh(2d)`|`3.76219569108363d`|
|**Exp**(double d)|Return a double value that is e raised to the specified d power|`Exp(3d)`|`20.0855369231877d`|
|**Floor**(double d)|Return a double value that is the largest integer less than or equal to the specified d argument|`Floor(4.23d)`|`4d`|
|**if**(bool condition, object yes, object no)|Return the yes object value if condition is true.<br/>Return the no object if condition is false|`if(1>2, "It is true", "It is false")`|`"It is false"`|
|**Log**(double a, double base)|Return a double value that is the logarithm of a in the specified base|`Log(64d, 2d)`|`6d`|
|**Log10**(double a)|Return a double value that is the base 10 logarithm of a specified a|`Log10(1000d)`|`3d`|
