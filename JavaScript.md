# 鲸准·洞见 JS开发规范
===========================

1，不要对数组进行 for-in 操作
2，如果使用for-in对对象操作的时候，需要使用hasOwnProperty
3，switch-case中必须使用default处理，记住要break。
4，switch-case中，case关键字与switch在统一缩进，case内代码需要缩进
5，每一行都要有；
6，缩进采用2个空格
7，使用===或者!==进行比较判断
8，不允许在for循环中通过length作为判断条件。在for循环开始将数组长度取出来付给一个临时变量。读取length会造成反复长度计算。尤其是遍历dom数组。
9，原生for操作的性能是最高的，无论是时间还是空间。
10，禁止使用匿名函数，这会造成代码难以跟踪。如果使用了async/await，需要配合try-catch使用。
11，所有函数内的局部变量要在函数最开始的地方进行声明，并赋予初始值。
12，禁止全局变量，如果有全局变量需求，请使用Vuex
13，尽可能使用字符串模版`${var}xxx`来替代字符串拼接
14，变量名，函数名采用小驼峰法。常量名全大写字母，绝对禁止拼音命名法。类名，首字母大写。
15，常量使用const，局部变量请使用let。
16，变量，参数需要提供默认值
17，类的私有属性，请使用下划线 ‘_’ 开头
18，类型检测
  - String: `typeof object === 'string'`
  - Number: `typeof object === 'number'`
  - Boolean: `typeof object === 'boolean'`
  - Object: `typeof object === 'object'` // 警惕 array和null
  - null: `object === null`
  - undefined: `object === undefined` or for globals `typeof window.someGlobal === 'undefined'`
19，超级链接必须提供href属性。
20，vue文件首字母大写，js文件采用全部小写字母并用下划线 '_' 来分割单词。
21，文件夹名全小写，使用中划线‘-’分割单词。
22，对于未使用的变量必须删除
23，if，for必须使用 大括号{},且 { 必须 与 if，for在同一行，避免出错。
24，在js关键字和符号之间要加一个空格以增加可读性，比如if () { let a = 1; }
25，逗号之后要加一个空格。逗号之前不要加空格
26，