# 第一节 测试相关的法则

## No.1 为什么要写测试用例,写测试用例是否会拖累开发进度?

项目多人协作开始时,为了某个功能修改了某个模块的代码,实际的情况中修改一个地方可能会影响到别人开发的多个功能,那么在自己不知情的情况下想要保证自己修改的代码不影响到其他功能,最简单的办法是通过测试用例来保证.

当然写测试用例拖累开发进度的情况也是客观存在的,通常有以下几种情况:

* 不会写测试用例;
* 过度测试,不必要的测试;
* 为了迎合测试,而忽略了实际需求;

## No.2 什么是测试金字塔?举例说明

测试金字塔反映的是需要写的单元测试,集成测试以及端到端的测试比例

以一个测试HTTP接口需要的测试比例来说:

1. 需要比较多的单元测试,分别测试各个模块(需要依赖stub);
2. 需要较少的集成测试,测试各个模块之间的交互(不能依赖stub);
3. 少量端到端测试,去调用真正的接口(不能依赖stub).

## No.3 测试是如何保证业务逻辑中不会出现死循环的?

你可以通过测试来避免业务中某些逻辑写出死循环,在通常的测试中加上超时的时间,在覆盖率足够的情况下,就可以通过跑出超时的测试来排查出现死循环以及低性能的情况.

## No.4 常用的测试方法有哪些呢?

* 黑盒测试: 测试应用程序的功能,关心输入和输出;
* 白盒测试: 测试应用程序的内部结构和逻辑;
* 单元测试: 是白盒测试的一种,用于针对程序模块进行正确性检验的测试工作,单元是指最小可测试的部件;
* 覆盖率: 指代码中各项逻辑被测试覆盖到的比例,常用的测试覆盖率框架istanbuf;
* mock: 通过模拟其他对象的数据来隔离你要测试的对象;
* 基准测试: 使用benchmark;
* 集成测试: 检查软件单位之间的接口是否正确;
* 压力测试: 保证系统稳定性的一种测试方法;
* Assert断言: 快速判断并对不符合预期的情况进行报错的模块.

## No.5 常用的测试工具有哪些?

* mocha: 现在最流行的JavaScript测试框架之一,在浏览器和Node环境都可以使用;
* ava: ava是mocha的替代品,对es6语法支持更好,对async/await有支持;执行效率更高,使用io并发,就必须保证测试的原子性;语义上更简单
* jest: Jest是Facebook出品的一个测试框架,相对其他测试框架,其一大特点就是内置了常用的测试工具,比如自带断言、测试覆盖率工具,实现了开箱即用.

## No.6 如何实现一个简单的测试单元框架?

```js
// 同步功能测试
test("测试 1", function() {
    assert.equal(1 + 1, 2);
});
// 异步功能测试
test("测试 2", function(done) {
    setTimeout(function() {
        assert.equal(2 + 2, 4); done();
    }, 100);
});
```
