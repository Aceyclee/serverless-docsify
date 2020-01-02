# 部署 serverless-docsify 站点

通过 Serverless Website 组件快速构建一个 Serverless docsify 站点。

三步进行：安装与初始化 → 配置 yml 文件 → 部署

## ▎安装与初始化

首先确保系统包含以下环境：
- [Node.js](https://nodejs.org/en/) (Node.js 版本需不低于 8.6，建议使用 10.0 及以上版本)
- [Git](https://git-scm.com/)

**1. 安装 Serverless Framework**

```
$ npm install -g serverless
```

**2. 安装 docsify**

```
$ npm i docsify-cli -g
```

**3. 初始化项目**

```
$ docsify init docsify
```

初始化成功后，可以看到 ./docsify 目录下创建的几个文件

- `index.html` 入口文件
- `README.md` 会做为主页内容渲染

直接编辑 `docsify/README.md` 就能更新网站内容，当然也可以写多个页面，这是后话。

**4. 本地预览**

运行以下命令，并通过浏览器访问 http://localhost:3000 即可方便地预览效果，而且提供 LiveReload 功能，可以实时预览。

```
$ docsify serve docsify
```

## ▎配置 yml 文件

在项目目录下，创建 `serverless.yml` 文件：

```
$ touch serverless.yml
```

将以下内容写入上述的 yml 文件里：

```console
# serverless.yml

mydocsify:
  component: "@serverless/tencent-website"
  inputs:
    code:
      src: ./docsify # Upload static files generated by docsify
      index: index.html
      error: index.html
    region: ap-guangzhou
    bucketName: my-bucket
```

配置完成后，文件目录如下：

```
.
├── docsify
|   ├── index.html
|   └── README.md
└── serverless.yml
```

## ▎部署

通过 `sls` 命令进行部署，这里还可以添加 `--debug` 参数来查看部署过程中的信息，

```
$ sls --debug
```

如果你的账号未 [登陆](https://cloud.tencent.com/login) 或 [注册](https://cloud.tencent.com/register) 腾讯云，可以直接通过微信扫描命令行中的二维码，从而进行授权登陆和注册。这也是我觉得特别方便的一个地方！

部署过程中，terminal 显示信息示意：

![部署过程](https://img.serverlesscloud.cn/20191216/1576499845193-terminal.png)

访问命令行输出的 url，即可查看使用 Serverless Framework 部署的 docsify 文档网站啦~

![最终效果](https://img.serverlesscloud.cn/20191216/1576501239900-WX20191216-205729%402x.png)

## ▎移除

如需移除，键入以下命令即可：

```
$ sls remove --debug
```