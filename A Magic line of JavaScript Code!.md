# A Magic line of JavaScript Code

@author: Tianhuan Tu

@date: 2021-10-08



------



Do you know JavaScript ? 

> Yes.

Have long have you learnt JavaScript?  

> A few years.

How well do you believe you master JavaScript?

> Intermediate +

Great! Please try to tell what the following code below yields.

```javasript
(!(~+[])+{})[--[~+""][+[]]*[~+[]] + ~~!+[]]+({}+[])[[~!+[]]*~+[]]
```

>  What *** ?! ...

Don't feel irritated. It is not nonsense indeed.

Copy&paste the line of code into your browser's console, and ENTER!

>What *** ?! ...









------



Well, to figure out what it happens behind, we need to recall a little bit **Operators Priority** and **Type Conversion** in JavaScript. 



### JS fundamental recaps

#### JavaScript Operators

##### [Operators Types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#operators)

* Arithmetic Operators
* Logical Operators
* Bitwise Operators
* Assignment Operators
* Comparison Operators
* Conditional (ternary) Operator
* String Operators
* Unary Operators
* Relational Operators
* Comma Operator



| **category**                                                 |  **operator**  | **description**                              | **example**                              | **result** |
| ------------------------------------------------------------ | :------------: | -------------------------------------------- | :--------------------------------------- | :--------- |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       +        | Addition                                     |                                          |            |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       -        | Subtraction                                  |                                          |            |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       *        | Multiplication                               |                                          |            |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       /        | Division                                     |                                          |            |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       %        | Remainder                                    |                                          |            |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       ++       | Increment                                    |                                          |            |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       --       | Decrement                                    |                                          |            |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       +        | Unary plus (+)                               | \+”3” <br />+”true”                      | 3<br />1   |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       -        | Unary negation (-)                           |                                          |            |
| **[Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)** |       **       | Exponentiation operator (**)                 | 2**3                                     | 8          |
|                                                              |                |                                              |                                          |            |
| **[Logical operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#logical_operators)** |       &&       | Logical AND (&&)                             |                                          |            |
| **[Logical operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#logical_operators)** |      \|\|      | Logical OR (\|\|)                            |                                          |            |
| **[Logical operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#logical_operators)** |       !        | Logical NOT (!)                              |                                          |            |
|                                                              |                |                                              |                                          |            |
| **[Bitwise operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bitwise_operators)** |       &        | Bitwise AND                                  | 5 & 1                                    | 1          |
| **[Bitwise operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bitwise_operators)** |       \|       | Bitwise OR                                   | 5 \| 1                                   | 5          |
| **[Bitwise operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bitwise_operators)** |       ^        | Bitwise XOR                                  | 5^1                                      | 4          |
| **[Bitwise operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bitwise_operators)** |       ~        | Bitwise NOT                                  | ~5                                       | -6         |
| **[Bitwise operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bitwise_operators)** |       <<       | Left shift                                   | 5<<1                                     | 10         |
| **[Bitwise operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bitwise_operators)** |       >>       | Sign-propagating right shift                 | 5>>1                                     | 2          |
| **[Bitwise operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bitwise_operators)** |      >>>       | Zero-fill right shift                        | 5>>>1                                    | 2          |
|                                                              |                |                                              |                                          |            |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |       =        | Assignment                                   | x = y                                    | x = y      |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |       +=       | Addition assignment                          | x += y                                   | x = x + y  |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |       -=       | Subtraction assignment                       | x -= y                                   | x = x - y  |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |       *=       | Multiplication assignment                    | x *= y                                   | x = x * y  |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |       /=       | Division assignment                          | x /= y                                   | x = x / y  |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |       %=       | Remainder assignment                         | x %= y                                   | x = x%y    |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |      **=       | Exponentiation assignment                    | x **= y                                  | x = x**y   |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |      <<=       | Left shift assignment                        | x <<= y                                  | x = x<<y   |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |      >>=       | Right shift assignment                       | x >>= y                                  | x = x>>y   |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |      >>>=      | Unsigned right shift assignment              | x >>>= y                                 | x=x>>>y    |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |       &=       | Bitwise AND assignment                       | x &= y                                   | x=x&y      |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |       ^=       | Bitwise XOR assignment                       | x ^= y                                   | x = x ^ y  |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |      \|=       | Bitwise OR assignment                        | x \|= y                                  | x = x\|y   |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |      &&=       | Logical AND assignment                       | x &&= y                                  | x&&(x=y)   |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |     \|\|=      | Logical OR assignment                        | x \|\|= y                                | x\|\|(x=y) |
| **[Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators)** |      ??=       | Logical nullish assignment                   | x ??= y                                  | x??(x=y)   |
|                                                              |                |                                              |                                          |            |
| **[Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators)** |       ==       | Equal                                        |                                          |            |
| **[Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators)** |       !=       | Not equal                                    |                                          |            |
| **[Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators)** |      ===       | Strict equal                                 |                                          |            |
| **[Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators)** |      !==       | Strict not equal                             |                                          |            |
| **[Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators)** |       >        | Greater than                                 |                                          |            |
| **[Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators)** |       >=       | Greater than or equal                        |                                          |            |
| **[Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators)** |       <        | Less than                                    |                                          |            |
| **[Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators)** |       <=       | Less than or equal                           |                                          |            |
| **[Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comparison_operators)** |       ?        | ternary operator                             |                                          |            |
|                                                              |                |                                              |                                          |            |
| **[Conditional (ternary) operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#conditional_ternary_operator)** |      ? :       | Conditional ternary operator                 | con? v1:v2                               |            |
|                                                              |                |                                              |                                          |            |
| **[String operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#string_operators)** |       +        | Concatenation                                | "a" + "b"                                | "ab"       |
| **[String operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#string_operators)** |      \+=       | Concatenation assignment                     | x += y                                   |            |
|                                                              |                |                                              |                                          |            |
| **[Unary operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#unary_operators)** |   **delete**   | Delete an object’s property                  |                                          |            |
| **[Unary operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#unary_operators)** |     typeof     | Return variable type string                  |                                          |            |
| **[Unary operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#unary_operators)** |    **void**    | Evaluate an expression without a return      |                                          |            |
|                                                              |                |                                              |                                          |            |
| **[Relational operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#relational_operators)** |     **in**     | Evaluate if the property is in the object    |                                          |            |
| **[Relational operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#relational_operators)** | **instanceof** | Evaluate if the object is of the object type |                                          |            |
|                                                              |                |                                              |                                          |            |
| **[Comma operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#comma_operator)** |       ,        | return last result                           | for (var i = 0, j = 9; i <= j; i++, j--) |            |






##### [Operator Precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#operator_precedence)


The *precedence* of operators determines the order they are applied when  evaluating an expression. You can override operator precedence by using parentheses.

The following table describes the precedence of operators, from highest to lowest.

| Operator type          | Individual operators                                 |
| ---------------------- | ---------------------------------------------------- |
| member                 | `. []`                                               |
| call / create instance | `() new`                                             |
| negation/increment     | `! ~ - + ++ -- typeof void delete`                   |
| multiply/divide        | `* / %`                                              |
| addition/subtraction   | `+ -`                                                |
| bitwise shift          | `<< >> >>>`                                          |
| relational             | `< <= > >= in instanceof`                            |
| equality               | `== != === !==`                                      |
| bitwise-and            | `&`                                                  |
| bitwise-xor            | `^`                                                  |
| bitwise-or             | `|`                                                  |
| logical-and            | `&&`                                                 |
| logical-or             | `||`                                                 |
| conditional            | `?:`                                                 |
| assignment             | `= += -= *= /= %= <<= >>= >>>= &= ^= |= &&= ||= ??=` |
| comma                  | `,`                                                  |

When **comparing** a string with a number, JavaScript will convert the string to  a number when doing the comparison. An empty string converts to 0. A non-numeric  string converts to `NaN` which is always `false`.



#### JavaScript Type Conversion

##### Data Types in JavaScript

* Primitive values
  * Boolean
  * Null
  * Undefined
  * Number
  * BigInt
  * String
  * Symbol
* Objects
  * Function
  * Array
  * Date
  * null



##### [Type Conversion Cheatsheet](https://www.w3schools.com/js/js_type_conversion.asp)

|  Original Value  | Converted to Number | Converted to String | Converted to Boolean |
| :--------------: | :-----------------: | :-----------------: | :------------------: |
|      false       |          0          |       "false"       |        false         |
|       true       |          1          |       "true"        |         true         |
|        0         |          0          |         "0"         |        false         |
|        1         |          1          |         "1"         |         true         |
|       "0"        |          0          |         "0"         |         true         |
|      "000"       |          0          |        "000"        |         true         |
|       "1"        |          1          |         "1"         |         true         |
|       NaN        |         NaN         |        "NaN"        |        false         |
|     Infinity     |      Infinity       |     "Infinity"      |         true         |
|    -Infinity     |      -Infinity      |     "-Infinity"     |         true         |
|        ""        |          0          |         ""          |        false         |
|       "20"       |         20          |        "20"         |         true         |
|     "twenty"     |         NaN         |      "twenty"       |         true         |
|       [ ]        |          0          |         ""          |         true         |
|       [20]       |         20          |        "20"         |         true         |
|     [10,20]      |         NaN         |       "10,20"       |         true         |
|    ["twenty"]    |         NaN         |      "twenty"       |         true         |
| ["ten","twenty"] |         NaN         |    "ten,twenty"     |         true         |
|   function(){}   |         NaN         |   "function(){}"    |         true         |
|       { }        |         NaN         |  "[object Object]"  |         true         |
|       null       |          0          |       "null"        |        false         |
|    undefined     |         NaN         |     "undefined"     |        false         |



##### Implicit Type Casting Rules in JS































