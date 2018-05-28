# 编写可以维护的JS(二)

1.2 命名
命名分变量、常量、函数、构造函数四类：其中变量和函数使用小驼峰命名法（首字母小写），构造函数使用大驼峰命名法（首字母大写），常量使用全大写并用下划线分割单词。
let myAge; // 变量：小驼峰命名
const PAGE_SIZE; // 常量：全大写，用下划线分割单词

function getAge() {} // 普通函数：小驼峰命名
function Person() {} // 构造函数：大驼峰命名
为了区分变量和函数，变量命名应该以名字作为前缀，而函数名前缀应当是动词（构造函数的命名通常是名词）。看如下例子：
```
    let count = 10; // Good
    let getCount = 10; // Bad, look like function

    function getName() {} // Good
    function theName() {} // Bad, look like variable
```

命名不仅是一门科学，更是一门技术，但通常来讲，命名长度应该尽可能短，并抓住要点。尽量在变量名中体现出值的数据类型。比如，命名count、length和size表明数据类型是数字，而命名name、title和message表明数据类型是字符串。但用单个字符命名的变量诸如i、j和k通常在循环中使用。使用这些能够体现出数据类型的命名，可以让你的代码容易被别人和自己读懂。
要避免使用没有意义的命名，如：foo、bar和tmp。对于函数和方法命名来说，第一个单词应该是动词，这里有一些使用动词常见的约定：



动词
含义




can
函数返回一个布尔值


has
函数返回一个布尔值


is
函数返回一个布尔值


get
函数返回一个非布尔值


set
函数用来保存一个值



1.3 直接量
JS中包含一些类型的原始值：字符串、数字、布尔值、null和undefined。同样也包含对象直接量和数组直接量。这其中，只有布尔值是自解释（self-explanatory）的，其他的类型或多或少都需要思考一下它们如何才能更精确地表示出来。
关于字符串：字符串可以用双引号也可以用单引号，不同的JS规范推荐都不同， 但切记不可在一个项目中混用单引号和双引号。
关于数字：记住两点建议：第一，为了避免歧义，请不要省略小数点之前或之后的数字；第二，大多数开发者对八进制格式并不熟悉，也很少用到，所以最好的做法是在代码中禁止八进制直接量。
    // 不推荐的小数写法：没有小数部分
    let price = 10.;

    // 不推荐的小数写法：没有整数部分
    let price = .1;

// 不推荐的写法：八进制写法已经被弃用了
let num = 010;
关于null：null是一个特殊值，但我们常常误解它，将它和undefined搞混。在下列场景中应当使用null。

用来初始化一个变量，这个变量可能赋值为一个对象。
用来和一个已经初始化的变量比较，这个变量可以是也可以不是一个对象。
当函数的参数期望是对象时，用作参数传入。
当函数的返回值期望是对象时，用作返回值传出。

还有下面一些场景不应当使用null。

    不要使用null来检测是否传入了某个参数。
    不要用null来检测一个未初始化的变量。

理解null最好的方式是将它当做对象的占位符（placeholder）。这个规则在所有的主流编程规范中都没有提及，但对于全局可维护性来说至关重要。
关于undefined：undefined是一个特殊值，我们常常将它和null搞混。其中一个让人颇感困惑之处在于null == undefined结果是true。然而，这两个值的用途却各不相同。那些没有被初始化的变量都有一个初始值，即undefined，表示这个变量等待被赋值。比如：
    let person; // 不好的写法
    console.log(person === undefined); // true
尽管这段代码能正常工作，但我建议避免在代码中使用undefined。这个值常常和返回"undefined"的typeof运算符混淆。事实上，typeof的行为也很让人费解，因为不管是值是undefined的变量还是未声明的变量，typeof运算结果都是"undefined"。比如：
```
    // foo未被声明
    let person;
    console.log(typeof person); // "undefined"
    console.log(typeof foo); // "undefined"
```

这段代码中，person和foo都会导致typeof返回"undefined"，哪怕person和foo在其他场景中的行为有天壤之别(在语句中使用foo会报错，而使用person则不会报错)。
通过禁止使用特殊值undefined，可以有效地确保只在一种情况下typeof才会返回"undefined"：当变量为声明时。如果你使用了一个可能(或者可能不会)赋值为一个对象的变量时，则将其赋值为null。
```
    // 好的做法
    let person = null;
    console.log(person === null); // true
```
将变量初始值赋值为null表明了这个变量的意图，它最终很可能赋值为对象。typeof运算符运算null的类型时返回"object"， 这样就可以和undefined区分开了。
关于对象直接量和数组直接量: 请直接使用直接量语法来创建对象和数组，避免使用Object和Array构造函数来创建对象和数组。

#### date 2018.5.28
