# 项目发布规范

TEST

TEST 环境为前后端开发、联调环境/预测试环境。

可同时存在多套环境，用端口区分。

端口规则：前端8000~8999，后端7000~7999。发布时，前端端口根据后端端口定，前端port=后端port + 1000。

在test环境的jenkins上（[http://test.x.xxx.net.cn:8080/），复制一套project，命名为projectName-port，设置默认分支和端口。](http://test.x.xxx.net.cn:8080/），复制一套project，命名为projectName-port，设置默认分支和端口。)

点击构建，默认会监听当前设置的分支，自动发布。

在服务器的jenkins上，新增一套服务，改变端口和指向目录。（以后会配置进jenkins脚本中）

SIT

SIT环境为功能测试环境，发布对应的release分支。

在SIT环境的jenkins上（[http://sit.x.xxx.net.cn:8080/），设置项目默认分支。](http://sit.x.xxx.net.cn:8080/），设置项目默认分支。)

点击构建，默认会监听当前设置的分支，自动发布。

UAT & 生产

将某个release分支/已合并新功能的master分支、版本号告知运维，由运维发布。

## Vue 相关项目部署发布

环境配置

安装git，node v7.1.0 拉取git项目, 如project 编译

在project项目中，执行 npm install，安装依赖\(若安装出错，则需要切换镜像源\) 执行 npm run build, 将文件产出到dist目录 server 配置

将server根目录指向project/dist 配置 404 转发\(nginx 等\)到 project/dist/index.html,参见\[\[[https://router.vuejs.org/zh-cn/essentials/history-mode.html\|HTML5](https://router.vuejs.org/zh-cn/essentials/history-mode.html|HTML5) History 模式下后端配置例子\]\] 配置 /third 转发到 project/dist/third 测试

访问 [http://domain](http://domain) 到首页，[http://domain/third](http://domain/third) 到third目录下非Vue页面，访问 [http://domain/404](http://domain/404) 到404页面 注意

后端需要设置跨域

## 灰度发布

正常发布 文档：前端将发布文档更新在禅道，由测试更新发布计划文档。（关键点：发布分支，如release/20171123，版本号，如：4.10.00）。 WebContent构建：运维根据发布文档，jenkins构建项目，最终打包出WebContent压缩包，如WebContent41000.zip，放在生产服务器，可通过链接直接下载。 备份服务：运维启动备用服务器，将生产服务用nginx切换到备用服务器。 在生产主服务器，部署后端最新版本服务。 测试回归：用生产版本的debug app，设置app请求的后端地址，webcontent地址，前端请求的后端地址后，进入页面测试。 正式升级：回归测试完毕，将生产nginx后端服务切换为生产主服务器的最新服务，将数据库app版本和webcontent版本升级。

灰度发布 接口调用：后端发布新服务，前端通过添加请求url params关键字段，匹配nginx规则，转发到相应后端服务地址。 WebContent构建：运维根据发布文档，jenkins构建项目，最终打包出WebContent压缩包，如WebContent41000.zip，放在生产服务器，可通过链接直接下载。 设置灰度范围：将数据库sys\_version表中的字段s\_store\_mac改为需要上的门店的mac地址，多个mac地址用逗号分隔。并更新相应字段的版本数字。版本配置使用原来字段app\_js\_version , s\_js\_download\_url ,s\_app\_download\_url，没做apk和zip包的md5校验。 更新过程：当app启动时，安卓会根据s\_store\_mac匹配该pos机mac地址。若匹配成功，则根据灰度字段更新app和webcontent。若匹配不成功，则按照正常版本逻辑。 注意：appversion接口存在2min延迟。

