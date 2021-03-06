# JS正则匹配
#### ^ . * $ ? + |
    ^:代表以跟在^后面的字符为开头（^b以b为开头）
    .:代表任意字符
    *:代表字符出现零次或多次
    $:代表结尾字符（3$以3结尾）
    ?:非贪婪匹配模式
    +:字符至少出现一次
    |:或者的意思（（n | m）匹配n或m正则表达式）

#### { }
    {n}:出现n次
    {n,}:出现>= n次
    {n.m}:出现>=n and <=m次

#### [ ]
    [abcd]:代表要匹配[ ]内的字符
    [0-9]:代表区间
    [^1]:代表不出现1这个字符

#### \s \S \w \W \d
    \s:代表空格
    \S:只要不是空格都可以匹配
    \w:等同于[a-zA-Z0-9]
    \W:与\w相反
    \d:代表数字类型

#### [\u4E00-\u9FA5]
    [\u4E00-\u9FA5]:代表汉字的Unicode编码区间

ECAMScript通过RegExp类型来支持正则表达式。使用下面的语法来创建一个正则表达式
> var expression = / pattern / flages ;

其中的模式（pattern）部分可以是任何简单或复杂的正则表达式。每个正则表达式可以带有一或多个标志（flags），用以标明正则表达式的行为。
正则表达式的匹配模式支持下列3个标志：
- g: 表示全局（global）模式，即模式将被应用于所有字符串，而非在发现第一个匹配项时立即停止；
- i: 表示不区分大小写（case-insensitive）模式，即在确定匹配项时忽略模式与字符串的大小写；
- m: 表示多行（multiline）模式，即在到达一行文本末尾时还有继续查找下一行中是否存在与模式匹配的项。

我们可以通过两种方式来创建。
- 字面量（例如：var pattern=/[bc]at/i）
- RegExp函数（例如：var pattern = new RegExp("[bc]at", "i")）

RegExp对象的主要方法是exec()，该方法是专门为捕获组而设计的。
exec()接受一个参数，即要应用模式的字符串，然后返回包含第一个匹配项信息的数组；或者在没有匹配项的情况下返回null。
返回的数组虽然是Array的实例，但包含两个额外的属性：index 和 input。
> index 表示匹配项在字符串中的位置，而input表示应用正则表达式的字符串。
在数组中，第一项是与整个模式匹配的字符串，其他项是与模式中的捕获组匹配的字符串。
```
var text = "mom and dad and baby";
var pattern = /mom( and dad ( and baby)?)?/gi;

var matches = pattern.exec(text);
alert(matches.index); // 0 
alert(matches.input); // "mom and dad and baby" 
alert(matches[0]); // "mom and dad and baby" 
alert(matches[1]); // " and dad and baby" 
alert(matches[2]); // " and baby" 
```

正则表达式的第二个方法是test()，它接受一个字符串参数。在模式与该参数匹配的情况下返回true；否则返回false。