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

Always call actions like this: for creating - `post`, for updating - `patch`, for deleteing - `delete`. Dont add `Action` suffix to action, just write `post()`, `patch()`, `delete()`.

#### Update action

After fetching the object from the database always check if it is not null. If it is null, return content like this:

```php
// Replace the word "object" to the name of the model
$this->setErrorMessageAndExit('Object is not found');
```

#### Delete action

After fetching the object from the database always check if it is not null. If it is null, return content like this:

```php
// Replace the word "object" to the name of the model
$this->setErrorMessageAndExit('Object is not found');
```

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

Don't throw exceptions in domain, if any fields missing. Just set a field to model if it exists.

When setting fields to model cast them to appropriate type based on field purpose.
