# 代码规范

## PC端代码规范

### JS规范

- 使用[ES 2016+ 规范](http://kangax.github.io/compat-table/es2016plus/)

- 在ESLint的代码风格检查的基础上增加额外要求：

  - 命名同时还需要关注语义，如：
    - 变量名应当使用名词camel命名
    - boolean类型的应当使用is、has等起头,表示其类型
    - 函数名应当用动宾短语

  - 永远不省略分号
  - 组件文件和组件使用相同的名字，组件名必须避免使用Vue保留标签名（包括HTML标签和Vue内部标签）

### React/JSX 规范

#### 基本

- 原则上每个文件只写一个组件, 多个[无状态组件](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions)可以放在单个文件中. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).

- 推荐使用 JSX 语法编写 React 组件, 而不是 `React.createElement`

#### 命名

**扩展名**: React 组件使用 `.jsx` 扩展名

- **文件名**: 文件名使用帕斯卡命名. 如, `ReservationCard.jsx`
- **引用命名**: React组件名使用帕斯卡命名, 实例使用骆驼式命名. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

- **组件命名**: 组件名与当前文件名一致. 如 `ReservationCard.jsx` 应该包含名为 `ReservationCard`的组件. 如果整个目录是一个组件, 使用 `index.js`作为入口文件, 然后直接使用 `index.js` 或者目录名作为组件的名称
- **属性命名**: 避免使用 DOM 相关的属性来用命名自定义属性

#### 代码缩进

- 遵循 JSX 语法缩进/格式. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

#### 括号

- 将多行 JSX 标签写在 `()`里. eslint: [`react/jsx-wrap-multilines`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-wrap-multilines.md)

#### 标签

- 对于没有子元素的标签, 总是自关闭标签. eslint: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)
- 如果组件有多行的属性, 关闭标签时新建一行. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

#### 函数/方法

- 当在 `render()` 里使用事件处理方法时, 提前在构造函数里把 `this` 绑定上去. eslint: [`react/jsx-no-bind`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-bind.md)
- 在React组件中, 不要给所谓的私有函数添加 `_` 前缀, 本质上它并不是私有的
- 在 `render` 方法中总是确保 `return` 返回值. eslint: [`react/require-render-return`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/require-render-return.md)

#### 生命周期顺序

- `static` 方法（可选）

- `constructor` 构造函数

- `getChildContext` 获取子元素内容

- `componentWillMount` 组件渲染前

- `componentDidMount` 组件渲染后

- `componentWillReceiveProps` 组件将接受新的数据

- `shouldComponentUpdate` 判断组件是否需要重新渲染

- `componentWillUpdate` 上面的方法返回 `true`时, 组件将重新渲染

- `componentDidUpdate` 组件渲染结束

- `componentWillUnmount` 组件将从DOM中清除, 做一些清理任务

- 事件绑定 如 `onClickSubmit()` 或 `onChangeDescription()`

- *render 里的 getter 方法* 如 `getSelectReason()` 或 `getFooterContent()`

- *可选的 render 方法* 如 `renderNavigation()` 或 `renderProfilePicture()`

- `render` render() 方法

## 服务端代码规范

### 命名规范：

* 文件：小写
* 包命名
  * package名和目录保持一致，需避免和标准库冲突
  * 避免import相对路径
* 方法/接口
  * 采用驼峰命名法
  * 非对外方法，首字母需为小写
* 变量：采用驼峰命名法
* 常量：大写+下划线

### 注释

* 注释
  * 可以通过 `/* …… */` 或者 `// ……`增加注释， `//`之后应该加一个空格
  * 注释内容需要在文件/方法/变量上方
* 每一个包都应该有包注释，位于文件的顶部，在包名出现之前。如果一个包有多个文件，包注释只需要出现在一个文件的顶部即可。包注释建议使用C注释风格，如果这个包特别简单，需要的注释很少，也可以选择使用C++注释风格。

### 异常

* 需要对异常做判断处理
* 不要将error赋值给匿名变量_

* 不允许逻辑中调用Panic，选择日志的log.Fatal
* 不要频繁的调用defer
* 尽早return，一旦有错误发生，马上返回

### import

* 当import多个包时，应该对包进行分组。同一组的包之间不需要有空行，不同组之间的包需要一个空行。标准库的包应该放在第一组。



### 其他

* 对于bool类型的变量`var b bool`,直接使用它作为判断条件，而不是使用它和true/false进行比较

byte/string slice相等性比较，使用Equal

* 当接受者是map, chan, func, 不要使用指针传递，因为它们本身就是引用类型
* 当接受者是slice，而函数内部不会对slice进行切片或者重新分配空间，不要使用指针传递
* 当函数内部需要修改接受者，必须使用指针传递
* 当接受者是一个结构体，并且包含了`sync.Mutex`或者类似的用于同步的成员。必须使用指针传递，避免成员拷贝
* 当接受者类型是一个结构体并且很庞大，或者是一个大数组，建议使用指针传递来提高性能，其他场景使用值传递即可

