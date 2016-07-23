# Node Starter Kit

如果第一次使用 `node`，熟悉此文档内所有内容至少需要几天时间，做好心理准备 😄

## 语法约定

按照目前 `Node` 对 ES2015 的支持标准，除 `import` 等特性，其余均可以使用，
详情见：https://nodejs.org/en/docs/es6/

语法风格按照 [Google JavaScript 编码规范指南](http://alloyteam.github.io/JX/doc/specification/google-javascript.xml)

熟悉 ES2015 建议查看此文章：http://gank.io/post/564151c1f1df1210001c9161

1. 统一使用严格模式

    需要在每个文件开头加入 `'use strict';`

2. 定义变量和常用使用 `let`， `const`，尽量不使用 `var`

3. 参考 #其他-1 配置好语法高亮和语法检查


## 如何把项目跑起来（以 Mac 为例）

1. 安装 Homebrew

   ```
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

2. 安装 `node` 要求至少 `5.10.0` 以上版本

   ```
   brew install node
   ```

3. 安装 `cnpm` 镜像加速，`npm` 国内访问太慢

   ```
   npm install -g cnpm --registry=https://registry.npm.taobao.org
   ```

4. 安装全局 `npm` 依赖

   可以使用 `cnpm info knex` 查看各个包的详细信息

   ```
   cnpm i -g knex nodemon babel babel-eslint
   // 各模块说明
   // knex - SQL 构造器以及数据库迁移工具
   // nodemon - node 调试工具，用于代码改变后自动重启服务
   // balbel, balbel-eslint 用于 ES2015 语法兼容，用于 IDE 语法查错等
   ```

5. 安装项目依赖

   ```
   cnpm i
   ```

6. 创建项目配置

    可以根据自己机器适当修改配置，例如数据库端口、密码等

    ```
    cp .env.example .env
    ```

7. 初始化数据库

    执行此操作前请确认自己机器数据库服务已正常运行，
    另外由于 `bookshelf` 默认采用 JSON 标准格式存储日期，如果使用 mysql 请关闭严格模式：
    https://github.com/TryGhost/Ghost/issues/5050#issuecomment-83613536
    http://dba.stackexchange.com/questions/48704/mysql-5-6-datetime-incorrect-datetime-value-2013-08-25t1700000000-with-er

    ```
    // 表结构
    knex migrate:latest

    // 初始数据
    knex seed:run

    // 更多用法参见 `knex -h`
    ```

8. 启动项目

   ```
   npm run dev // dev 环境
   npm start // 线上环境
   ```

9. Nginx 配置

   如果需要可以参考项目 `xx.nginx.conf.example`



## Node.js 基础类库 （按重要级排序）

在开始之前，你至少需要熟悉 `node` 的一些内置的类库，
例如：`Buffer`，`File System`，`Path`，`URL`，`HTTP`，`Process`，`Utilities`，`Events`

http://nodejs.org/api

**以下类库为基础类库，建议把文档看完再开始**

1. bluebird - Promise A+ 规范实现类库，一个通用的异步编程规范

   http://bluebirdjs.com/docs/api-reference.html

2. co - koa 底层类库，基于 ES6 特性实现同步式异步编程

   https://github.com/tj/co

3. knex - 一个 SQL 构造器，`bookshelfjs` 基础支撑

   http://knexjs.org/

4. bookshelf - 一个不错的 ORM

   http://bookshelfjs.org/


## WEB 服务

**koa 库为主框架，同样建议把文档看完再开始**

1. koa - next generation web framework for node.js

    官网：http://koajs.com/
    官网翻译：http://koa.bootcss.com/
    中文指南：https://github.com/guo-yu/koa-guide

2. koa 基础依赖

    以下为列举的一些常用中间件，需要其他可以上 Github 搜索
    https://github.com/koajs/

    - koa-compose 中间键分发，用于多个域名等情况
    - koa-onerror 统一错误处理
    - koa-compress 内容压缩 gzip 等
    - koa-router 路由，此中间件非官方，但是比官方好用
    - koa-bodyparser 请求内容解析，自动根据 content-type 解析 json 或者 www-url-encode
    - koa-session
    - koa-passport 一个基于 `Passport` 的身份管理库
    - koa-views 模板
        - ejs

3. 缓存相关

    - co-redis
    - then-redis



## 扩展类库

1. lodash - 一个强大的工具类库，一般用于数组或者对象的批量处理

    **强烈建议熟悉常用 API**
    https://lodash.com/

2. dotenv/dotenv-safe - 项目配置支持，方便管理环境变量，区分开发和线上环境

    https://github.com/rolodato/dotenv-safe
    https://github.com/motdotla/dotenv

3. debug - 带颜色和时间的调试打印，可以作为 `winston` 的 transports

    https://github.com/visionmedia/debug

4. winston - 一个强大的日志系统，可以自定义 `transports`，例如支持 `redis` 和 文件存储等

    https://github.com/winstonjs/winston

5. fs-extra-promise - 一个基于 `promise` 实现的 `fs`

6. request-promise/co-request - 请求发起工具

    https://github.com/request/request-promise
    https://github.com/leukhin/co-request


## 后台任务

1. kue - 一个不错的任务管理系统


## 服务管理

1. pm2 - 服务管理工具



## 其他

1. IDE/编辑器 语法检查

    如果使用 Sublime Text 建议安装，你需要安装如下几个插件：
    `Babel` - 用于对 ES2015 的语法高亮支持
    `SublimeLinter`， `sublimeLinter-contrib-eslint` - 用于基于 `eslint` 语法检查，在语法有问题时有提示

    其余 IDE/编辑器请自行搜索
