React和jQuery评估
#####################
:date: 2019-03
:tags: React,jQuery
:authon: Zhang Jie

.. contents::

.. _reactandjquery_rst:



React 核心内容
^^^^^^^^^^^^^^
**组件**

React组件能够像原生的HTML标签一样输出特定的界面元素，并且也能包括一些元素相关逻辑功能的代码。

.. code-block:: javascript

    class MyComponent extends React.Component {
        render() {
            return <p>Hello World!<p>;
        }
    }

**JSX**

React框架中推荐使用的一种写法，是Java+XML的缩写，推荐在React中尽量少使用html标签。这样做的好处就是以一种熟悉的语法来定义HTML元素树，让程序结构更容易被直观化。

.. code-block:: javascript
    
    class MyComponent extends React.Component {
        render() {
            return <p>Today is: {new Date()}</p>;//使用了{} 来显示JS变量
        }
    }

在JSX中还可以使用三元运算符一类的逻辑，让代码看起来更加整洁

.. code-block:: javascript

    class MyComponent extends React.Component {
        render() {
            return <p>Hello {this.props.someVar ?  'World' : 'Kitty'}</p>;
        }
    }

**Props&State**

Props主要用于React组件之间的交互，相当于<a>标签中的href属性，因为使用了Props，React中的数据流是单向的，即数据只能从父组件传向子组件，反过来则不行。在开发过程中不必关心数据是如何处理的，只需要关注什么时候和在哪里获取props以及state即可。


state使用于子组件发生改变时，主要通过setState的方法来修改state

.. code-block:: javascript

    class MyComponent extends React.Component {
        handleClick = (e) => {
            this.setState({clicked: true});
        }
        render() {
            return <a href="#" onClick={this.handleClick}>Click me</a>;
        }
    }

**组件API**

React提供的方法，Props和State就是组件API中的一部分，还有经常使用的constructor，同时还提供了按照特定次序触发的生命周期。
React的生命周期一般会经历三个步骤：

- 装载过程(Mount)：把组件第一次在DOM树中渲染的过程，发生在组件第一次被渲染的时候；
- 更新过程(Update)：当组件被重新渲染的过程，当props或者state被修改的时候；
- 卸载过程(Unmount)：组件从DOM中删除的过程，当React组件要从DOM树上清掉之前调用。

 通过React的生命周期可以从全局观测到组件的各个状态，并做出相应的处理。


**组件类型**


React中的组件类型一般分为两种，容器组件和展示组件，容器组件主要关注数据交互，展示组件则是主要用来展示或隐藏内容。

.. code-block:: javascript

    //presentational component
 
    class CommentList extends React.Component {
        constructor(props) {
            super(props);
        }
 
        render() { 
            return <ul> {this.props.comments.map(renderComment)} </ul>;
        }
 
        renderComment({body, author}) {
            return <li>{body}—{author}</li>;
        }
    }
 
    //container component
 
    class CommentListContainer extends React.Component {
        constructor() {
            super();
            this.state = { comments: [] }
        }
 
        componentDidMount() {
            $.ajax({
                url: "/my-comments.json",
                dataType: 'json',
                success: function(comments) {
                    this.setState({comments: comments});
                }.bind(this)
            });
        }
 
        render() {
            return <CommentList comments={this.state.comments} />;
        }
    }

    
jQuery 核心内容
^^^^^^^^^^^^^^^^^

使用原生的JavaScript操纵方式，以少量的代码去解决问题。

不同点
^^^^^^

从本质上来说jQuery是一个js工具类，React是一个js框架。

jQuery
:::::::

- 操作DOM方式

  **直接操作**

 使用选择器筛选出需要改变的Dom元素，或者直接对某个Dom元素进行监听。最后来直接改变真实Dom来达到预期的结果,流程图如下：

.. figure:: /_static/img/Deployment/ReactAndJquery0003.png

当页面的功能性不高时，jQuery可以比较直接的解决问题，但是在功能点比较复杂情况下，jQuery不断的去操纵DOM，不断去判断各种情况，造成代码结构复杂，后期难以维护，流程图如下：

.. figure:: /_static/img/Deployment/ReactAndJquery0004.png


- 页面切换

  关于页面jQuery采用传统链接的方式，直接访问新的地址，然后通过向后台获取新的数据加载出来。

React
::::::

- 操作DOM方式

  **基于数据驱动，数据决定DOM**

 React是提供了一整套的vistualDom，也就是虚拟Dom，所有的操作都在这个虚拟的Dom上而并非真实的Dom，React默认这个真实的Dom是不会被改变的，被改变的只有虚拟的Dom，然后通过这个虚拟的Dom来对真实的Dom进行渲染,流程图如下：

.. figure:: /_static/img/Deployment/ReactAndJquery0001.png

当页面比较复杂时，设计人员只需要关注当前的状态，在不同的状态下去设置相应的表现，这样会使得代码结构较为清晰，易于二次开发，流程图如下：

.. figure:: /_static/img/Deployment/ReactAndJquery0002.png


- 页面切换

React在页面切换中不是采用传统的连接跳转，严格的说React项目中的内容都呈现在一张HTML中，使用Router，根据链接的地址，获取需要展示的信息然后渲染出来。通俗的讲就是去采购东西，给了一张清单，根据清单来获取相应的物件。

总结
^^^^^

.. list-table:: 
   :widths: 20 20 20
   :header-rows: 1

   * - 
     - jQuery
     - React
   * - 本质
     - js工具类 
     - js框架
   * - 核心
     - 简化脚本语言 
     - 元素组件化、虚拟DOM、Diff算法
   * - 操作DOM方式
     - 直接调用 
     - 渲染
   * - 页面跳转
     - 原生Js
     - 路由router
   * - 可阅读性
     - 很低 
     - 很高
   * - 后期维护
     - 困难 
     - 容易





   
