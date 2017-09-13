# Service 服务

## 简介

Service服务层的目的在于进一步解耦Model层，让Model层只专注于CRUD、规则验证、数据库映射等简单操作，**降低Model和业务逻辑的耦合性**，
方便日后业务发展可灵活定制Model底层，而其余复杂的业务逻辑则交由Service层为系统或各模块提供对内开放的使用接口。

## 原理

WoCenter的服务层由许多继承`\wocenter\core\Service`的服务类和起到定位作用的`\wocenter\core\ServiceLocator`服务定位器组成，
以系统组件（即`component`）的形式存在。

## 核心文件

- 继承`\wocenter\core\Service`的服务类，这是服务层提供功能的主要文件，如：`PassportService`、`LogService`等。
- `\wocenter\core\ServiceLocator`服务定位器。顾名思义，在使用服务时，系统会在此定位器搜索是否存在相关的服务。

## 功能粒度

- Model层的功能粒度：对应的是数据库的CRUD操作、规则验证、数据库映射、数据缓存等和具体功能实现相关性不高的操作。
- Service层的功能粒度：对应的是一个具体的行为实现，如：登录系统、找回密码、发送验证邮件等。

## 约定

- 尽量遵循[功能粒度](#gong-neng-li-du)的要求，方便日后Model底层的扩展或更换。

- 服务`component`组件的配置，必须遵循WoCenter的**服务类命名规则**：

  - 由`服务ID`+`Service`后缀组成，如：`passportService`、`systemService`等。

  - `服务ID`可通过服务类的`\wocenter\core\Service::getId()`方法获取，如：`passport`、`system`等。

  - `Service`后缀是为了区分开发者原有系统中存在的组件名，确保调用服务的可用性。

- 子服务必须存放在以顶级服务ID为名的目录内，如：`PassportService`顶级服务的`ValidationService`子服务，
存放在`@wocenter/services/passport`目录内。

- 按功能或行为类型，合理为顶级服务创建子服务，保证层次清晰，功能划分明显，易于管理和二次开发。

    如：`PassportService`顶级服务的子服务：`UcenterService`、`ValidationService`、`VerifyService`，
    每个子服务统一管理相似的功能或行为。日后需要调整，可以方便定位到相关服务。

## 使用

使用WoCenter服务，有以下两个方法：

1. 通过`\Yii::$app->get('xyzService')`方式调用，这是Yii2获取系统组件的方式。
2. 通过`\wocenter\Wc::$service->getXyz()`或`\wocenter\Wc::$service->xyz`方式调用，建议使用前者，不论是对IDE友好性
还是性能方面都很好。这是WoCenter推荐的使用服务的**首选方法**，它有以下优势：
  1. 检测服务组件是否符合WoCenter的服务类标准
  2. 支持IDE代码提示功能，方便开发。
  3. 支持`Yii::trace()`调试信息。
