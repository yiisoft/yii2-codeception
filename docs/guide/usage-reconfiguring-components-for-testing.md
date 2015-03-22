Reconfiguring components for testing
====================================

You can reconfigure a component for testing, for this purpose in your `setUp` method of your test case 
you can do this for example:

```php
<?php

use \yii\codeception\TestCase;
use Yii;

class MailTest extends TestCase
{

    protected function setUp()
    {
        // don't forget to call parent method that will setup Yii application
        parent::setUp();

        Yii::$app->mailer->fileTransportCallback = function ($mailer, $message) {
            return 'testing_message.eml';
        };
    }

}
```

> **Tip**: You also can reconfigure Yii components and properties with method `Yii::configure()`.

You don't need to worry about application instances and isolation because application will be created [each time](https://github.com/yiisoft/yii2/blob/master/extensions/codeception/TestCase.php#L31) before any of test method will be executed in test case.
You can mock application in a different way. For this purposes you have method [`mockApplication`](https://github.com/yiisoft/yii2/blob/master/extensions/codeception/TestCase.php#L55) available in your test case.
This method creates new application instance and replaces old one with it and is handy when you need to create application with a config that is different from other test methods in the current test suite. For example:

```php

use \yii\codeception\TestCase;

class SomeMyTest extends TestCase
{

    public function testOne()
    {
        ...
    }

    public function testTwo()
    {
        $this->mockApplication([
            'language' => 'ru-RU',
            'components' => [
                'db' => [
                    //your custom configuration here
                ],
            ],
        ]);

        //your expectations and assertions goes here
    }

    public function testThree()
    {
        ...
    }

}
```
