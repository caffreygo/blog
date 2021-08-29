

# 正则表达式

## 基础知识

::: tip 正则表达式（Regular expression）是用于匹配字符串中字符组合的模式。

- 正则表达式是在宿主环境下运行的，如`js/php/node.js` 等
- 在 JavaScript中，正则表达式也是对象

:::

### 对比分析

与普通函数操作字符串来比较，正则表达式可以写出更简洁、功能强大的代码。

下面使用获取字符串中的所有数字来比较函数与正则的差异。

```js
let str = "jerrychen2200hello9988";
let nums = [...str].filter(a => !Number.isNaN(parseInt(a))); // 过滤出数字数组
console.log(nums.join(""));  // 22009988
```

使用正则表达式将简单得多

```js
let str = "jerrychen2200hello9988";
console.log(str.match(/\d/g).join("")); // 22009988
```

### 创建正则

📗 JS提供字面量与对象两种方式创建正则表达式

#### 字面量创建

使用`//`包裹的字面量创建方式是推荐的作法，但它不能在其中使用变量

```js
let site = "caffreygo.com";
console.log(/f/.test(site)); // 是否含有f字母：true
```

下面尝试使用 `a` 变量时将不可以查询

```js
let site = "caffreygo.com";
let b = "f";
console.log(/b/.test(str)); // false
```

📌 虽然可以使用 `eval` 转换为js语法来实现将变量解析到正则中，但是比较麻烦

 💡 所以有变量时建议使用下面的对象创建方式

```js
let str = "caffreygo.com";
let a = "u";
console.log(eval(`/${a}/`).test(str)); //true
```

#### 对象创建

当正则需要动态创建时使用对象方法

正则拥有`test`方法测试字符串参数是否匹配

```js
let site = "caffreygo.com";
let name = "caffreygo";
let reg = new RegExp(name); // 接收一个字符串参数
console.log(reg.test(site)); // true
```

💡 根据用户输入高亮显示内容，支持用户输入正则表达式

```html
<body>
  <div id="content">caffreygo.com</div>
</body>
<script>
  const content = prompt("请输入要搜索的内容，支持正则表达式");
  const reg = new RegExp(content, "g");
  let body = document
    .querySelector("#content")
    .innerHTML.replace(reg, str => {
      return `<span style="color:red">${str}</span>`;
    });
  document.body.innerHTML = body;
</script>
```

通过对象创建正则提取标签

```html
<body>
  <h1>caffreygo.com</h1>
  <h1>strcms.com</h1>
</body>

<script>
function element(tag) {
  const html = document.body.innerHTML;
  let reg = new RegExp("<(" + tag + ")>.+</\\1>", "g");
  return html.match(reg);
}
console.table(element("h1"));
```

### 选择符

`|` 这个符号带表**选择修释符**，也就是 `|` 左右两侧有一个匹配到就可以。

**原子组**就是正则表达式中的小括号()及所包括的内容

检测电话是否是上海或北京的坐机

```js
let tel = "010-12345678";

// 错误结果：只匹配 | 左右两边任一结果
console.log(tel.match(/010|020\-\d{7,8}/));
// ["010", index: 0, input: "010-12345678", groups: undefined]

// 正确结果：所以需要放在原子组中使用
console.log(tel.match(/(010|020)\-\d{7,8}/));
// ["010-12345678", "010", index: 0, input: "010-12345678", groups: undefined]
```

匹配字符是否包含`world` 或 `hello`

```js
const str = "hiworld";
console.log(/world|hello/.test(str)); //true
```

### 字符转义

📗 转义用于改变字符的含义，用来对某个字符有多种语义时的处理。

假如有这样的场景，如果我们想通过正则查找`/`符号，但是 `/`在正则中有特殊的意义。如果写成`///`这会造成解析错误，所以要使用转义语法 `/\//`来匹配。

```js
const url = "https://www.caffreygo.com";
console.log(/https:\/\//.test(url)); //true
```

📌 使用 `RegExp` 构建正则时在转义上会有些区别，下面是对象与字面量定义正则时区别

```js
let price = 12.23;
//含义1: . 除换行外任何字符 	含义2: .普通点
//含义1: d 字母d   		    含义2: \d 数字 0~9
console.log(/\d+\.\d+/.test(price));

//字符串中 \d 与 d 是一样的，所以在 new RegExp 时\d 即为 d
console.log("\d" == "d");

//使用对象定义正则时，可以先把字符串打印一样，结果是字面量一样的定义就对了
console.log("\\d+\\.\\d+");   // \d+\.\d+
let reg = new RegExp("\\d+\\.\\d+");
console.log(reg.test(price));
```

