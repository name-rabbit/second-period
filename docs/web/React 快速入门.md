

# React 快速入门

## 1. 简介

### 1.1 React是什么

`React` 是一个快速创建可交互用户界面的 `Javascript`库（Library）



AngularJS / ReactJs / vueJS / NodeJs / Uni-App / Taro / ElementUl / AntDesign

### 1.2 核心概念

React 的核心是`Component`（组件

从技术实现上，组件是由 Javascript 中的`class`（类）实现的：

```javascript
class NavBar {
  // 保存组件的属性等状态
  state = {};
	// 根据具体的数据，在浏览器中渲染出相应的组件模样	
	render(){ 
    
  }
}
```

## 2. 环境搭建

安装 `NodeJS`

NodeJS官网：[https://nodejs.org/en/](https://nodejs.org/en/)

由于 npm 的官方服务器连接速度较慢，需要配置 npm 的淘宝镜像：

```shell
npm config set registry https://registry.npm.taobao.org
```

## 3. 快速上手

### 3.1 项目初始化

首先使用`npx create-react-app`指令创建一个名为`shopping-cart`的`React`项目

```shell
npx create-react-app shopping-cart
```

插件推荐：

![image-20220813173417712](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220813173417712.png)

### 3.2 Hello world

- node_modules 存放的当前项目所需要用到的所有第三方libs

- 在做完以后交付给别人的时候，一般会删除，然后再拷贝给他人，他人拿到以后，只需要在项目的根目录下输入如下指令即可：

  ​		npm i

- public 存放的静态资源 html css image

- src 存放源码 主要是JS + HTML(XML) -> JSX

找到程序的入口文件`index.js`，注释掉所有代码，编写如下内容： 

```jsx
//imrc快捷方式
import React from 'react';
import ReactDOM from 'react-dom/client';

// 导入外部样式
import './index.css';
import "bootstrap/dist/css/bootstrap.min.css";
// 导入自定义的组件
import App from './components/app';
import reportWebVitals from './reportWebVitals';


// 创建了一个根节点(VM)
const root = ReactDOM.createRoot(document.getElementById('root'));
// 在root渲染出App的子组件
root.render( // 渲染、绘制
  <React.StrictMode>
    {/* 自定义的组件 */}
    <App />
  </React.StrictMode>
);

reportWebVitals();

```

## 4. Component

### 4.1 创建Counter组件

在项目`src`目录下创建`components`文件夹，在其下创建`counter.jsx`文件。

> jsx属于结合`javascript`和`xml`的一门扩展语言，可以让我们直接在`javascript`中操作`html`元素，在项目使用babel编译以后，会转换成传统浏览器能识别的代码。

```jsx
// imrc
import React, { Component } from "react";

// cc
class Counter extends Component {
	// state = {  }
	render() {
		return <h1>Hello</h1>;
	}
}

export default Counter;
```

在`index.js`中导入并使用这个组件：

```jsx
import Counter from "./components/counter";

import reportWebVitals from "./reportWebVitals";

ReactDOM.render(
	<React.StrictMode>
		<Counter />
	</React.StrictMode>,
	document.getElementById("root")
);
```

### 4.2 子元素

在`counter`组件中继续创建其它按钮：

```jsx
class Counter extends Component {
	// state = {  }
	render() {
		return (
			<div>
				<h1>Hello</h1>
				<button>Increment</button>
			</div>
            // <React.Fragment>
			// 	<h1>Hello</h1>
			// 	<button>Increment</button>
			// </React.Fragment>
		);
	}
}
```

在渲染方法中，如果需要创建多个元素，这些元素需要被一个顶层元素（比如`div`）包含起来。

如果不想使用`div`标签的话，可以使用`React.Fragment`标签。



### 4.3 state

`state`是`react`组件中一个特殊的属性，它里面可以定义这个组件所需要用到的所有数据

`{}`是在`jsx`中用来获取值的一种语法，又称胡子（`mustache`）语法，在其中可以使用任意符合`javascript`语法的变量、表达式或者有返回值的函数：

```jsx
//imrc快捷方式
import React, { Component } from 'react';

import SideMenu from './sideMenu';
import Counters from './counters';
import TotalBar from './totalBar';
//cc快捷方式
class MainContent extends Component {

    // 组件的属性
    // react会根据组件的属性值(state)来动态的渲染出页面
    state = {
       
        // 数据源
        counters: [
            { id: 0, count: 0, decrement: "-", increment: "+" }, // counter0
            { id: 1, count: 1, decrement: "-", increment: "+" }, // counter1
            { id: 2, count: 2, decrement: "-", increment: "+" }, // counter2
        ]
    }

    // 组件的方法（入口方法）使用了bootstrap框架 col栅栏格 m->margin p->padding
    render() {
        return (
            <div className='row m-2'>
                <div className="col-2"><SideMenu /></div>
                <div className="col-10">
                    <TotalBar counters={this.state.counters} />
                    <Counters
                        counters={this.state.counters}
                        //react调用方法不带括号，如果要带括号进行传参必须使用箭头函数
                        //父组件向子组件传值如下，而子组件接受是this.props.XXX                   
                        formatCount={this.formatCount}
                        handleIncrement={this.handleIncrement}
                        handleDecrement={this.handleDecrement}
                        handleDelete={this.handleDelete}
                    />
                </div>
            </div>
        );
    }
	//动态渲染值：三目运算表达式
    formatCount(val) {
        // console.log(this.state.count);
        return val === 0 ? 'Zero' : val;
    }

    // 处理“+”事件
    // this 要指向当前对象需要使用箭头函数，普通函数不行
    handleIncrement = (id) => {     
        // 直接在state做出修改，react是不会监控到的
        // 1、clone原先state中的数据
        const counters = [...this.state.counters];
        // 2、编写修改逻辑
        counters[id].count++;
        // 3、调用Component父类提供的setState方法
        this.setState({ counters });

    }
	
    // 处理“-”事件
    handleDecrement = (id) => {

        // 1、clone原先state中的数据
        const counters = [...this.state.counters];
        // 2、编写修改逻辑
        if (counters[id].count > 0) counters[id].count--;
        // 3、调用Component父类提供的setState方法
        this.setState({ counters });

    }

    handleDelete = (id) => {
        const counters = [...this.state.counters];
        // 通过id在counters中搜索定位，得到index
        // item就是遍历的每一个元素，index该元素的索引
        const index = counters.findIndex((item) => item.id === id);
        // 通过切片执行删除
        counters.splice(index, 1);

        this.setState({ counters });

    }

}

export default MainContent;
```

### 4.4 安装bootstrap

在`VSCode`的控制台输入如下指令安装`bootstrap`

```shell
npm i bootstrap
```

在`index.js`入口文件中导入样式

```jsx
import "bootstrap/dist/css/bootstrap.css";
```

### 4.5 渲染列表

要渲染一个列表出来，首先需要在状态中定义好相关的数据：

```jsx
state = {
  count: 1,
  tags: ["tag1", "tag2", "tag3"],
};
```

然后在`render`方法中编写循环逻辑：

```jsx
<li key={tag}>{tag}</li>
```

> 这个`key`属性只要保证在列表项这个范围具有唯一性即可，而无需在整个页面上保持唯一。

### 4.7 条件渲染

需求：当`tags`有数据的时候就进行渲染，如果没有，则显示相应提示信息

首先编写条件渲染逻辑，在`Counter`组件中新增方法：

```jsx
renderTags() {
  if (!this.state.tags || this.state.tags.length === 0) return <p>没有tag数据。</p>;
  return (
    <ul>
      {this.state.tags.map((tag) => (
        <li key={tag}>{tag}</li>
      ))}
    </ul>
  );
}
```

然后在render方法中直接进行调用即可：

```jsx
render() {
  return (
    <React.Fragment>
      {/* <img src={this.state.imgUrl} alt="" /> */}
      <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
      <button className="btn btn-secondary btn-sm">Increment</button>
      {this.renderTags()}
    </React.Fragment>
  );
}
```

### 4.8 事件处理

所有的`react`元素都有基于`DOM`事件的属性，这些属性都以`on`作为前缀：

```jsx
<button
  onClick={this.handleIncrement}
  className="btn btn-secondary btn-sm"
  >
```

在`Counter`中添加对应的方法：

```jsx
handleIncrement() {
  console.log("...", this.state.count);
}
```

当我们在测试点击事件的时候，会发现，方法虽然被调用了，但是无法获取到`state`中的属性

### 4.9 绑定事件句柄

我们可以通过绑定`this`来解决这个问题：

```jsx
handleIncrement = () => {
  console.log("...", this.state.count);
};
```

> 箭头函数的特点：它不会重新绑定`this`对象，它们只会继承当前上下文中的`this`，即我们在哪里定义了这个函数，这个函数中的`this`就指向谁。

### 4.10 更新state

> 

### 4.11 传递事件参数

在给事件传递参数的时候，我们再次可以使用箭头函数：

```jsx
<button
  onClick={() => this.handleIncrement(1)}
  className="btn btn-secondary btn-sm"
  >
```

相应的方法为：

```jsx
handleIncrement = (productId) => {
  console.log(productId);
  this.setState({ count: this.state.count + 1 });
};
```

> 练习：
>
> 请使用现有的知识完成此前的`todo`列表案例：
>
> - 展示所有待办事项
> - 点击每一行的删除按钮时，删除对应的这行记录

## 5. 组合Components

每个`react`程序都基本是由组件树组成的，我们可以将组件组合在一起，去构建更复杂的用户 UI 。

### 5.1 创建组合组件

在`components`文件夹中新增组件：

```jsx
import React, { Component } from "react";
import Counter from "./counter";

class Counters extends Component {
	state = {
		counters: [
			{ id: 1, value: 0 },
			{ id: 2, value: 0 },
			{ id: 3, value: 0 },
			{ id: 4, value: 0 },
		],
	};
	render() {
		return (
			<div>
				{this.state.counters.map((counter) => (
					<Counter key={counter.id} />
				))}
			</div>
		);
	}
}

export default Counters;
```

同时，记得将入口文件`index.js`中的`Counter`，修改为`Counters`。

### 5.2 在组合组件之间传递数据

在上述案例中，我们给每一个`Counter`组件设置了一个`key`属性，同理，我们可以给其设置其它属性：若依 renrenfast

```jsx
<Counter key={counter.id} value={counter.value} selected={true} />
```

然后在`Counter`的`render`方法中增加如下调试语句：

```jsx
console.log(this.props);
```

每个`react`组件都有一个叫`props`的属性，它是一个`Javascript`对象，拥有我们向这个组件传递的所有属性。`key`比较特殊，它不会成为`props`属性的一员，它是`React`自用的。

基于上述机制，`Counter`可以修改为：

```jsx
import React, { Component } from "react";

class Counter extends Component {
	state = {
		value: this.props.value,
	};

	handleIncrement = () => {
		this.setState({ value: this.state.value + 1 });
	};

	render() {
		return (
			<div>
				<span className={this.getBadgeClasses()}>{this.formatCount()}</span>
				<button
					onClick={this.handleIncrement}
					className="btn btn-secondary btn-sm"
				>
					Increment
				</button>
			</div>
		);
	}

	getBadgeClasses() {
		let classes = "badge m-2 bg-";
		classes += this.state.value === 0 ? "warning" : "primary";
		return classes;
	}

	formatCount() {
		const { value } = this.state;
		return value === 0 ? "Zero" : value;
	}
}

export default Counter;
```

### 5.3 props vs state

- `props`就是我们给组件传递的数据，它是组件的输入数据，我们在组件内部不能修改，只能读取。
- `state`是组件局部或者私有的数据容器，其它组件是不能访问这个组件的状态的，它完全只能在组件内部被访问。

### 5.4 发起与处理事件

给`Counter`组件添加删除按钮：

```jsx
<button
  onClick={this.handleDelete}
  className="btn btn-danger btn-sm m-2"
  >
  Delete
</button>
```

新增删除逻辑：

```jsx
handleDelete = () => {};
```

分析问题：

每个组件都有自己的状态，只有自己能编辑自己的状态。因此，当执行删除某一个`Counter`操作的时候，需要删除`Counters`组件`state`中`counters`数组中对应的元素，而这个操作只应当由`Counters`组件自己来完成。

解决办法：

由`Counter`组件发起一个删除事件，然后在`Counters`组件中执行具体的删除逻辑

![image-20210523004341450](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20210523004341450.png)

在`Counters`中新增删除逻辑：

```jsx
	handleDelete = (counterId) => {
		
	};
```

通过`props`传递数据：

```jsx
<Counter
  onDelete={this.handleDelete}
  key={counter.id}
  id={counter.id}
  value={counter.value}
  />
```

在`Counter`中发起删除事件：

```jsx
<button
  onClick={() => this.props.onDelete(this.props.id)}
  className="btn btn-danger btn-sm m-2"
  >
```

> 代码优化：简化传参

```jsx
<Counter
  onDelete={this.handleDelete}
  key={counter.id}
  counter={counter}
  />
```

### 5.5 单一数据来源原则

添加重置按钮

在Counters组件中添加相应的重置按钮：

```jsx
<button
  onClick={this.handleReset}
  className="btn btn-primary btn-sm m-2"
  >
  Reset
</button>
```

相应的重置逻辑：

```jsx
handleReset = () => {
  const counters = this.state.counters.map((c) => {
    c.value = 0;
    return c;
  });
  this.setState({ counters });
};
```

当我们点击重置按钮时，会发现程序没有任何重置效果。

原因：

我们的`Counters`组件有一个`counters`数组，而每一个`Counter`组件都有自己的`value`属性，这个`value`没有与`counters`数组中对应的`counter`对象的`value`保持一致。

```jsx
state = {
  value: this.props.counter.value,
};
```

虽然在`Counter`组件中有这样的逻辑，但是这个逻辑只在实例创建的时候执行一次。可以理解为每个`Counter`子组件维护了一个自己的`state`，而重置事件改变的是父组件的`state`。

解决办法：

我们需要删除子组件`Counter`中的`state`，然后建立唯一的数据源。

### 5.6 受控组件

将`Counter`的`state`删除，只使用props来接收组件所需的数据，这种类型的组件为受控组件。

![image-20210523013003269](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20210523013003269.png)

受控组件没有自己的`state`，它所有的数据都来自`props`，之后，在数据需要修改的时候发起事件，这种组件是完全被其父组件控制的。

Counter

```jsx
import React, { Component } from "react";

class Counter extends Component {
	handleIncrement = () => {
		this.setState({ value: this.state.value + 1 });
	};

	render() {
		return (
			<div>
				<span className={this.getBadgeClasses()}>{this.formatCount()}</span>
				<button
					onClick={() => this.props.onIncrement(this.props.counter)}
					className="btn btn-secondary btn-sm"
				>
					Increment
				</button>
				<button
					onClick={() => this.props.onDelete(this.props.counter.id)}
					className="btn btn-danger btn-sm m-2"
				>
					Delete
				</button>
			</div>
		);
	}

	getBadgeClasses() {
		let classes = "badge m-2 bg-";
		classes += this.props.counter.value === 0 ? "warning" : "primary";
		return classes;
	}

	formatCount() {
		const { value } = this.props.counter;
		return value === 0 ? "Zero" : value;
	}
}

export default Counter;
```

Counters

```jsx
import React, { Component } from "react";
import Counter from "./counter";

class Counters extends Component {
	state = {
		counters: [
			{ id: 1, value: 2 },
			{ id: 2, value: 3 },
			{ id: 3, value: 4 },
			{ id: 4, value: 5 },
		],
	};

	handleIncrement = (counter) => {
		const counters = [...this.state.counters];
		const index = counters.indexOf(counter);
		counters[index] = { ...counter };
		counters[index].value++;
		this.setState({ counters });
	};

	handleDelete = (counterId) => {
		const counters = this.state.counters.filter((c) => c.id !== counterId);
		this.setState({ counters });
	};

	handleReset = () => {
		const counters = this.state.counters.map((c) => {
			c.value = 0;
			return c;
		});
		this.setState({ counters });
	};

	render() {
		return (
			<div>
				<button
					onClick={this.handleReset}
					className="btn btn-primary btn-sm m-2"
				>
					Reset
				</button>
				{this.state.counters.map((counter) => (
					<Counter
						onIncrement={this.handleIncrement}
						onDelete={this.handleDelete}
						key={counter.id}
						counter={counter}
					/>
				))}
			</div>
		);
	}
}

export default Counters;
```

### 5.7 多组件同步技术

为了新增导航条，需要调整组件结构为

![image-20210523015421813](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20210523015421813.png)

NavBar

```jsx
import React, { Component } from "react";

class NavBar extends Component {
	render() {
		return (
			<nav className="navbar navbar-light bg-light">
				<div className="container-fluid">
					<a className="navbar-brand" href="#">
						Navbar
					</a>
				</div>
			</nav>
		);
	}
}

export default NavBar;
```

App

```jsx
import "./App.css";
import React, { Component } from "react";
import NavBar from "./components/navBar";
import Counters from "./components/counters";

class App extends Component {
	state = {};
	render() {
		return (
			<React.Fragment>
				<NavBar />
				<div className="container">
					<Counters />
				</div>
			</React.Fragment>
		);
	}
}

export default App;
```

分析问题：

在`NavBar`中需要统计所有的`counters`信息，但是`counters`目前维护在`Counters`组件中，`Narbar`和`Counters`组件是平级关系，而不是上下父子组件关系，因此无法通过`props`传递数据。

解决办法：

将`counters`属性提升到父组件`App`中，形成如下结构：

![image-20210523022123834](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20210523022123834.png)

App

```jsx
import "./App.css";
import React, { Component } from "react";
import NavBar from "./components/navBar";
import Counters from "./components/counters";

class App extends Component {
	state = {
		counters: [
			{ id: 1, value: 2 },
			{ id: 2, value: 3 },
			{ id: 3, value: 4 },
			{ id: 4, value: 5 },
		],
	};

	handleIncrement = (counter) => {
    //...
	};

	handleDelete = (counterId) => {
		//...
	};

	handleReset = () => {
		//...
	};

	render() {
		return (
			<React.Fragment>
				<NavBar />
				<div className="container">
					<Counters
            counters={this.state.counters}
						onReset={this.handleReset}
						onIncrement={this.handleIncrement}
						onDelete={this.handleDelete}
					/>
				</div>
			</React.Fragment>
		);
	}
}

export default App;

```

Counters

```jsx
import React, { Component } from "react";
import Counter from "./counter";

class Counters extends Component {
	render() {
		return (
			<div>
				<button
					onClick={this.props.onReset}
					className="btn btn-primary btn-sm m-2"
				>
					Reset
				</button>
				{this.props.counters.map((counter) => (
					<Counter
						key={counter.id}
						counter={counter}
						onIncrement={this.props.onIncrement}
						onDelete={this.props.onDelete}
					/>
				))}
			</div>
		);
	}
}

export default Counters;
```

在`App`组件中给`NavBar`传递统计参数：

```jsx
<NavBar
  total={this.state.counters.filter((c) => c.value !== 0).length}
  />
```

在`NavBar`中显示结果：

```jsx
<a className="navbar-brand" href="#">
  Navbar{" "}
  <span className="badge rounded-pill bg-secondary">
    {this.props.total}
  </span>
</a>
```

### 5.8 无状态功能组件

对于`NavBar`这种，没有`state`，没有事件句柄，仅有一个`render`方法，在这种情况下，我们可以将该组件转换为无状态功能组件。

```jsx
import React, { Component } from "react";

const NavBar = (props) => {
	return (
		<nav className="navbar navbar-light bg-light">
			<div className="container-fluid">
				<a className="navbar-brand" href="#">
					Navbar{" "}
					<span className="badge rounded-pill bg-secondary">{props.total}</span>
				</a>
			</div>
		</nav>
	);
};

export default NavBar;
```

> 参数析构：可以利用对象的析构技术，从参数中析构出对应的属性

```jsx
const NavBar = ({ total }) => {
	return (
		<nav className="navbar navbar-light bg-light">
			<div className="container-fluid">
				<a className="navbar-brand" href="#">
					Navbar{" "}
					<span className="badge rounded-pill bg-secondary">{total}</span>
				</a>
			</div>
		</nav>
	);
};
```

### 5.9 减少按钮

Counter

```jsx
render() {
  return (
    <div className="row">
      <div className="col-1">
        <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
      </div>
      <div className="col">
        <button
          onClick={() => this.props.onIncrement(this.props.counter)}
          className="btn btn-secondary btn-sm"
          >
          +
        </button>
        <button
          onClick={() => this.props.onDecrement(this.props.counter)}
          className="btn btn-secondary btn-sm m-2"
          disabled={this.props.counter.value === 0 ? "disabled" : ""}
          >
          -
        </button>
        <button
          onClick={() => this.props.onDelete(this.props.counter.id)}
          className="btn btn-danger btn-sm"
          >
          Delete
        </button>
      </div>
    </div>
  );
}
```

Counters

```jsx
<Counter
  key={counter.id}
  counter={counter}
  onIncrement={this.props.onIncrement}
  onDecrement={this.props.onDecrement}
  onDelete={this.props.onDelete}
  />
```

App

```jsx
handleDecrement = (counter) => {
  const counters = [...this.state.counters];
  const index = counters.indexOf(counter);
  counters[index] = { ...counter };
  counters[index].value--;
  this.setState({ counters });
};
```

```jsx
<Counters
  counters={this.state.counters}
  onReset={this.handleReset}
  onIncrement={this.handleIncrement}
  onDecrement={this.handleDecrement}
  onDelete={this.handleDelete}
  />
```

## 6. 项目工作流

### 6.1 需求分析

确定做什么项目，项目中应该包含哪些模块，每个模块需要实现什么样的`UI`（User Interface，用户界面）和功能。产出《需求说明书》、原型（Axure）

### 6.2 设计阶段

技术选型，CTO

产出《概要设计》《详细设计书》 

### 6.3 编码阶段

初中级工程师会一边写代码实现功能，一边给代码配备相应说明书

### 6.4 测试

### 6.5 交付 & 部署

> 3、4、5是把一个大型的项目切割成很多小阶段、小模块，迭代进行的

在交付期间，产出项目的操作手册，并派出相关人员对甲方用户进行培训。

