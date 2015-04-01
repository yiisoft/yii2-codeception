追加のデバッグ出力
==================

Codeception は全ての出力をバッファするため、テストケースの中では単純な `var_dump()` を実行することが出来ません。
その代りに、`Codeception\Util\Debug::debug()` 関数を使って、テストを `--debug` オプションを付けて実行する必要があります。
例えば、

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

そして、コマンド `php codecept.phar run --debug unit/SomeDebugTest` を実行すると、次のような出力が表示されます。

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

更なる説明は、[Yii 2.0 決定版ガイド](https://github.com/yiisoft/yii2/blob/master/docs/guide/test-overview.md) のテストの節を参照してください。
