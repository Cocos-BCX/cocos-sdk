[中文](https://github.com/Cocos-BCX/cocos-sdk/blob/master/README_cn.md)

# Loom SDK for Cocos Creator

## Content:
 * [Prerequisites](#prerequisites)
 * [Loom Cocos SDK](#loom-cocos-sdk)
 * [Generate LoomJS SDK](#generate-loomjs-sdk)
 * [Install Loom](#install-loom)
 * [Install Cocos Creator](#install-cocos-creator)
 * [Integrate to Creator Game](#integrate-to-creator-game)
 * [Sample](#sample)
 * [Notice](#notice)

## Prerequisites

1. Python 2.7
2. Git
3. [NodeJS](https://nodejs.org/en/), [NPM](https://www.npmjs.com/get-npm)
4. [Loom](https://loomx.io/), [Install Steps](https://loomx.io/developers/docs/en/prereqs.html)
5. [Cocos Creator](http://www.cocos.com/creator)

## Loom Cocos SDK

Loom global structure diagram

![](https://github.com/Cocos-BCX/cocos-sdk/blob/master/images/Loom-Cocos-SDK.png)

Loom Cocos SDK structure diagram

![](https://github.com/Cocos-BCX/cocos-sdk/blob/master/images/loom-cocos-sdk-struct.png)

`Loom-Cocos-SDK` have same api, same protobuf, similar contract with `loom-js`.

`Loom Cocos SDK` is base on [Loom-JS](https://github.com/loomnetwork/loom-js/) , and proting it to `Cocos Creator` .

### Generate LoomJS SDK
* `git submodule update --init`, update git submodule
* `./tools/genCocoSDK.py`

`Loom SDK for Cocos Creator` is the directory `loom-cocos-sdk`, which is generated by command `./tools/genCocoSDK.py`

## Install Loom

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

Run Blockchain:

```
# unable to start http server: listen tcp 127.0.0.1:9092: bind: address already in use
pkill blueprint # kill server first
../../loom run
```



Please consult the [Loom SDK docs](https://loomx.io/developers/docs/en/prereqs.html) for further instruction on running your own DappChain.

## Install Cocos Creator

![](http://www.cocos2d-x.org/s/images/creator_192.png)

Cocos Creator is a complete package of game development tools and workflow, including a game engine (based on Cocos2d-x), resource management, scene editing, game preview, debug and publish one project to multiple platforms.

For the first time we introduced entity-component structure and data-driven workflow to the Cocos2d-x family. With JavaScript, you can scripting your component in no time. The editor and engine extension is also made with JavaScript so you can make games and refine your tool in a single programming language.

Cocos Creator provides an innovative, easy to use toolset such as the UI system and Animation editor. The toolset will be expanding continuously and quickly, thanks to the open editor extension system.

you can download `Cocos Creator` from [here](http://www.cocos.com/creator) , and install.

## Integrate to Creator Game

1. copy the generated `Loom Cocos SDK` to your project's `asset/script` directory, and rename it to `loom`
2. write your own `proto` file as requirements of your game
  e.g. `sample/loomDemoForCreator` use  [setscore.proto](https://github.com/loomnetwork/phaser-sdk-demo/blob/master/src/assets/protobuff/setscore.proto), and related [setscore_pb.js](https://github.com/loomnetwork/phaser-sdk-demo/blob/master/src/assets/protobuff/setscore_pb.js)
3. write yur own contract as requirements of your game, and serailezse your data with `setscore_pb.js`, and send to Loom Blockchain, take a look at [SimpleContract](https://github.com/loomnetwork/phaser-sdk-demo/blob/master/src/SimpleContract.js)

![](https://github.com/Cocos-BCX/cocos-sdk/blob/master/images/script_loom_folder.png)

4. invoke api of your contract at suitable position.
5. Run

## Sample:

there have two `Sample` project:
* `loomDemoForCreator` simplely use loom sdk
* `dark-slash` use loom sdk in a real game

Test Steps

* update git submodule, run command `git submodule update --init`, if you have done this, skip this.
* generate and pack `Loom Cocos SDK`, run command `./tools/genCocoSDK.py`
* sync `Loom Cocos SDK` to `sample/loomDemoForCreator` and `sample/dark-slash`, run command `./tools/syncLoomJSToSample.py`
* entry directory `blueprint/build`, run `Loom Block Chain` services, run command `../../loom run`, if you have done this, skip this.
* open `sample/loomDemoForCreator` or `sample/dark-slash` with `Cocos Creator` and run

## Notice

* `Loom Block Chain` configuration, Contract's usage, take a look at [this](https://loomx.io/developers/docs/en/prereqs.html)
* Sample `dark-slash` come from `Cocos Creator` [Tutorial Project](https://github.com/cocos-creator/tutorial-dark-slash)

---
