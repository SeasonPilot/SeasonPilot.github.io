---
layout: post
categories: JavaScript
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
JavaScript 返回值 undefined

Answer:

您好，这是必应。我可以用简体中文回答您的问题。😊

JavaScript 返回值 undefined 的原因有以下几种：

- 访问一个未初始化的变量或对象属性<sup>2</sup> <sup>3</sup>。例如：

```javascript
let name; // 声明了一个变量，但没有赋值
console.log(name); // undefined
console.log(person.age); // undefined，person对象没有age属性
```

- 调用一个没有返回值的函数<sup>2</sup> <sup>3</sup>。例如：

```javascript
function sayHello() {
  console.log("Hello");
}
let result = sayHello(); // 调用函数，但没有return语句
console.log(result); // undefined
```

- 函数的参数没有传递值<sup>2</sup> <sup>3</sup>。例如：

```javascript
function add(a, b) {
  return a + b;
}
let sum = add(1); // 只传递了一个参数，b的值为undefined
console.log(sum); // NaN，因为undefined不能和数字相加
```

- 使用void运算符<sup>2</sup> <sup>3</sup>。例如：

```javascript
let x = void 0; // void运算符返回undefined
console.log(x); // undefined
```

- 使用delete运算符删除一个对象属性或数组元素<sup>2</sup> <sup>3</sup>。例如：

```javascript
let obj = {name: "Alice", age: 20};
delete obj.name; // 删除对象的name属性
console.log(obj.name); // undefined

let arr = [1, 2, 3];
delete arr[1]; // 删除数组的第二个元素
console.log(arr[1]); // undefined
```

如果您想避免返回undefined，您可以：

- 给变量和对象属性赋初始值<sup>1</sup>。例如：

```javascript
let name = ""; // 给变量赋一个空字符串
console.log(name); // ""

let person = {name: "Bob", age: null}; // 给对象属性赋一个null值
console.log(person.age); // null
```

- 在函数中使用return语句返回一个值<sup>1</sup>。例如：

```javascript
function sayHello() {
  console.log("Hello");
  return "Hello"; // 返回一个字符串值
}
let result = sayHello(); 
console.log(result); // "Hello"
```

- 在调用函数时传递所有需要的参数<sup>1</sup>。例如：

```javascript
function add(a, b) {
  return a + b;
}
let sum = add(1, 2); // 传递两个参数，a和b都有值
console.log(sum); // 3
```

- 不要使用void运算符<sup>1</sup>，除非您有特殊的需求。
- 不要使用delete运算符删除对象属性或数组元素<sup>1</sup>，除非您有特殊的需求。

希望这些信息对您有帮助。如果您还有其他问题，请继续提问。😊


\-
\[1]: [undefined - JavaScript | MDN - Mozilla Developer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)
\[2]: [undefined - JavaScript | MDN - Mozilla Developer](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)
\[3]: [https://dmitripavlutin.com/7-tips-to-handle-undefined-in-javascript/#:~:text=The%20short%20answer%20is%20that%20JavaScript%20interpreter%20returns,doesn%E2%80%99t%20initialize%20variables%20or%20object%20properties%20with%20null.](https://bing.com/search?q=JavaScript+%e8%bf%94%e5%9b%9e%e5%80%bc+undefined)
\[4]: [JavaScript编写函数返回值时出现undefined问题 - CSDN博客](https://blog.csdn.net/weixin_43957143/article/details/97148985)

<hr/>

