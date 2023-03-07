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

Always call actions like this: for creating - `post`, for updating - `patch`, for deleteing - `delete`.

### ORM

Use always Propel 2 ORM.

### Domain

Domain is a class which contains saving models to database.

Always call domain when saving something to database.

Inject domain to controller like this: $this->s('domain'). If model is Human, then domain processing Human objects is called HumanDomain, and injected as 'domain.human' service.

Domain MUST have `create`, `update` and `delete` methods.

`Create` method must receive an array of data and save fields to model one-by-one, with checking that certain field exists in the data array. `Create` method returns created object.

`Update` method must receive an object to update, and an array of data and save fields to model one-by-one, with checking that certain field exists in the data array.

`Delete` method must receive an object and deletes it.
