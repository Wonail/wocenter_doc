# 多模板系统

## 简介

WoCenter使用多主题模板系统，系统内置了多个主题模板路径映射，这个特性的存在，使得开发者可以方便地对系统核心视图文件（View）、
布局文件（Layout）、资源文件（AssetBundle、Js、Css、Img）等进行重写与个性化，而这一切的修改都不会影响WoCenter后期的升级。

## 原理

WoCenter的多主题模板系统是由`\wocenter\core\View`组件提供功能支持，具体是通过主题路径映射实现。你可以查看
`\wocenter\core\View::setPathMap()`了解详细配置，也可继续阅读下面**[优先级](#you-xian-ji)**所做的具体文字说明了解详情。

>   如果需要自定义Yii2默认的`\yii\web\View`组件，必须确保自定义的`View`类继承`\wocenter\core\View`类或其派生类。

## 主要方法

`\wocenter\core\View`类实现了**系统核心主题路径**和**开发者主题路径**的获取方法，以下是系统默认的主题路径配置：

- **系统核心主题路径**：`@wocenter/{app}/themes/{theme}`：

  以`backend`为当前应用、`adminlte`为当前系统使用的主题为例，该应用的系统核心主题路径为
`vendor/wonail/wocenter/backend/themes/adminlte`。

  获取方法：`\wocenter\core\View::getCoreThemePath()`。

- **开发者主题路径**：`@app/themes/{theme}`：

  以`backend`为当前应用、`adminlte`为当前系统使用的主题为例，该应用的开发者主题路径为`backend/themes/adminlte`。

  获取方法：`\wocenter\core\View::getDeveloperThemePath()`。

系统默认的**开发者主题路径**可以通过`\wocenter\core\View::setBaseThemePath()`方法自定义，详情请查看该方法。

>   信息：`\wocenter\core\View::getCoreThemePath()`和`\wocenter\core\View::getDeveloperThemePath()`方法是系统
**[Dispatch调度服务](dispatch.md)**的基础。

## 优先级

以下是系统默认内置的路径映射配置，优先级从上到下（可直接阅读 **[总结](#zong-jie)** ，也可阅读下面了解详情）：

1. `@app/views`：当前应用的视图目录。一般是当前应用的默认路由需要使用到，如：`site/index`操作，视图`index.php`文件通常存放于此。

   1. `@app/views`视图目录下的文件优先级最高。

      系统使用多主题设计，我们不建议在此处存放修改系统核心的视图文件，因为这会覆盖所有主题目录下的该文件。
      如果你不是非常确定需要替代所有主题下的该文件，建议你可以在**开发者主题路径**下进行操作。

   2. **开发者主题路径**下的`views`视图目录。

      >   这是我们推荐的用于存放修改系统核心视图文件的位置。

   3. **系统核心主题路径**下的`views`视图目录。

      如果此处找不到所需的视图文件，则会抛出`ViewNotFoundException`异常信息。

2. `@backend/modules`：开发者模块目录。该值可通过`\wocenter\services\ModularityService::$developerModuleNamespace`属性自定义。

   1. `@backend/modules`模块目录下的文件优先级最高。

      系统使用多主题设计，我们不建议在此处存放修改系统核心的视图文件，因为这会覆盖所有主题目录下的该文件。
      如果你不是非常确定需要替代所有主题下的该文件，建议你可以在**开发者主题路径**下进行操作。

   2. **开发者主题路径**下的`modules`模块目录。

      >   这是我们推荐的用于存放修改系统核心视图文件的位置。

      这是确保开发者能够自由定义系统核心视图文件的前提，只要该路径下存在和**系统核心主题路径**下相同位置的视图文件，
      即可起到轻松替换系统核心视图文件的作用。

   3. **系统核心主题路径**下的`modules`模块目录。

      如果此处找不到所需的视图文件，则会抛出`ViewNotFoundException`异常信息。

3. `@wocenter/backend/modules`：系统核心模块目录。该值可通过`\wocenter\services\ModularityService::$coreModuleNamespace`
属性自定义。通常该值由WoCenter开发其他应用时使用，开发者可以忽略。

   1. `@backend/modules`模块目录下的文件优先级最高。

      系统使用多主题设计，我们不建议在此处存放修改系统核心的视图文件，因为这会覆盖所有主题目录下的该文件。
      如果你不是非常确定需要替代所有主题下的该文件，建议你可以在**开发者主题路径**下进行操作。

   2. **开发者主题路径**下的`modules`模块目录。

      >   这是我们推荐的用于存放修改系统核心视图文件的位置。

      这是确保开发者能够自由定义系统核心视图文件的前提，只要该路径下存在和**系统核心主题路径**下相同位置的视图文件，
      即可起到轻松替换系统核心视图文件的作用。

   3. **系统核心主题路径**下的`modules`模块目录。

      如果此处找不到所需的视图文件，则会抛出`ViewNotFoundException`异常信息。

## 总结

只要在`@app`相同路径下存在和`@wocenter`相同路径下同名的文件，即可起到轻松替换系统核心视图文件的作用。