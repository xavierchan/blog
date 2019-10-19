---
title: react component的生命周期
date: 2018-03-09 18:56:06
tags:
- 前端
categories:
---

## 一、构造函数

constructor(props, context)
构造函数，在创建组件的时候调用一次。

## 二、挂载之前

void componentWillMount()
在组件挂载之前调用一次。如果在这个函数里面调用setState，本次的render函数可以看到更新后的state，并且只渲染一次。

## 三、挂载之后

void componentDidMount()
在组件挂载之后调用一次。这个时候，子主键也都挂载好了，可以在这里使用refs。

## 四、属性传递

void componentWillReceiveProps(nextProps)
props是父组件传递给子组件的。父组件发生render的时候子组件就会调用componentWillReceiveProps（不管props有没有更新，也不管父子组件之间有没有数据交换）。

## 五、组件更新

bool shouldComponentUpdate(nextProps, nextState)
组件挂载之后，每次调用setState后都会调用shouldComponentUpdate判断是否需要重新渲染组件。默认返回true，需要重新render。在比较复杂的应用里，有一些数据的改变并不影响界面展示，可以在这里做判断，优化渲染效率。

## 六、组件更新之前

void componentWillUpdate(nextProps, nextState)
shouldComponentUpdate返回true或者调用forceUpdate之后，componentWillUpdate会被调用。

## 七、组件更新之后

void componentDidUpdate()
除了首次render之后调用componentDidMount，其它render结束之后都是调用componentDidUpdate。

componentWillMount、componentDidMount和componentWillUpdate、componentDidUpdate可以对应起来。区别在于，前者只有在挂载的时候会被调用；而后者在以后的每次更新渲染之后都会被调用。

## 八、渲染

ReactElement render()
render是一个React组件所必不可少的核心函数（上面的其它函数都不是必须的）。记住，不要在render里面修改state。

## 九、组件解除挂载

void componentWillUnmount()
组件被卸载的时候调用。一般在componentDidMount里面注册的事件需要在这里删除。
