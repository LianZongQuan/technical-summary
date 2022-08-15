## 1.弹窗自动弹出问题

使用bind

.bind(event,data)

event :执行的方法，

data：数据

在React Native中bind方法的作用是为指定的事件添加相应的处理函数。就是将处理函数和指定的操作绑定在一起。操作触发时函数执行。

例子：

reload的时候就会弹出弹窗

```js
    show(text){
        alert('确认名字为'+text+"?");
      }
     render() {
        return (
           <TouchableOpacity onPress={this.show("Hello")}>
                <Text>
                    按钮
                </Text>

           </TouchableOpacity>
        )
     }
```

使用bind更改后：

```js
    show(text){
        alert('确认名字为'+text+"?");
      }
     render() {
        return (
           <TouchableOpacity onPress={this.show.bind(this,"lian")}>
                <Text>
                    按钮
                </Text>

           </TouchableOpacity>
        )
     }
```

### 2、react-native-safe-area-context组件报错

报错如下：

```js
react-native-safe-area-context:compileDebugKotlin FAILED
```

解决方法：

找到：**android\build.gradle**

将**compileSdkVersion = 30**从29改为30
