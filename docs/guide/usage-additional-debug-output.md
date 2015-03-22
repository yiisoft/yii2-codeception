Additional debug output
=======================

Because of Codeception buffers all output you can't make simple `var_dump()` in the TestCase, instead you need to use
`Codeception\Util\Debug::debug()` function and then run test with `--debug` key, for example:

```php
<?php

use Codeception\Util\Debug;

SomeDebugTest extends \yii\codeception\TestCase
{
    public function testSmth()
    {
        Debug::debug('some string');
        Debug::debug($someArray);
        Debug::debug($someObject);
    }

}
```

Then run command `php codecept.phar run --debug unit/SomeDebugTest` and you will see in output:

```html
  some string

  Array
  (
      [0] => 1
      [1] => 2
      [2] => 3
      [3] => 4
      [4] => 5
  )
  
  yii\web\User Object
  (
      [identityClass] => app\models\User
      [enableAutoLogin] => 
      [loginUrl] => Array
          (
              [0] => site/login
          )
  
      [identityCookie] => Array
          (
              [name] => _identity
              [httpOnly] => 1
          )
  
      [authTimeout] => 
      [autoRenewCookie] => 1
      [idParam] => __id
      [authTimeoutParam] => __expire
      [returnUrlParam] => __returnUrl
      [_access:yii\web\User:private] => Array
          (
          )
  
      [_identity:yii\web\User:private] => 
      [_events:yii\base\Component:private] => 
      [_behaviors:yii\base\Component:private] => 
  )

```

For further instructions refer to the testing section in the [Yii Definitive Guide](https://github.com/yiisoft/yii2/blob/master/docs/guide/test-overview.md).
