
## Comparison

### Use [identical comparison](http://php.net/manual/en/language.operators.comparison.php)

**Not good:**

The simple comparison will convert the string into an integer.

```php
$a = '42';
$b = 42;

if ($a != $b) {
    // The expression will always pass
}
```

The comparison `$a != $b` returns `FALSE` but in fact it's `TRUE`!
The string `42` is different than the integer `42`.

**Good:**

The identical comparison will compare type and value.

```php
$a = '42';
$b = 42;

if ($a !== $b) {
    // The expression is verified
}
```

The comparison `$a !== $b` returns `TRUE`.

**[⬆ back to top](#table-of-contents)**

### Null coalescing operator

Null coalescing is a new operator [introduced in PHP 7](https://www.php.net/manual/en/migration70.new-features.php). The null coalescing operator `??` has been added as syntactic sugar for the common case of needing to use a ternary in conjunction with `isset()`. It returns its first operand if it exists and is not `null`; otherwise it returns its second operand.

**Bad:**

```php
if (isset($_GET['name'])) {
    $name = $_GET['name'];
} elseif (isset($_POST['name'])) {
    $name = $_POST['name'];
} else {
    $name = 'nobody';
}
```

**Good:**
```php
$name = $_GET['name'] ?? $_POST['name'] ?? 'nobody';
```

**[⬆ back to top](#table-of-contents)**
