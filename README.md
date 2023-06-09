# 关于这个项目

这是我参加第五届字节跳动青训营大项目与其他三名同学完成的极简版抖音服务端，关于这个项目的说明请参阅下方的文档以及docs目录下部分模块的说明文档。另外，在app目录里已经上传了极简版抖音的apk安装包，通过安卓模拟器就可以在PC上运行，以便调试项目。

# tiktok

This is a distributed **simple-tiktok** backend based on RPC and HTTP protocols using Kitex + Hertz + Etcd + MySQL + Jaeger + Docker + Protobuf3

# How To Run This Project

We use docker to create project's biz environment. So before everything, we need to start docker in project root :

```bash
docker-compose up -d
```

Then, we should launch all of the different miceoservices.

We step in every microservice's folder: **./services**，in microservice's workspace, we start it by :

```bash
sh build.sh
sh output/bootstrap.sh
```

Finally, we should launch api-gateway，we tap in **./api-gateway** folder, then use this command :

```bash
sh run.sh
```

# How To Send Request

we use Postman to test request.

import **./postman** to Postman，we can see :

![202303031231510](docs/img/202303031233520.png)

We have preset the request, you can directly modify the request parameters for testing

# Architecture Design

![202303031231510](docs/img/202303031231510.jpg)

# Tracer

Visit `http://localhost:16686` for more detail

![](docs/img/20230303132744.png)

# Directory Structure

Next, some directories will be annotated in Chinese

## Gateway

```plain
api-gateway/
├── Makefile        // 常用命令行指令
├── biz             // 核心
│   ├── handler    // HTTP处理
│   ├── model      // 模型定义
│   ├── router     // 路由
│   ├── rpc        // RPC调用函数
│   └── types      // 模型抽象
├── main.go         // 入口
├── router.go       // 自定义路由
└── router_gen.go   // Hertz路由生成代码
```

## Microservice

For every different microservice, we have different or same file struct.

Here is one of the file structure:

```plain
user/
├── configs               // 微服务启动配置，包括数据库连接
├── service               // 微服务实际处理模块
├── model                 // 自定义结构体
├── script                // 编译指令
├── pack                  // 请求封装
├── utils                 // 通用函数
├── main.go               // 程序入口
├── handler.go            // 请求处理
├── kitex.yaml            // Kitex配置
└── Makefile              // 常用指令
```

# API Interface

For more detail, please visit :

https://www.apifox.cn/apidoc/shared-09d88f32-0b6c-4157-9d07-a36d32d7a75c/api-50707523

# Project Features

- Distributed architecture
- Support tracing
- Suppoort recovery
- Unified error handle
- Layered processing of requests
- Unified constant management
- ...

# Roadmap

This project is not perfect，here are the items we have noticed and plan to optimize

- Unified logging
- Add redis support
- Use message queue to optimize some interfaces
- Use yaml custom configuration
- Unit test
- ...
