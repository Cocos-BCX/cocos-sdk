[英文](https://github.com/Cocos-BCX/cocos-sdk/blob/master/readme.md)

# Loom SDK for Cocos Creator

## Content:

 * [环境依赖](#环境依赖)
 * [Loom Cocos SDK](#loom-cocos-sdk-介绍)
 * [打包并生成 Loom Cocos SDK](#打包并生成-loom-cocos-sdk)
 * [安装 Loom](#安装-loom)
 * [安装 Cocos Creator](#安装-cocos-creator)
 * [Creator Game 内集成调用](#creator-game-内集成调用)
 * [Sample](#sample)
 * [说明](#说明)


## 环境依赖:

1. Python 2.7
2. Git
3. [NodeJS](https://nodejs.org/en/), [NPM](https://www.npmjs.com/get-npm)
4. [Loom](https://loomx.io/), [Install Steps](https://loomx.io/developers/docs/en/prereqs.html)
5. [Cocos Creator](http://www.cocos.com/creator)


## Loom Cocos SDK 介绍

Loom 全局结构如下:

![](https://github.com/Cocos-BCX/cocos-sdk/blob/master/images/Loom-Cocos-SDK.png)

Loom Cocos SDK 软件结构如下:

![](https://github.com/Cocos-BCX/cocos-sdk/blob/master/images/loom-cocos-sdk-struct.png)

由图可见, `Loom-Cocos-SDK` 与 `loom-js` 使用相同的API, 相同的 `protobuf` 文件, 基本类似的合约写法。

`Loom Cocos SDK` 是基于 [Loom-JS](https://github.com/loomnetwork/loom-js/) 而移植到 `Cocos Creator` 上.

### 打包并生成 Loom Cocos SDK

* `git submodule update --init`, 更新 `git` 子工程， 如果已更新可以跳过
* 运行命令 `./tools/genCocoSDK.py`

`./tools/genCocoSDK.py` 会在工程根目录下生成的 `loom-cocos-sdk` 目录, 这就是 Loom SDK 在 Cocos Creator 上的适配包

## 安装 Loom

```
wget https://storage.googleapis.com/private.delegatecall.com/loom/osx/build-128/loom
chmod +x loom

mkdir tmpgopath
export GOPATH=`pwd`/tmpgopath
./loom spin weave-blueprint
cd blueprint
export GOPATH=$GOPATH:`pwd`
make deps
make
cd build

../../loom init
cp ../genesis.example.json genesis.json
```

运行 Blockchain

```
../../loom run
```

更多详情介绍参见[Loom SDK docs](https://loomx.io/developers/docs/en/prereqs.html).


## 安装 Cocos Creator

![](http://www.cocos2d-x.org/s/images/creator_192.png)

Cocos Creator是以内容创作为核心的游戏开发工具，在Cocos2d-x基础上实现了彻底脚本化、组件化和数据驱动等特点。

Cocos Creator基于开源框架Cocos2d-x，实现了一体化、可扩展、可自定义工作流的编辑器，并在Cocos系列产品中第一次引入了组件化编程思想和数据驱动的架构设计，这极大地简化了Cocos2d-x开发工作流中的场景编辑、UI设计、资源管理、游戏调试和预览、多平台发布等工作，是使用Cocos2d-x进行团队协作开发的最佳选择。

在 [这里](http://www.cocos.com/creator) 下载最新的 `Cocos Creator` 安装即可.


## Creator Game 内集成调用

1. 将上一步中打包生成好的 Loom Cocos SDK 放到工程的 `script` 目录下, 重命名为 `loom`
2. 根据你的游戏的需求编写自己的 `proto` 文件, 然后用 `protoc` 生成对应的 `js` 文件
  e.g. 本例中使用的是 [setscore.proto](https://github.com/loomnetwork/phaser-sdk-demo/blob/master/src/assets/protobuff/setscore.proto), 及对应生成的 [setscore_pb.js](https://github.com/loomnetwork/phaser-sdk-demo/blob/master/src/assets/protobuff/setscore_pb.js)
3. 编写适应自己游戏需求的合约, 使用上一步中的 `setscore_pb.js` 将数据序列化, 并将数据发往 `DappChain`, 参见  [SimpleContract](https://github.com/loomnetwork/phaser-sdk-demo/blob/master/src/SimpleContract.js)

![](https://github.com/Cocos-BCX/cocos-sdk/blob/master/images/script_loom_folder.png)

4. 在你的游戏中需要的位置调用上一步中的接口.
5. 运行, 检查

## Sample:

本工程中有带有两个 `Sample`:
* `loomDemoForCreator` 简单直接的调用合约接口, 更偏向于功能测试与只关注使用方式
* `dark-slash` 以更真实的游戏的方式来调用合约接口

测试步骤:

* 更新 `git` 子工程, 运行 `git submodule update --init`, 已更新的话，可以跳过
* 生成并打包 `Loom Cocos SDK`, 运行 `./tools/genCocoSDK.py`
* 同步生成好的包到 `sample/loomDemoForCreator`, `sample/dark-slash`, 运行 `./tools/syncLoomJSToSample.py`
* 切换到 `blueprint/build` 目录, 运行 `Loom Block Chain` 服务, 运行 `../../loom run`, 已运行，可以跳过
* 用 `Cocos Creator` 打开 `sample/loomDemoForCreator` 或 `sample/dark-slash`, 运行

## 说明

* `Loom Block Chain Server` 的配置, 运行, 合约的使用, 参见[这里](https://loomx.io/developers/docs/en/prereqs.html)
* Sample `dark-slash` 来自于 `Cocos Creator` 的[样例工程](https://github.com/cocos-creator/tutorial-dark-slash)


