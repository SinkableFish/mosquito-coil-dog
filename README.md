### 安装

第一步，在机器上安装node环境（v6+），然后将源码download到本地后，在项目根目录执行：

```
npm install
```

第二步，在机器上安装redis（3.2.0+），打开项目根目录中的`config.js`文件，修改其中的相关配置。一切就绪后就可以运行了：

```
$ node app.js
     ___  ___   _____   _____   _____   _____
    /   |/   | /  ___| |  _  \ /  _  \ /  ___|
   / /|   /| | | |     | | | | | | | | | |
  / / |__/ | | | |     | | | | | | | | | |  _
 / /       | | | |___  | |_| | | |_| | | |_| |
/_/        |_| \_____| |_____/ \_____/ \_____/
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Author: kazaff(edisondik@gmail.com)
=====================================
Api Server: http://127.0.0.1:2333/
Admin Server: http://127.0.0.1:2334/
account: kz
password: 123
```

### 服务编排

MCDog基于json语法（并不是严格遵守）来实现的DSL语义，允许使用者描述包括：

- 并行流
- 串行流
- REST任务
- 自定义函数任务
- 条件分支
- 输出过滤

在内的相关语义完成常见的服务编排工作。接下来我们举一个常见的例子：

第一步，按照安装流程将MCDog运行起来，确保它的配置（`config.js`）开启了管理后台服务。

第二步，打开任何一个REST调试工具，这里我们使用Postman来演示，如下图：
![](https://github.com/kazaff/mosquito-coil-dog/blob/master/docs/create.png)

第三步，继续用Postman请求`http://127.0.0.1:2334/service/rest_get_example_0.2_0/1`接口，注意，这个url前半部分是根据配置文件中定义的（例如：管理后台端地址和端口号），`/service/`部分是rest服务地址，为固定的。`/rest_get_example_0.2_0/`部分是上一步创建的服务的id。`/1`部分则表示将指定服务上线。

最后，一切就绪后，就可以访问创建的服务了: `http://127.0.0.1:2333/example/?id=1`，注意，应该在请求的header中添加对应的version参数，只有这样MCDog才能最终定位一个上线的服务。

### 不足

MCDog现在还很简陋，未来会根据其实际使用情况来逐步完善。目前可以预测的不足包括但不限于：

- 服务编排dsl校验不彻底，这会使得在上手时体验很差，无法很直观的定位错误
- 个别复杂的场景可能无法适配

至于功能扩展方面，可以参考其它文档中的描述。
