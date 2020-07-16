---
title: React 组件生命周期
date: 2020-07-16 23:07:05
tags:
---
每个组件都包含生命周期方法， 你可以重写这些方法，以便在运行的过程中特定的阶段执，以下列表中常用的生命周期方法被加粗：

挂载
当组件实例被创建并插入dom时，按如下顺序调用生命周期方法：

1. **constructor()**
2. static getDerivedStateFromProps()
3. **render()**
4. **componentDidMount()**

v16.3后
componentWillMount 被替换成
UNSAFE_componentWillMount() 并且该生命周期方法也即将过时

被替换原因： 开发时习惯于在此生命周期中初始化state及做一些异步数据的请求等一些可能产生副作用的操作，比如在此时进行了订阅操作， 在componentWillUnmount中取消订阅，但是componentWillUnmount执行的前提是 执行过componentDidMount，这样就会导致无法取消订阅， 订阅产生的副作用容易导致内存泄漏； 所以我们可以在constructor中进行数据的初始化，在componentDidMount中去进行异步数据的请求


更新
当组件的state或者props发生改变时会触发组件更新
1. static getDerivedStateFromProps()
2. shouldComponentUpdate()
3. **render()**
4. getSnapshotBeforeUpdate()
5. **componentDidUpdate()**

UNSAFE_componentWillUpdate();
UNSAFE_componentWillRecieveProps();

弃用原因：
componentWillRecieveProps() 一般用于props更新，组件同步更新state,但如果在此生命周期中调用父组件带有setState的操作函数造成父组件重新渲染，子组件会再次调用此函数 时容易造成死循环 （之前使用时，是会进行相应的判断去避免造成重复渲染）
componentWillUpdate() 在视图更新前触发

