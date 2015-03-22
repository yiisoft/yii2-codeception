Customizing application config
==============================

You may need to specify different configuration files per test cases, to do this you can make it like the following:

```php
<?php

SomeConsoleTest extends \yii\codeception\TestCase
{
    // this is the config file to load as application config
    public $appConfig = '@app/path/to/my/custom/config/for/test.php';
}
```

The `$appConfig` property could be an array or a valid alias, pointing to the file that returns a config array. You can specify
application class in the config, for example for testing console commands or features you can create `_console.php` config under
`tests/unit` directory like this:

```php
return yii\helpers\ArrayHelper::merge(
    require(__DIR__ . '/../../config/console.php'),
    require(__DIR__ . '/../_config.php'),
    [
        'class' => 'yii\console\Application',
        'components' => [
            //override console components if needed
        ],
    ]
);
```

and then just use your `ConsoleTestCase` like the following:

```php

use \yii\codeception\TestCase;

class ConsoleTestCase extends TestCase
{
    public $appConfig = '@tests/unit/_console.php';
}
```

You can extend other console test cases from this basic `ConsoleTestCase`.