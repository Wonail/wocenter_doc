# 如何升级 #

## 升级WoCenter Advanced高级项目模板 ##

通常该项目模板很少涉及到太多的更新，因为系统主要功能都以composer包方式存在。如果需要升级，可以通过以下方式进行：

1. 通过浏览器访问 URL [https://github.com/Wonail/wocenter_advanced/releases](https://github.com/Wonail/wocenter_advanced/releases)
了解是否存在可以更新的版本。

2. 执行以下命令进行更新：

   ```bash
   $ cd wocenter_advanced #进入项目根目录
   $ git pull origin master #拉取最新版本
   ```

如果更改过项目原有文件，请手动解决冲突后再执行更新操作。

## 升级WoCenter核心 ##

WoCenter核心以composer包方式发布，如果需要升级，可以通过以下方式进行：

1. 打开wocenter_advanced目录下面的composer.json文件，可以看到类似以下的内容：

   ```php
   "require": {
       "wonail/wocenter": "dev-master",
   },
   ```

2. 把`dev-master`更改为你想要升级或降级的版本号，目前默认使用的是开发者版本`dev-master`，即每次升级，使用的都是最新提交的版本。

3. 执行更新命令：

   ```bash
   $ composer update -v
   ```

>   注意：我们不建议直接使用`dev-master`版本来部署你的线上系统，因为这并不一定稳定。
>   我们推荐你通过**WoCenter升级帮助文件**来辅助完成更新步骤。如果不存在该文件，通常意味着你可以放心执行更新操作。