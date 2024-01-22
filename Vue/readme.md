Vue.js学习记录
# 开始
[前端最新Vue2+Vue3基础入门到实战项目全套教程，自学前端vue](https://www.bilibili.com/video/BV1HV4y1a7n4/?p=4&share_source=copy_web&vd_source=95cd608da1e2c1b445ff2d5f43dbdd5a)

## 通过引入`scrpit`标签，创建一个vue实例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>vue实例</title>
</head>

<body>
    <div id="app">
        <h1>{{msg}}</h1>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                msg: 'hello vue2'
            }
        })
    </script>
</body>
</html>
```
el 是指定挂载点，通过选择器指定DOM盒子，data提供渲染视图层数据。  

## 模板语法
插值表达式： `{{msg}}`  


## Vue指令
- v-html： 设置元素的innerHTML
- v-bind： 绑定属性
- v-model： 双向数据绑定
- v-on： 绑定事件
- v-if： 条件渲染
- v-for： 循环渲染
- v-show： 显示隐藏
- v-slot： 组件插槽
- v-text： 设置元素的innerText
- v-once： 只渲染一次
- v-pre： 保留标签不编译
- v-cloak： 隐藏元素
- v-ref： 注册组件实例


## 案例：小黑记事本
功能： 列表渲染、删除功能、添加功能、统计和清空功能。  
```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>案例：小黑记事本</title>
    <style>
        * {
            margin: 0px;
            padding: 0px;
            /* background-color: #eee; */
        }

        #app {
            background-color: #dad8d8;
            width: 100%;
            height: 100vh;
        }

        .title {
            color: #e76d6d;
            text-align: center;
            margin-top: 30px;
            margin-bottom: 20px;
        }

        .container {
            width: 20%;
            margin: 0 auto;
            background-color: #eee;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 20px;
            box-shadow: 0 0 10px #ccc;
        }

        .input {
            display: flex;
            justify-content: center;
            align-items: center;
            background: #eee;
        }

        .new-todo {
            width: 350px;
            outline: none;
            border: 2px solid #e76d6d;
            border-radius: 5px 0px 0px 5px;
            height: 30px;
            padding-left: 5px;
            background: #eee;
        }

        .add-todo {
            outline: none;
            border: none;
            border-radius: 0px 5px 5px 0px;
            cursor: pointer;
            color: white;
            background: #e76d6d;
            height: 34px;
            padding: 5px;
        }

        .content {
            margin-top: 10px;
            width: 400px;
            font-size: 20px;
        }

        .todo-list {
            list-style: none;
        }

        .todo-item {
            border-bottom: 1px solid #dad8d8;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .todo-item button {
            border: none;
            cursor: pointer;
            color: rgb(207, 51, 51);
        }

        .footer {
            width: 350px;
            margin-top: 5px;
            font-size: 14px;
            color: #a5a2a2;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .clear-todo {
            border: none;
            cursor: pointer;
            color: #a5a2a2;
        }
    </style>
</head>

<body>
    <div id="app">
        <div class="title">
            <h1>TodoList</h1>
        </div>
        <div class="container">
            <div class="input">
                <input type="text" class="new-todo" placeholder="输入任务" v-model="newTodo" @keyup.enter="addTodo">
                <button class="add-todo" @click="addTodo">添加任务</button>
            </div>
            <div class="content">
                <ul class="todo-list">
                    <li class="todo-item" v-for="(item,index) in list" :key="index">
                        <div class="item">
                            <span class="index">{{index+1}}.</span>
                            <span class="text">{{item.text}}</span>
                        </div>
                        <button @click="delTodo(item.id)">x</button>
                    </li>
                </ul>
            </div>
            <div class="footer">
                <span>合计：<strong>{{total}}</strong></span>
                <button class="clear-todo" @click="clear">清空任务</button>
            </div>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                list: [
                    { "id": 1, "text": "吃饭" },
                    { "id": 2, "text": "睡觉" },
                    { "id": 3, "text": "打豆豆" }
                ],
                newTodo: ''
            },
            computed: {
                total() {
                    return this.list.length;
                }
            },
            methods: {
                addTodo() {
                    if (this.newTodo.trim()) {
                        this.list.push({
                            id: this.list.length + 1,
                            text: this.newTodo
                        })
                        this.newTodo = ''
                    } else {
                        alert('请输入任务')
                    }
                },
                delTodo(id) {
                    this.list = this.list.filter(item => item.id !== id)
                },
                clear() {
                    this.list = []
                }
            }
        })
    </script>
