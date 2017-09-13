# 约定

- 别名或参数约定

   `@wocenter`：WoCenter核心的所在路径，实际路径为`./vendor/wonail/wocenter`。

   `{app}`：当前应用的ID，从`Yii::$app->id`处获得，如：`backend`。

   `@app`：当前应用的所在路径，实际路径为`/rootPath/{app}`，参数说明：

   - `rootPath`：项目根目录的所在路径，如：`/home/www/wocenter_advanced`。
   - `{app}`：见上述。

      以上面的参数为例，当前应用的实际路径为`/home/www/wocenter_advanced/backend`。

   `@backend`：`backend`应用的所在路径，类似的可能有`@frontend`、`@console`等。

   `{theme}`：当前系统使用的主题名称，可从`Yii::$app->getView()->themeName`处获得，如：`adminlte`。

>   WoCenter一直坚持着对二次开发友好性和便捷性原则的基础上开发所有功能，建议开发者同样以此为目标进行开发。
不论是良好的代码注释还是对IDE的友好支持，于人于己都能为日后的开发带来更好的体验、维护和帮助。