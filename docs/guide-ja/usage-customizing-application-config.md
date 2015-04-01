アプリケーションの構成をカスタマイズする
========================================

テストケースごとに異なる構成を指定する必要があるかも知れません。
その場合は、次のようにすることが出来ます。

```php
<?php

SomeConsoleTest extends \yii\codeception\TestCase
{
    // これがアプリケーションの構成としてロードする構成情報ファイル
    public $appConfig = '@app/path/to/my/custom/config/for/test.php';
}
```

`$appConfig` プロパティには、構成情報配列か、または、構成情報配列を返すファイルを示す有効なエイリアスを指定します。
構成情報でアプリケーションのクラスを指定することが出来ます。
例えば、コンソールのコマンドまたは機能をテストする場合、`tests/unit` ディレクトリの下に次のような `_console.php` 構成情報ファイルを作成することが出来ます。

```php
return yii\helpers\ArrayHelper::merge(
    require(__DIR__ . '/../../config/console.php'),
    require(__DIR__ . '/../_config.php'),
    [
        'class' => 'yii\console\Application',
        'components' => [
            // 必要に応じてコンソールコンポーネントをオーバーライド
        ],
    ]
);
```

そして、あなたの `ConsoleTestCase` の中で、次のようにそれを使用します。

```php

use \yii\codeception\TestCase;

class ConsoleTestCase extends TestCase
{
    public $appConfig = '@tests/unit/_console.php';
}
```

他のコンソールテストケースをこの基底の `ConsoleTestCase` から拡張することが出来ます。
