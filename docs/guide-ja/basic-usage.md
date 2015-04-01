基本的な使用方法
================

Codeception のページオブジェクトを使用するとき、同じようなコードがあるのに気付きます。
コードの重複を避けるために、そういうコードを抽出して `BasePage` クラスに置いています。
このクラスからあなたのページオブジェクトを派生させてください。
`yii2-app-basic` と `yii2-app-advanced` のボイラープレートでも、そのようにしています。

単体テストのためには `TestCase` クラスがあり、このクラスがいくつかの共通機能、たとえば、各テスト前のアプリケーションの生成や、各テスト後のアプリケーションの破壊などを保持しています。
このクラスを使って、模擬アプリケーションを構成することが出来ます。
`TestCase` は `Codeception\TestCase\Case` から拡張されているため、Codeception の全てのメソッドやアサーションが利用できます。
あなたのテストで Codeception のモジュールを使ったり、イベントを発生させたりすることも、そのメソッドを使って出来ます。

Codeception のモジュールを取得する
----------------------------------

単体テストの中で Codeception のモジュールやヘルパを使いたいときは、次のようにしてすることが出来ます。

```php
<?php
# あなたの単体テストの中で
$this->getModule('CodeHelper'); # または、その他のモジュール
```

アクターのインスタンスにアクセスして、アクターの全てのメソッドを使うことも出来ます。

```php
<?php
$this->unitTester->someMethodFromModule();
```

Codeception イベント
--------------------

イベントを発生させるためには、次のようにします。

```php
<?php
use Codeception\Event\TestEvent;

public function testSomething()
{
    $this->fire('myevent', new TestEvent($this));
}
```

このイベントは、モジュールおよびヘルパの中でキャッチすることが出来ます。
あなたのテストがグループに属している場合は、例えば ```myevent.somegroup``` のように、イベント名の後にグループ名が付きます。


スペシャルテストメソッドのチェーン
----------------------------------

スペシャルテストメソッドの実行は、例えば、```UserTest``` クラスの場合、次のようになります。

```
tests\unit\models\UserTest::setUpBeforeClass();

    tests\unit\models\UserTest::_before();

        tests\unit\models\UserTest::setUp();

            tests\unit\models\UserTest::testSomething();

        tests\unit\models\UserTest::tearDown();

    tests\unit\models\UserTest::_after();

tests\unit\models\UserTest::tearDownAfterClass();
```

スペシャルテストメソッドを使うときは、その親を呼ぶのを忘れないようにしてください。
