⬆️ [Go to main menu](../README.md) ⬅️ [Previous (Introduction)](introdction.md) ➡️ [Next (Naming)](naming.md)

## Variables (#table-of-contents)

### Use meaningful and pronounceable variable names

**Bad:**

```php
$ymdstr = $moment->format('y-m-d');
```

**Good:**

```php
$currentDate = $moment->format('y-m-d');
```

**[⬆ back to top](#table-of-contents)**

### Use the same vocabulary for the same type of variable

**Bad:**

```php
getUserInfo();
getUserData();
getUserRecord();
getUserProfile();
```

**Good:**

```php
getUser();
```

**[⬆ back to top](#table-of-contents)**

### Use searchable names (part 1)

We will read more code than we will ever write. It's important that the code we do write is
readable and searchable. By *not* naming variables that end up being meaningful for
understanding our program, we hurt our readers.
Make your names searchable.
[Sample Link](https://gist.github.com/ewwink/f14474fd955801153c47)


**Bad:**

```php
// What the heck is 448 for?
$result = $serializer->serialize($data, 448);
```

**Good:**

```php
$json = $serializer->serialize($data, JSON_UNESCAPED_SLASHES | JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
```

### Use searchable names (part 2)

**Bad:**

```php
class User
{
    // What the heck is 7 for?
    public $access = 7;
}

// What the heck is 4 for?
if ($user->access & 4) {
    // ...
}
```

**Good:**

```php
class User
{
    public const ACCESS_READ = 1;

    public const ACCESS_CREATE = 2;

    public const ACCESS_UPDATE = 4;

    public const ACCESS_DELETE = 8;

    // User as default can read, create and update something
    public $access = self::ACCESS_READ | self::ACCESS_CREATE | self::ACCESS_UPDATE;
}

if ($user->access & User::ACCESS_UPDATE) {
    // do edit ...
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid nesting too deeply and return early (part 1)

Too many if-else statements can make your code hard to follow. Explicit is better
than implicit.

**Bad:**

```php
function isShopOpen($day): bool
{
    if ($day) {
        if (is_string($day)) {
            $day = strtolower($day);
            if ($day === 'friday') {
                return true;
            } elseif ($day === 'saturday') {
                return true;
            } elseif ($day === 'sunday') {
                return true;
            }
            return false;
        }
        return false;
    }
    return false;
}
```

**Good:**

```php
function isShopOpen(string $day): bool
{
    if (empty($day)) {
        return false;
    }

    $openingDays = ['friday', 'saturday', 'sunday'];

    return in_array(strtolower($day), $openingDays, true);
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid nesting too deeply and return early (part 2)

**Bad:**

```php
function fibonacci(int $n)
{
    if ($n < 50) {
        if ($n !== 0) {
            if ($n !== 1) {
                return fibonacci($n - 1) + fibonacci($n - 2);
            }
            return 1;
        }
        return 0;
    }
    return 'Not supported';
}
```

**Good:**

```php
function fibonacci(int $n): int
{
    if ($n === 0 || $n === 1) {
        return $n;
    }

    if ($n >= 50) {
        throw new Exception('Not supported');
    }

    return fibonacci($n - 1) + fibonacci($n - 2);
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid Mental Mapping

Don’t force the reader of your code to translate what the variable means.
Explicit is better than implicit.

**Bad:**

```php
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // Wait, what is `$li` for again?
    dispatch($li);
}
```

**Good:**

```php
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```

**[⬆ back to top](#table-of-contents)**

### Don't add unneeded context

If your class/object name tells you something, don't repeat that in your
variable name.

**Bad:**

```php
class Car
{
    public $carMake;

    public $carModel;

    public $carColor;

    //...
}
```

**Good:**

```php
class Car
{
    public $make;

    public $model;

    public $color;

    //...
}
```
