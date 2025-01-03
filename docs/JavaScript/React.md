# React 使用指南：从入门到实践

React 是一个由 Facebook 开发的开源 JavaScript 库，用于构建用户界面，尤其是单页应用（SPA）。它以组件化、声明式编程和高效的虚拟 DOM 渲染机制而闻名。本文将带你快速入门 React，并通过代码示例展示其核心特性。

---

## 1. 环境准备

在开始之前，你需要确保本地已经安装了 Node.js 和 npm。可以通过以下命令检查是否已安装：

```bash
node -v
npm -v
```

如果未安装，可以从 [Node.js 官方网站](https://nodejs.org/) 下载并安装。

---

## 2. 创建 React 应用

使用 `create-react-app` 工具可以快速创建一个新的 React 项目：

```bash
npx create-react-app my-app
cd my-app
npm start
```

运行 `npm start` 后，浏览器会自动打开 `http://localhost:3000/`，你将看到一个默认的 React 欢迎页面。

---

## 3. React 组件

React 的核心思想是组件化。组件是构建用户界面的基本单元，可以是函数组件或类组件。

### 3.1 函数组件

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Alice" />
      <Welcome name="Bob" />
    </div>
  );
}

export default App;
```

### 3.2 类组件

```jsx
import React, { Component } from 'react';

class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}

class App extends Component {
  render() {
    return (
      <div>
        <Welcome name="Alice" />
        <Welcome name="Bob" />
      </div>
    );
  }
}

export default App;
```

---

## 4. JSX 语法

JSX 是 JavaScript 的语法扩展，允许在 JavaScript 代码中编写类似 HTML 的标记。

```jsx
const element = <h1>Hello, World!</h1>;
```

JSX 表达式可以嵌入 JavaScript 代码：

```jsx
const name = "React";
const element = <h1>Hello, {name}!</h1>;
```

---

## 5. 状态与生命周期

### 5.1 使用 `useState` 钩子

函数组件可以通过 `useState` 钩子管理状态。

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

export default Counter;
```

### 5.2 类组件的状态与生命周期

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  componentDidMount() {
    console.log("Component mounted");
  }

  componentDidUpdate() {
    console.log("Component updated");
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}

export default Counter;
```

---

## 6. 事件处理

React 事件处理与 DOM 事件类似，但使用驼峰命名法。

```jsx
function Button() {
  function handleClick() {
    alert("Button clicked!");
  }

  return <button onClick={handleClick}>Click me</button>;
}

export default Button;
```

---

## 7. 条件渲染

React 支持通过条件语句或三元运算符进行条件渲染。

```jsx
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  return isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please sign up.</h1>;
}

function App() {
  return (
    <div>
      <Greeting isLoggedIn={true} />
    </div>
  );
}

export default App;
```

---

## 8. 列表与键

使用 `map` 函数可以渲染列表，每个元素需要唯一的 `key` 属性。

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) => (
    <li key={number.toString()}>{number}</li>
  ));
  return <ul>{listItems}</ul>;
}

function App() {
  const numbers = [1, 2, 3, 4, 5];
  return <NumberList numbers={numbers} />;
}

export default App;
```

---

## 9. 表单处理

React 中的表单元素是受控组件，其值由状态管理。

```jsx
import React, { useState } from 'react';

function NameForm() {
  const [name, setName] = useState("");

  function handleSubmit(event) {
    alert("A name was submitted: " + name);
    event.preventDefault();
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={(e) => setName(e.target.value)} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}

export default NameForm;
```

---

## 10. 使用 React Router

React Router 是 React 中常用的路由库，用于实现单页应用的路由功能。

安装 React Router：

```bash
npm install react-router-dom
```

示例代码：

```jsx
import React from 'react';
import { BrowserRouter as Router, Route, Routes, Link } from 'react-router-dom';

function Home() {
  return <h1>Home Page</h1>;
}

function About() {
  return <h1>About Page</h1>;
}

function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Router>
  );
}

export default App;
```

---

## 11. 状态管理：使用 Redux

Redux 是一个流行的状态管理库，适用于复杂的应用状态管理。

安装 Redux：

```bash
npm install @reduxjs/toolkit react-redux
```

示例代码：

```jsx
import React from 'react';
import { createSlice, configureStore } from '@reduxjs/toolkit';
import { Provider, useSelector, useDispatch } from 'react-redux';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
  },
});

const store = configureStore({
  reducer: counterSlice.reducer,
});

function Counter() {
  const count = useSelector((state) => state.value);
  const dispatch = useDispatch();

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => dispatch(counterSlice.actions.increment())}>+</button>
      <button onClick={() => dispatch(counterSlice.actions.decrement())}>-</button>
    </div>
  );
}

function App() {
  return (
    <Provider store={store}>
      <Counter />
    </Provider>
  );
}

export default App;
```

---

## 12. 总结

React 是一个强大且灵活的库，适用于构建现代 Web 应用。通过本文的介绍，你应该已经掌握了 React 的基础知识，并能够编写简单的组件和应用。接下来，你可以继续深入学习 React 的高级特性，如 Context API、Hooks、性能优化等。

Happy coding! 🚀