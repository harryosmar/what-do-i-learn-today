# 24 Jan 2019

## PHP Magic Method __invoke

PHP magic method `__invoke` will make the `class instantiation`/`object` can be called(`callable`), just like a `function`.

```php
<?php
/** @var MyClass|callable $myClass */
$myClass = new MyClass();
$myClass(); // This will trigger the cal to magic method __invoke
```

This is usefull when implementing :
- Event Listener
- Middleware stacks call

Example :

We have 2 class stacks : `StackStepOne`, `StackStepTwo`

```php
<?php
class StackStepOne
{
    public function __invoke(array $stack)
    {
        $stack[] = 'one';
        return $stack;
    }
}
```

```php
<?php
class StackStepTwo
{
    public function __invoke(array $stack)
    {
        $stack[] = 'two';
        return $stack;
    }
}
```

We also have `CallableStack`, which is used to stored collection of stack.

```
<?php
class CallableStack
{
    /**
     * @var Callable[]
     */
    private $callableCollection;
    /**
     * @param callable $callable
     *
     * @return self
     */
    public function addCallableToStack(callable $callable): self
    {
        $this->callableCollection[] = $callable;
        return $this;
    }

    public function run()
    {
        $stack = [];
        foreach ($this->callableCollection as $callable) {
            $stack = $callable($stack);
        }
        return $stack;
    }
}
```

This is how the main script look like.

```php
<?php
$callableStack = new CallableStack();

// add stack to collection
$callableStack->addCallableToStack(new StackStepOne())
            ->addCallableToStack(new StackStepTwo());

// run each of stack logic
$callableStack->run(); // return ['one', 'two']
```

Check here for the full source code : [ClassInvokeMethod.php](https://github.com/harryosmar/sample-phpunit-test/blob/invoke-magic-method/tests/unit/ClassInvokeMethod.php)

