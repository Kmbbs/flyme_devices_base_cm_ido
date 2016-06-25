#红米3插桩适配FlymeOS5,基于CM12.1的底包
20160613更新日志：
同步FlymeOS官方最新开源项目version Flyme 5.1.6.13代码
【相机】使用旧版相机，修复相机拉长，支持二维码扫描
【短信】修复短信FC
【音乐】使用旧版音乐修复本地音乐FC
【设置】移除关于-系统更新以及MzUpdate.apk
【其他】修复若干bug
--------------------------------------------
1. 介绍
FlymeOS开源项目致力于为开发者提供业界一流的ROM适配工具。

二零一五年六月三十日，FlymeOS开放适配终于来了，我们相信虽晚未迟。

License

2. 分支命名
开源项目的分支命名与Android版本对应,目前支持Android 5.1的机型适配，分支名为：lollipop-5.1

目录结构如下所示:

FlymeOS
 +-- manifest           项目清单
 +-- tutorials          教程文档
 +-- build              编译环境，用于构建和编译机型
 +-- tools              适配工具
 +-- flyme              Flyme相关，内容定期更新
      +-- release       官方发布的ROM包
      +-- overlay       资源覆盖
 +-- devices            机型目录
      +-- base          官方提供的默认机型
      +-- base_cm       第三方提供的CM机型
      +-- your_device   待开发者适配的机型
3. 代码下载
通过repo init命令的-b参数, 选择需要下载的分支。 通过repo sync命令同步远程代码:

$ repo init -u https://github.com/FlymeOS5/manifest.git -b lollipop-5.1
$ repo sync -c -j4
4. 机型适配
* 标准流程

下载完代码以后, 在开源项目根目录, 执行以下命令初始化开发环境:

$ source build/envsetup.sh
创建一个新的机型工程的目录(以demo为例), 后续的移植都在机型目录完成。

$ mkdir -p devices/demo
$ cd devices/demo
按照如下步骤，完成一个新机型的适配：

$ flyme config      # 生成机型配置文件Makefile
$ flyme newproject  # 生成新机型目录
$ flyme patchall    # 自动插桩
$ flyme fullota     # 生成适配完成的ROM包
* 冲突处理

自动插桩可能会造成代码合并冲突。冲突会以下面的形式标注出来, 开发者需要在厂商的文件中手工解决这些冲突。

<<<<<<< VENDOR
  原厂的代码块
=======
  Flyme的代码块
>>>>>>> BOSP
* 版本升级

可以跟随官方发布的最新ROM包，将已经是适配完成的机型升级到最新版本：

$ flyme clean
$ flyme upgrade