</body>

</html>
```


## v-bind
v-bind对于样式控制的增强  
语法：`:class="对象/数组"`

```
<div class="box" :class="{ 类名1:布尔值,类名2:布尔值 }"></div>
```
语法：`:style="{ 属性名1:属性值1,属性名2:属性值2 }"`
```
<div :style="{ width: '400px', height: '400px', backgroundColor: 'red' }"></div>
```
值得注意的是，由于v-bind绑定了style属性，style里就变成了js对象的形式，所以在css中属性名应该按驼峰命名或是加上引号。  

## v-model
v-model应用表单元素
```html
    <div id="app">
        姓名*：
        <input type="text" v-model.trim="username">
        <br>
        是否单身：
        <input type="checkbox" v-model="isSingle">
        <br>
        性别*：
        <input type="radio" name="gender" value="1" v-model="gender">男
        <input type="radio" name="gender" value="0" v-model="gender">女
        <br>
        所在城市*：
        <select v-model="city">
            <option value="1">成都</option>
            <option value="2">上海</option>
            <option value="3">深圳</option>
        </select>
        <br>
        个人简介*：
        <textarea v-model="desc" cols="30" rows="10"></textarea>
        <br>
        <button @click="submit">提交</button>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                username: '',
                isSingle: false,
                gender: "1",
                city: "1",
                desc: ''
            },
            methods: {
                submit() {
                    if (this.username !== '' && this.desc !== '') {
                        let list = [
                            {
                                "用户名": this.username,
                                "是否单身": this.isSingle ? "是" : "否",
                                "性别": this.gender ? "男" : "女",
                                "城市": this.city == '1' ? "成都" : this.city == '2' ? "上海" : "深圳",
                                "介绍": this.desc
                            }
                        ]
                        console.log(list)
                    } else {
                        alert('请填写完整信息')
                    }
                    this.username = ''
                    this.desc = ''
                }
            }
        })
    </script>
```


## 案例：成绩案例
功能： 列表渲染、删除功能、添加功能、统计总分和求平均分功能。 
```html
<!-- 略...见目录同名文件 -->
```

## watch
watch是监听数据变化，执行一些业务逻辑或异步操作。 
watch的简单写法 
```
watch: {
    'obj.words' (newValue,oldValue) {
        console.log('变化了',newValue,oldValue)
    }
}
```


## vue生命周期
一个vue实例从创建到销毁的整个过程。  

生命周期四个阶段：
1. 创建阶段：
响应式数据
2. 挂载阶段：
渲染模板
3. 更新阶段：
数据更新
4. 销毁阶段：
销毁实例

生命周期钩子：

### 案例：小黑记账清单
源代码见目录同名文件  
具体实现：
1. 渲染DOM  
在methods方法中封装 `getList()` 方法，方便调用  
通过异步 `axios` 请求API接口获取数据  
在`created`钩子函数中回调该方法
2. 添加功能  
收集表单数据 `v-model`  
给添加按钮绑定点击事件 `@click`  
通过异步 `axios` 请求API接口添加数据  
回调`getList()`方法，重新渲染添加后的数据
3. 删除功能  
给删除按钮绑定点击事件 `@click(item.id)` ，并传参循环渲染`v-for`中的当前项的 `id`  
根据传参`id`请求API接口删除数据  
4. 饼图渲染  
通过`Echarts`插件根据获取到的数据动态渲染饼图  
将`echarts.setOption({...})`方法挂载到`mounted`钩子函数上，并在 `getList()` 方法中配置`setOption()` `data`数据，实现数据实时变化动态渲染饼图。

## 工程化开发
基于脚手架webpack开发前端项目。  
组件化项目  

[vue2组件化实现todolist](https://github.com/shiori2024/todolist)
通过组件间通信的方式，使子组件能够通过 `props` 得到数据，子组件要修改数据通过 `$emit` 传回给父组件。而根据这种特点，兄弟组件间可以使用共同的父组件数据。  

### 两种组件关系，对应的组件通信
父子关系 -> `props` 和 `$emit`  
非父子关系 -> `provide` 和 `inject` 或 `eventbus`  
通用方案 -> vuex 或 pinia  