下面是网址检测中转义符使用

```js
let url = "https://www.caffreygo.com";
console.log(/https?:\/\/\w+\.\w+\.\w+/.test(url));
```

### 字符边界

📗 使用字符边界符用于控制匹配内容的开始与结束约定。

| 边界符 | 说明                         |
| ------ | ---------------------------- |
| ^      | 匹配字符串的开始             |
| $      | 匹配字符串的结束，忽略换行符 |

匹配内容必须以`www`开始

```js
const str = "www.caffreygo.com";
console.log(/^www/.test(str)); //true
```

匹配内容必须以`.com`结束

```js
const str = "www.caffreygo.com";
console.log(/\.com$/.test(str)); //true
```

检测用户名长度为3~6位，且只能为字母。如果不使用 `^与$` 限制将得不到正确结果

```html
<body>
  <input type="text" name="username" />
</body>

<script>
  document
    .querySelector(`[name="username"]`)
    .addEventListener("keyup", function() {
      let res = this.value.match(/^[a-z]{3,6}$/i);
      console.log(res);
      console.log(res ? "正确" : "失败");
    });
</script>
```

## 元子字符

📗 元字符是正则表达式中的**最小元素**，只代表单一（一个）字符

### 字符列表

| 元字符 | 说明                                                 | 示例          |
| ------ | ---------------------------------------------------- | ------------- |
| \d     | 匹配任意一个数字                                     | [0-9]         |
| \D     | 与除了数字以外的任何一个字符匹配                     | [^0-9]        |
| \w     | 与任意一个英文字母,数字或下划线匹配                  | [a-zA-Z_]     |
| \W     | 除了字母,数字或下划线外与任何字符匹配                | [^a-zA-Z_]    |
| \s     | 任意一个空白字符匹配，如空格，制表符`\t`，换行符`\n` | [\n\f\r\t\v]  |
| \S     | 除了空白符外任意一个字符匹配                         | [^\n\f\r\t\v] |
| .      | 匹配除换行符外的任意字符                             |               |

### 使用体验

匹配任意数字`string.match(regexp)`

```js
let str = "hellowrold 2010";
console.log(str.match(/\d/g)); //["2", "0", "1", "0"]
```

匹配所有电话号码

```js
let str = "张三:010-99999999,李四:020-88888888";

let res = str.match(/\d{3}-\d{7,8}/g);
console.log(res);   // ["010-99999999", "020-88888888"]
```

获取所有用户名

```js
let str = "张三:010-99999999,李四:020-88888888";

let res = str.match(/[^:\d-,]+/g); 
// [^:\d-,]表示匹配除了 : 数字 - , 这些字符之外的部分
console.log(res);
```

匹配任意非数字

```js
console.log(/\D/.test(2029)); //false
```

匹配字母数字下划线

```js
let str = "hello@";
console.log(str.match(/\w/g)); // ["h", "e", "l", "l", "o"]
```

匹配除了字母,数字或下划线外与任何字符匹配

```js
console.log(/\W/.test("@")); //true
```

匹配与任意一个空白字符匹配

```js
console.log(/\s/.test(" ")); //true
console.log(/\s/.test("\n")); //true
```

匹配除了空白符外任意一个字符匹配

```js
let str = "hi123 @";
console.log(str.match(/\S/g)); // ["h", "i", "1", "2", "3", "@"]
```

如果要匹配点则需要转义

```js
let str = `caffreygo@com`;
console.log(/caffreygo.com/i.test(str)); //true
console.log(/houdunren\.com/i.test(str)); //false
```

📗`.`匹配除换行符外任意字符了，下面匹配不到`test.com` 因为有换行符

```js
const url = `https://www.caffreygo.com
  test.com
`;
console.log(url.match(/.+/));
// ["  https://www.caffreygo.com", index: 1, input: "\n  https://www.caffreygo.com\n  test.com\n", groups: undefined]
```

使用`/s`视为单行模式（忽略换行）时，`.` 可以匹配所有

```js
let str = `
  <span>
    hello
    jerry
  </span>
`;
let res = str.match(/<span>.*<\/span>/s);
console.log(res[0]); 
```

正则中空格会按普通字符对待

```js
let tel = `010 - 999999`;
console.log(/\d+-\d+/.test(tel)); // false
console.log(/\d+ - \d+/.test(tel)); // true
```

### 所有字符

可以使用 `[\s\S]` 或 `[\d\D]` 来匹配所有字符

```js
let str = `
  <span>
    houdunren
    strcms
  </span>
`;
let res = str.match(/<span>[\s\S]+<\/span>/);
console.log(res[0]);
```