

# 权衡的艺术

::: tip Vue.js

- 性能与可维护性之间的取舍
- 运行时与编译时之间的取舍

::: 

## 命令式与声明式

视图层框架的范式通常分为**命令式**与**声明式**

- 命令式：关注过程，比如原生js的 DOM 操作、jQuery，按步操作

  ```js
  const div = document.querySelector("#app"); // 获取div
  div.innerText = 'hello world';  // 设置文本内容
  dic.addEventListener('click', () => alert('ok'));  // 绑定点击事件
  ```

- 声明式：关注结果，比如Vuejs，用户需要的最终视图结果

  ```html
  <div @click="() => alert('ok')">hello world</div>
  ```

🔥 Vue.js帮助我们封装了过程，它的内部实现一定是命令式的，但是暴露给用户的却更加声明式

## 性能与可维护性的权衡

::: tip 声明式代码的性能不优于命令式代码的性能

- 命令式代码的更新性能消耗：A
- 声明式代码的更新性能消耗：A + B

A: 直接修改的性能消耗；B: 找出差异的性能消耗

:::

🔥 虽然声明式代码的性能无法超越命令式代码，但是声明式代码具有更好的可维护性，无需用户参与整个过程的，只需要关心结果的视图。因此，在保持可维护性的同时让性能损失最小化。

## 虚拟DOM的性能

🔖 声明式代码的关键在于，如果我们能**最小化**找出差异的性能消耗，就可以让声明式代码的性能无限接近于命令式代码。虽然这很难，但是这也正是虚拟 DOM 想要解决的问题。

### 创建页面

innerHTML于虚拟DOM在创建页面时的性能：

|                  | 虚拟DOM         | innerHTML       |
| ---------------- | --------------- | --------------- |
| 纯JavaScript运算 | 创建VNode       | 渲染HTML字符串  |
| DOM运算          | 新建所有DOM元素 | 新建所有DOM元素 |

新建页面时，innerHTML和虚拟DOM性能差距不大，都是在新建DOM

### 更新页面

innerHTML于虚拟DOM在更新页面时的性能：

|                  | 虚拟DOM          | innerHTML                     |
| ---------------- | ---------------- | ----------------------------- |
| 纯JavaScript运算 | 创建VNode + Diff | 渲染HTML字符串                |
| DOM运算          | 必要的DOM更新    | 销毁所有旧DOM + 创建所有新DOM |
| 性能因素         | 与数据变化量有关 | 与模板大小有关                |

虚拟 DOM 只更新必要的 DOM，和页面大小无关；innerHTML 性能差的原因：在更新页面时，需要销毁所有旧 DOM，重新创建新 DOM，页面越大，性能越差

### 对比总结

| innerHTML    | 虚拟 DOM   | 原生       |
| ------------ | ---------- | ---------- |
| 性能差       | 性能不错   | 性能高     |
|              | 可维护性强 | 可维护性差 |
| 心智负担中等 | 心智负担小 | 心智负担大 |

## 运行时和编译时

### 运行时

代码直接可以运行，没有编译的过程。缺点是不能分析提供的代码内容，进行对应的性能优化操作

```js
function Render(obj, root) {
    const el = document.createElement(obj.tag)
    if(typeof obj.children === 'string') {
        const text = document.createTextNode(obj.children)
        el.appendChild(text)
    }else if(obj.children) {
        obj.children.forEach(child=> Render(child, el))
    }
    root.appendChild(el)
}

const obj = {
    tag: 'div',
    children: [
        { tag: 'span', children: 'hello world' }
    ]
}

Render(obj, document.body)
```

### 编译时

将代码进行分析转换为可执行的代码，可以分析用户内容。缺点是灵活性较差，必须编译后使用

```html
<div>
    <span>hello world</span>
</div>
```

如果是运行时+编译时，compiler将代码编译成：

```js
const obj = {
    tag: 'div',
    children: [
        { tag: 'span', children: 'hello world' }
    ]
}
// compiler + render
```

当然，也可以实现为纯编译时，compiler直接编译为：

```js
const div = document.createElement('div')
const span = document.createElement('span')
span.innerText = "hello world"
div.appendChild(span)
```

🔥 Vue.js 是运行时 + 编译时架构，保证灵活性的基础上，通过分析，尽可能提升性能。编译器提供了代码提前分析的可能，Vue.js 使用编译器分析出动态数据，让渲染器在更新时能快速区分定位，相辅相成。
