テストのためにコンポーネントを再構成する
========================================

テストのためにコンポーネントを再構成することが出来ます。
この目的のためには、テストケースの `setUp` メソッドの中で、例えば次のようにします。

```php
<?php

use \yii\codeception\TestCase;
use Yii;

class MailTest extends TestCase
{

    protected function setUp()
    {
        // Yii アプリケーションをセットアップする親メソッドを呼ぶことを忘れないように
        parent::setUp();

        Yii::$app->mailer->fileTransportCallback = function ($mailer, $message) {
            return 'testing_message.eml';
        };
    }

}
```

> **Tip**: Yii のコンポーネントとプロパティは、`Yii::configure()` メソッドによっても再構成することが出来ます。

アプリケーションのインスタンスとその隔離性については心配する必要はありません。
なぜなら、テストケースの中で、どのテストメソッドが実行されるときも、[毎回](https://github.com/yiisoft/yii2/blob/master/extensions/codeception/TestCase.php#L31) アプリケーションが生成されるからです。
模擬アプリケーションを作成するためには、別の方法も使えます。
この目的のために、[`mockApplication`](https://github.com/yiisoft/yii2/blob/master/extensions/codeception/TestCase.php#L55) というメソッドをテストケースで使うことが出来ます。
このメソッドは新しいアプリケーションインスタンスを作成して、元のアプリケーションを置き換えます。
この方法は、現在のテストスイートの他のテストメソッドとは異なる構成のアプリケーションを作成する必要があるときに便利です。
例えば、

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
                    // カスタムの構成をここに書く
                ],
            ],
        ]);

        // 期待する結果とアサーションをここに書く
    }

    public function testThree()
    {
        ...
    }

}
```
