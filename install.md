# windows安装cypress_realworld

### 安装cmder

cmder自带了git支持，而且支持部分的linux like命令，用起来比较舒适，尽管颜值不如ms的windows terminal，不过使用习惯之后整体效率还是很高的。

[官网](https://cmder.net/)

这里推荐full版本，这个版本带了git支持。(with Git for Windows) 

### 在windows上安装nodejs

在windows上安装nodejs的方式很多，为了方便以后管理，推荐使用[nvm windows](https://github.com/coreybutler/nvm-windows)。

nvm windows可以管理多个不同版本的nodejs，这为后面升级提供了灵活性。

[下载地址](https://github.com/coreybutler/nvm-windows/releases)。

[安装教程](https://github.com/coreybutler/nvm-windows)

典型使用

```
nvm use 14.0.0
npm install -g yarn
nvm use 12.0.1
npm install -g yarn
```


### 使用git下载代码

[cypress-realworld-app](https://github.com/cypress-io/cypress-realworld-app)

在cmder中使用下面的命令下载项目代码

```
git clone https://github.com/cypress-io/cypress-realworld-app.git
```

### 安装依赖包

``` 
nmp install -g yarn
yarn install
```

在一般的网络条件下，整个过程非常缓慢，我第一次安装大概花了1个多小时。

### yarn 加速

参考[这里](https://learnku.com/articles/15976/yarn-accelerate-and-modify-mirror-source-in-china)

为什么慢?

执行 yarn 各种命令的时候，默认是去 npm/yarn 官方镜像源获取需要安装的具体软件信息

以下命令查看当前使用的镜像源

```
yarn config get registry
```

默认源地址在国外，从国内访问的速度肯定比较慢

如何修改镜像源

阿里旗下维护着一个完整的 npm 镜像源 ```registry.npm.taobao.org/``` 同样适用于 yarn

1. 临时修改

```
yarn save 软件名 --registry https://registry.npm.taobao.org/
```

2. 全局修改
```
yarn config set registry https://registry.npm.taobao.org/
```

### 启动开发环境

```
yarn dev
```

如无错误浏览器会自动打开，并访问localhost:3000。

### 使用项目自带的用户进行登录

[自带用户](https://github.com/cypress-io/cypress-realworld-app/blob/develop/data/database.json#L8)

注意:在开发环境下，所有的用户密码都是**s3cret**


### 启动cypress

```
yarn cypress:open
```

