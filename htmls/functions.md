⬆️ [Go to main menu](../README.md) ⬅️ [Previous (Comments)](comments.md) ➡️ [Next (Objects and Data Structures)](objects.md)

## Functions

### Functions should be small
Functions should hardly ever be 20 lines long.
```
public function getPaginator(Image $image, int $offset): Paginator
{
    $query = $this->createQueryBuilder('c')
    ->andWhere('c.image = :image')
    ->setParameter('image', $image)
    ->orderBy('c.createdAt', 'DESC')
    ->setMaxResults(self::PAGINATOR_PER_PAGE)
    ->setFirstResult($offset)
    ->getQuery()
    ;

    return new Paginator($query);
}
```

**[⬆ back to top](#functions)**

### Functions should do one thing
Function is doing more than "one thing" if you can extract another function from it with a name that is not merely a restatement of its implementation.

**Bad:**
```
public function pay(EmployeeRepository $employeeRepository): void
{
    foreach ($employeeRepository->findAll() as $employee) {
        if ($employee->isPayday()) {
            $pay = $employee->calculatePay();
            $employee->deliverPay($pay);
        }
    }
}
```

**Good:**
```
public function pay(EmployeeRepository $employeeRepository): void
{
    foreach ($employeeRepository->findAll() as $employee) {
        $this->payIfNecessary($employee);
    }
}

protected function payIfNecessary(Employee $employee): void
{
    if ($employee->isPayday())
        $this->calculateAndDeliverPay($employee);
}

protected function calculateAndDeliverPay(Employee $employee): void
{
    $pay = $employee->calculatePay();
    $employee->deliverPay($pay);
}
```

**[⬆ back to top](#functions)**

### Follow the step-down rule
We want every function to be followed by those at the next level of abstraction so that `we can read code from top to bottom`.
```
// First level of abstraction
public function pay(EmployeeRepository $employeeRepository): void
{
    foreach ($employeeRepository->findAll() as $employee) {
        $this->payIfNecessary($employee);
    }
}

// Second level of abstraction
protected function payIfNecessary(Employee $employee): void
{
    if ($employee->isPayday())
        $this->calculateAndDeliverPay($employee);
}

// Third level of abstraction
protected function calculateAndDeliverPay(Employee $employee): void
{
    $pay = $employee->calculatePay();
    $employee->deliverPay($pay);
}
```

**[⬆ back to top](#functions)**

### Avoid Side Effects
The side effect is the call to session_start(). The checkPassword function, by its name, says that it checks the password. The name does not imply that it initializes the session.
```
public function checkPassword(string $password): bool
{
    session_start();
```

### Use default arguments instead of short-circuiting or conditionals

**Not good:**

This is not good because `$breweryName` can be `NULL`.

```php
function createMicrobrewery($breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**Not bad:**

This opinion is more understandable than the previous version, but it better controls the value of the variable.

```php
function createMicrobrewery($name = null): void
{
    $breweryName = $name ?: 'Hipster Brew Co.';
    // ...
}
```

**Good:**

You can use [type hinting](https://www.php.net/manual/en/language.types.declarations.php) and be sure that the `$breweryName` will not be `NULL`.

```php
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**[⬆ back to top](#functions)**

### Function arguments (2 or fewer ideally)

Limiting the amount of function parameters is incredibly important because it makes
testing your function easier. Having more than three leads to a combinatorial explosion
where you have to test tons of different cases with each separate argument.

Zero arguments is the ideal case. One or two arguments is ok, and three should be avoided.
Anything more than that should be consolidated. Usually, if you have more than two
arguments then your function is trying to do too much. In cases where it's not, most
of the time a higher-level object will suffice as an argument.

**Bad:**

```php
class Questionnaire
{
    public function __construct(
        string $firstname,
        string $lastname,
        string $patronymic,
        string $region,
        string $district,
        string $city,
        string $phone,
        string $email
    ) {
        // ...
    }
}
```

**Good:**

```php
class Name
{
    private $firstname;

    private $lastname;

    private $patronymic;

    public function __construct(string $firstname, string $lastname, string $patronymic)
    {
        $this->firstname = $firstname;
        $this->lastname = $lastname;
        $this->patronymic = $patronymic;
    }

    // getters ...
}

class City
{
    private $region;

    private $district;

    private $city;

    public function __construct(string $region, string $district, string $city)
    {
        $this->region = $region;
        $this->district = $district;
        $this->city = $city;
    }

    // getters ...
}

class Contact
{
    private $phone;

    private $email;

    public function __construct(string $phone, string $email)
    {
        $this->phone = $phone;
        $this->email = $email;
    }

    // getters ...
}

class Questionnaire
{
    public function __construct(Name $name, City $city, Contact $contact)
    {
        // ...
    }
}
```

**[⬆ back to top](#functions)**

### Function names should say what they do

**Bad:**

```php
class Email
{
    //...

    public function handle(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// What is this? A handle for the message? Are we writing to a file now?
$message->handle();
```

**Good:**

```php
class Email
{
    //...

    public function send(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// Clear and obvious
$message->send();
```

**[⬆ back to top](#functions)**

### Functions should only be one level of abstraction

When you have more than one level of abstraction your function is usually
doing too much. Splitting up functions leads to usability and easier
testing.`It should'n be complex. Use seperate class and resolve them to follow DI`

**Bad:**

```php
function parseBetterPHPAlternative(string $code): void
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            // ...
        }
    }

    $ast = [];
    foreach ($tokens as $token) {
        // lex...
    }

    foreach ($ast as $node) {
        // parse...
    }
}
```

**Bad too:**

We have carried out some functionality, but the `parseBetterPHPAlternative()` function is still very complex and not testable.

```php
function tokenize(string $code): array
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            $tokens[] = /* ... */;
        }
    }

    return $tokens;
}

function lexer(array $tokens): array
{
    $ast = [];
    foreach ($tokens as $token) {
        $ast[] = /* ... */;
    }

    return $ast;
}

function parseBetterPHPAlternative(string $code): void
{
    $tokens = tokenize($code);
    $ast = lexer($tokens);
    foreach ($ast as $node) {
        // parse...
    }
}
```

**Good:**

The best solution is move out the dependencies of `parseBetterPHPAlternative()` function.

```php
class Tokenizer
{
    public function tokenize(string $code): array
    {
        $regexes = [
            // ...
        ];

        $statements = explode(' ', $code);
        $tokens = [];
        foreach ($regexes as $regex) {
            foreach ($statements as $statement) {
                $tokens[] = /* ... */;
            }
        }

        return $tokens;
    }
}

class Lexer
{
    public function lexify(array $tokens): array
    {
        $ast = [];
        foreach ($tokens as $token) {
            $ast[] = /* ... */;
        }

        return $ast;
    }
}

class BetterPHPAlternative
{
    private $tokenizer;
    private $lexer;

    public function __construct(Tokenizer $tokenizer, Lexer $lexer)
    {
        $this->tokenizer = $tokenizer;
        $this->lexer = $lexer;
    }

    public function parse(string $code): void
    {
        $tokens = $this->tokenizer->tokenize($code);
        $ast = $this->lexer->lexify($tokens);
        foreach ($ast as $node) {
            // parse...
        }
    }
}
```

**[⬆ back to top](#functions)**

### Don't use flags as function parameters

Flags tell your user that this function does more than one thing. Functions should
do one thing. Split out your functions if they are following different code paths
based on a boolean.

**Bad:**

```php
function createFile(string $name, bool $temp = false): void
{
    if ($temp) {
        touch('./temp/' . $name);
    } else {
        touch($name);
    }
}
```

**Good:**

```php
function createFile(string $name): void
{
    touch($name);
}

function createTempFile(string $name): void
{
    touch('./temp/' . $name);
}
```

**[⬆ back to top](#functions)**

### Don't write to global functions

Polluting globals is a bad practice in many languages because you could clash with another
library and the user of your API would be none-the-wiser until they get an exception in
production. Let's think about an example: what if you wanted to have configuration array?
You could write global function like `config()`, but it could clash with another library
that tried to do the same thing.

**Bad:**

```php
function config(): array
{
    return [
        'foo' => 'bar',
    ];
}
```

**Good:**

```php
class Configuration
{
    private $configuration = [];

    public function __construct(array $configuration)
    {
        $this->configuration = $configuration;
    }

    public function get(string $key): ?string
    {
        // null coalescing operator
        return $this->configuration[$key] ?? null;
    }
}
```

Load configuration and create instance of `Configuration` class

```php
$configuration = new Configuration([
    'foo' => 'bar',
]);
```

And now you must use instance of `Configuration` in your application.

**[⬆ back to top](#functions)**

### Encapsulate conditionals

**Bad:**

```php
if ($article->state === 'published') {
    // ...
}
```

**Good:**

```php
if ($article->isPublished()) {
    // ...
}
```

**[⬆ back to top](#functions)**

### Avoid negative conditionals

**Bad:**

```php
function isDOMNodeNotPresent(DOMNode $node): bool
{
    // ...
}

if (! isDOMNodeNotPresent($node)) {
    // ...
}
```

**Good:**

```php
function isDOMNodePresent(DOMNode $node): bool
{
    // ...
}

if (isDOMNodePresent($node)) {
    // ...
}
```

**[⬆ back to top](#functions)**

### Avoid conditionals

This seems like an impossible task. Upon first hearing this, most people say,
"how am I supposed to do anything without an `if` statement?" The answer is that
you can use polymorphism to achieve the same task in many cases. The second
question is usually, "well that's great but why would I want to do that?" The
answer is a previous clean code concept we learned: a function should only do
one thing. When you have classes and functions that have `if` statements, you
are telling your user that your function does more than one thing. Remember,
just do one thing.

**Bad:**

```php
class Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        switch ($this->type) {
            case '777':
                return $this->getMaxAltitude() - $this->getPassengerCount();
            case 'Air Force One':
                return $this->getMaxAltitude();
            case 'Cessna':
                return $this->getMaxAltitude() - $this->getFuelExpenditure();
        }
    }
}
```

**Good:**

```php
interface Airplane
{
    // ...

    public function getCruisingAltitude(): int;
}

class Boeing777 implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getPassengerCount();
    }
}

class AirForceOne implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude();
    }
}

class Cessna implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getFuelExpenditure();
    }
}
```
The normal approach to use while working with this kind of scenario would be to use the **Design Pattern**.


**[⬆ back to top](#functions)**

### Avoid type-checking (part 1)

PHP is untyped, which means your functions can take any type of argument.
Sometimes you are bitten by this freedom, and it becomes tempting to do
type-checking in your functions. There are many ways to avoid having to do this.
The first thing to consider is consistent APIs.

**Bad:**

```php
function travelToTexas($vehicle): void
{
    if ($vehicle instanceof Bicycle) {
        $vehicle->pedalTo(new Location('texas'));
    } elseif ($vehicle instanceof Car) {
        $vehicle->driveTo(new Location('texas'));
    }
}
```

**Good:**

```php
function travelToTexas(Vehicle $vehicle): void
{
    $vehicle->travelTo(new Location('texas'));
}
```

```php
class Vehicle
{
    public function travelTo(?string $source)
    {
        switch ($source) {
            case VehicleEnum::BICYCLE:
                //do something
            case VehicleEnum::CAR
                //do something
            default :
                ////
        }
    }
}
```
The normal approach to use while working with this kind of scenario would be to use the **Design Pattern**.

**[⬆ back to top](#functions)**

### Avoid type-checking (part 2)

If you are working with basic primitive values like strings, integers, and arrays,
and you use PHP 7+ and you can't use polymorphism but you still feel the need to
type-check, you should consider
[type declaration](https://www.php.net/manual/en/language.types.declarations.php)
or strict mode. It provides you with static typing on top of standard PHP syntax.
The problem with manually type-checking is that doing it will require so much
extra verbiage that the faux "type-safety" you get doesn't make up for the lost
readability. Keep your PHP clean, write good tests, and have good code reviews.
Otherwise, do all of that but with PHP strict type declaration or strict mode.

**Bad:**

```php
function combine($val1, $val2): int
{
    if (! is_numeric($val1) || ! is_numeric($val2)) {
        throw new Exception('Must be of type Number');
    }

    return $val1 + $val2;
}
```

**Good:**

```php
function combine(int $val1, int $val2): int
{
    return $val1 + $val2;
}
```

**[⬆ back to top](#functions)**

### Remove dead code

Dead code is just as bad as duplicate code. There's no reason to keep it in
your codebase. `If it's not being called, get rid of it!` It will still be safe
in your version history if you still need it.

**Bad:**

```php
function oldRequestModule(string $url): void
{
    // ...
}

function newRequestModule(string $url): void
{
    // ...
}

$request = newRequestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**Good:**

```php
function requestModule(string $url): void
{
    // ...
}

$request = requestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**[⬆ back to top](#functions)**

