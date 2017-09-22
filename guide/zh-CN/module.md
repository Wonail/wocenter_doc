# 高度模块化 #

## 简介

WoCenter在功能粒度上划分出多个模块，每个模块职能分配清楚，利于管理和二次开发。同时系统提供了一套专门用于管理符合 WoCenter
**模块标准**的模块管理系统，可以方便进行**安装**、**卸载**和**升级**等操作。

保持着对二次开发**便捷性**、**易用性**和**低干扰性**的重视，模块可以实现**零配置**即可使用，包括模块所属菜单、权限、URL路由规则、
bootstrap等都已实现**自动化**。

WoCenter的`backend`应用目前提供了用户管理、安全管理、扩展中心、系统管理、运营管理等多个模块，其中大部分模块都是系统的
**核心模块**，不可被卸载。可通过`\wocenter\services\ModularityService::getCoreModules()`方法查看当前应用的**核心模块**。

## 优势

- 自动加载模块所属的`菜单`、`权限`、`URL路由规则`、`bootstrap`等，实现模块使用**零配置**。
- **零配置**无缝切换**开发者模块**和**系统核心模块**。

## 如何使用

- 通过`WoCenter Gii`的模块生成器可轻松创建符合WoCenter**模块标准**的模块或修改已有的模块以符合WoCenter的**模块标准**。

- 手动更改已有模块，只需按照以下步骤即可完成改造：

  1. 模块目录下的模块配置文件名更改为`Module.php`。
  2. `Module.php`继承`\wocenter\core\Modularity`类或更改`$defaultRoute`属性值为`common`。

      如果原有模块存在`controllers/DefaultController`控制器，则必须更改名为`CommonController`。

      如果原有模块存在`views/default`视图目录，则必须更改名为`common`。

     >   改名的目的是为了使用系统的Dispath调度服务，因为调度器所需的命名空间不支持`default`|`public`等字符，
     这是`PHP`本身设计上的约束。

  3. 模块目录下创建`Info.php`模块详情类，该类必须继承`\wocenter\core\ModularityInfo`类或其派生类。
  可参考`\wocenter\backend\modules\gii\Info`类完成创建。

  4. 删除模块配置信息，一般可能存在于`main.php`、`main-local.php`这样的配置文件里。

  5. 进入【模块管理】，执行`清理缓存`即可看到新的模块。接着执行安装操作即可使用。

>   使用`WoCenter Gii`的模块生成器默认生成文件的路径为**开发者主题路径**，即`\wocenter\core\View::getDeveloperThemePath()`。

## 总结

>   使用WoCenter的模块管理系统可以轻松实现对现有系统功能的扩展或替换，免除每次增加或替换模块时都需要手动更改系统配置文件。