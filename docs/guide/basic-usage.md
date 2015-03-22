Basic Usage
===========

When using codeception page-objects they have some similar code, this code was extracted and put into the `BasePage`
class to reduce code duplication. Simply extend your page object from this class, like it is done in `yii2-app-basic` and
`yii2-app-advanced` boilerplates.

For unit testing there is a `TestCase` class which holds some common features like application creation before each test
and application destroy after each test. You can configure a mock application using this class.
`TestCase` is extended from `Codeception\TestCase\Case` so all methods and assertions are available.
You may use codeception modules and fire events in your test, just use methods:

Getting Codeception modules
---------------------------

If you want to use codeception modules and helpers in your unit tests, you can do it like this:

```php
<?php
#in your unit-test
$this->getModule('CodeHelper'); #or some other module
```

You also can use all actor methods by accessing actor instance like:

```php
<?php
$this->unitTester->someMethodFromModule();
```
Codeception events
------------------

To fire event do this:

```php
<?php
use Codeception\Event\TestEvent;

public function testSomething()
{
    $this->fire('myevent', new TestEvent($this));
}
```
this event can be catched in modules and helpers. If your test is in the group, then event name will be followed by the groupname, 
for example ```myevent.somegroup```.


Special test method chaining
----------------------------

Execution of special tests methods is (for example on ```UserTest``` class):

```
tests\unit\models\UserTest::setUpBeforeClass();

    tests\unit\models\UserTest::_before();

        tests\unit\models\UserTest::setUp();

            tests\unit\models\UserTest::testSomething();

        tests\unit\models\UserTest::tearDown();

    tests\unit\models\UserTest::_after();

tests\unit\models\UserTest::tearDownAfterClass();
```

If you use special methods dont forget to call its parent.
