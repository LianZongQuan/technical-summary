## 一、 React  Hooks 

  在 react 中组件的实现方式有两种：函数式组件、class 组件。class 组件中可以使用 state 、props 来更新状态和传递属性，使用 `componentDidMount()` 函数来初始化组件。如何在函数式组件中使用这些特性，需要使用React  Hooks（钩子）。

###   1、Hooks（钩子）概述

​	在 React 16.8 版中添加了 Hooks（钩子） 。Hooks 允许功能组件访问状态和其他特性。因此，通常不再需要 ~~**类组件**~~。

​	需要注意：

- 使用 Hooks 需要从 React 中导入，如 `import React, { useState } from "react";`

- Hooks 只能在 React 函数组件内部调用。

- Hooks 只能在组件的顶层调用。不要在循环语句、条件语句或者嵌套函数中声明 hooks

  ```js
  import React, { useState } from "react";//按需引用 Hooks
  import ReactDOM from "react-dom";
  function App() {
    /*
    	Hooks 需再此调用，是为了可以确保在每次呈现组件时以相同的顺序调用hook。这使得React能够在	
      多个useState和useEffect调用之间正确保存hook的状态。
    */
    const [color, setColor] = useState("red");
  
    return (
      <div>
        <h2>My favorite color is {color}!</h2>
      </div>
    );
  }
  ReactDOM.render(<App/>, document.getElementById('root'));
  ```

- Hooks 不能是有条件的，即不能使用如下语句

  ```js
  if (name !== '') {  //不能使用判断条件来使用 Hooks
    useEffect(function persistForm() {
      localStorage.setItem('formData', name) 
    });
  }
  ```

- Hooks 在 React 类组件中不起作用。

###   2、useState

​	`useState`  允许我们跟踪功能组件中的状态。状态通常是指需要在应用程序中跟踪的数据或属性。

​	`useState`  可以类比于 class 组件中的 `state`

- 实例

  `const [color, setColor] = useState("red");`

  第一个值，`color` 颜色，是我们当前的状态。

  第二个值 `setColor`, 是用于更新状态的函数

  将初始状态设置为 ”red“

  ```js
  import { useState } from "react";
  import ReactDOM from "react-dom";
  function FavoriteColor() {
      /*
      类比 class 组件：
      state = {
        color:"red",
      }
      color 是元素、而 "red" 则是赋给此元素的初始值
    */
    const [color, setColor] = useState("red");
    return(
      <div>
        <h2>
          My favorite color is {color}!
        </h2>
  	  /*
  	  	setColor("blue")
  	  	类比 class 组件：
  		this.setState({color:"blue"})
  	*/
        <button
          type="button"
          onClick={() => setColor("blue")}
        >Blue</button>
      </div>
    )
  }
  ReactDOM.render(<FavoriteColor/>, document.getElementById('root'));
  ```

- 作用

  `useState` 钩子可以用来跟踪字符串、数字、布尔值、数组、对象以及它们的任意组合

  - 创建多个状态来跟踪单个值：

    ```js
      const [brand, setBrand] = useState("Ford");
      const [model, setModel] = useState("Mustang");
      const [year, setYear] = useState("1964");
      const [color, setColor] = useState("red");
    ```

  - 可以只使用一个状态并包含一个对象！

    ```js
    import { useState } from "react";
    import ReactDOM from "react-dom";
      /*
      可以类比 state：
      state = {
      	brand: "Ford",
        model: "Mustang",
        year: "1964",
        color: "red"
      }
      取值则用 . 如 car.brand
    */
    function Car() {
      const [car, setCar] = useState({
        brand: "Ford",
        model: "Mustang",
        year: "1964",
        color: "red"
      });
      return (
        <>
          <h1>My {car.brand}</h1>
          <p>
            It is a {car.color} {car.model} from {car.year}.
          </p>
        </>
      )
    }
    ReactDOM.render(<Car />, document.getElementById('root'));
    ```

- 更新对象和数组的状态：

  若要更改跟踪对象的某一个属性，使用`setxxx( , )`则会删除其它属性

  应该使用`previousState`来更改

  ```js
  setCar(previousState => {
        return { ...previousState, color: "blue" }
      });
  ```

  例：

  ```js
  import { useState } from "react";
  import ReactDOM from "react-dom";
  function Car() {
    const [car, setCar] = useState({
      brand: "Ford",
      model: "Mustang",
      year: "1964",
      color: "red"
    });
    const updateColor = () => {
      //----
      setCar(previousState => {
        return { ...previousState, color: "blue" }
      });
      //----
    }
    return (
      <>
        <h1>My {car.brand}</h1>
        <p>
          It is a {car.color} {car.model} from {car.year}.
        </p>
        <button
          type="button"
          onClick={updateColor}
        >Blue</button>
      </>
    )
  }
  ReactDOM.render(<Car />, document.getElementById('root'));
  ```

  

- 

- 

- 
