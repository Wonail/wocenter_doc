# 手动安装 #

>   WoCenter只是一个底层框架，本身并不支持直接通过 Web 方式访问，需要手动部署。
当然，WoCenter已经为你准备了一套可以正常部署的高级项目模板 [wocenter_advanced](https://github.com/Wonail/wocenter_advanced) 。
这样做的目的是确保二次开发的文件和WoCenter核心文件完全隔离，互不干扰，做到升级WoCenter核心时不破坏二次开发已有的文件。

WoCenter核心以composer包方式发布，故安装前请确保你的系统已经安装了[composer](install-composer.md)。

## 环境准备
1. 搭建所需的服务器环境，参考[服务器环境搭建](server-environment.md)

2. 请确保使用的Composer和Composer Asset Plugin是最新版本，如果不是，需要执行以下命令：

   ```bash
   $ composer self-update
   $ composer global require "fxp/composer-asset-plugin:^1.3.1" --no-plugins
   ```
3. 建议更改为[国内镜像](https://pkg.phpcomposer.com/)，可以有效提高下载速度（可跳过）

   ```bash
   $ composer config -g repo.packagist composer https://packagist.phpcomposer.com
   ```

## 正式安装
1. 新建名为`wocenter`的数据库
2. 克隆 [wocenter_advanced](https://github.com/Wonail/wocenter_advanced) 项目

    切换到一个可以通过 Web 访问的目录（如：`/home/www`），执行以下命令：

   ```bash
   $ git clone https://github.com/Wonail/wocenter_advanced.git #克隆wocenter_advanced高级项目模板
   $ cd wocenter_advanced #进入项目目录
   ```

3. 配置数据库相关信息

    开发环境

   > environments/dev/common/config/main-local.php

    正式环境

   > environments/prod/common/config/main-local.php

   ```php
   'components' => [
       'db' => [
           ……，
           'dsn' => 'mysql:host=localhost;dbname=wocenter', // 数据库名称，如果没有修改，默认为wocenter
           'username' => 'root', // 数据库用户名
           'password' => '', // 数据库密码
           ……，
       ],
       ……
   ]
   ```
4. 安装composer依赖。此步骤会安装WoCenter核心包以及其他一些依赖包

   ```bash
   $ composer install -vvv
   ```

5. 使用 WoCenter 内置的安装方法完成剩余的安装步骤

   ```bash
   #Linux or Mac环境
   $ ./yii wocenter/install

   #Windows环境
   $ yii.bat wocenter/install
   ```

## 验证安装结果

通过浏览器访问 URL `localhost/wocenter_advanced/backend/web/index.php`即可。

>   账号：admin 密码：admin123


如果访问失败，请检查当前PHP环境是否满足WoCenter最基本需求，可以通过以下方式进行检查：

1. 通过浏览器访问 URL `localhost/wocenter_advanced/requirements.php`
2. WoCenter需要使用到数据库，所以必须安装 [PDO PHP 扩展](http://www.php.net/manual/zh/pdo.installation.php)
和MySQL数据库驱动所需的 `pdo_mysql`
3. **WoCenter建议安装 Intl**
4. 以上均无法解决，请查看 [问题反馈](issue.md)

