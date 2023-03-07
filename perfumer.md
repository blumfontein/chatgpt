### Controller

Always extend from LayoutController.

Inject service to controller not with constructor, it must be like:

```php
public function action()
{
  $service = $this->s('service');
}
```

Receive request variables with a helper $this->f:

```php
public function action()
{
  $var = $this->f('var');
}
```

Don't return any response object my action method.

Return json content with special helper $this->setContent():

```php
public function action()
{
  $this->setContent([
    'field' => 'content'
  ]);
}
```
