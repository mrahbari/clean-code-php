⬆️ [Go to main menu](../README.md) ⬅️ [Previous (Variable)](variables.md) ➡️ [Next (Comparison)](comparison.md)

## Meaningful Names


### Avoid disinformation
Of what type is the account list? String? Array of strings? Array of objects?

**Bad:**
```
$accountList
```

**Good:**
```
$accounts
```

**[⬆ back to top](#meaningful-names)**

### Use pronounceable names
How can you discuss it without sounding like an idiot?

**Bad:**
```
class CstmrRcrd
```

**Good:**
```
class Customer
```

**[⬆ back to top](#meaningful-names)**

### Adjust the length of a name to the size of its scope
Is it obvious outside the class body that WD is an acronym for work days per week?

**Bad:**
```
const WD
```
**Good:**
```
const WORK_DAYS_PER_WEEK
```

**[⬆ back to top](#meaningful-names)**

### Methods should have verb names
```
function postPayment()
function deletePage()
function save()
```

**[⬆ back to top](#meaningful-names)**

### Classes should have noun names
```
class Customer
class WikiPage
class Account
```

**[⬆ back to top](#meaningful-names)**

### Boolean Variables/Functions should have a `is/has/can` prefix.
Clean code reads like prose and these prefixes achieve clear and concise naming.
There is no difference between the naming of variables, e.g. `hasElements`, and functions, e.g. `hasElements()`, except that functions can also answer true/false questions regarding arguments, such as `isFile(path)` or `user.hasAccessTo(file)`.

<!-- Variable Example: `hasElements`, `isUsingIO`<br>
Function examples: `hasElements()`, `isFile(path)`, `user.hasAccessTo(file)` -->

* consider the slightly uncommon prefixes `can` to express abilities/possibilities, e.g. `canWalk`.
* boolean names regarding [Collections](https://en.wikipedia.org/wiki/Collection_(abstract_data_type)) should use `Each/Any` before the prefix, e.g. `isEachLightOn` / `isAnyLightOn`
* prefer positive forms. Use `isActive` not `isInactive` to avoid confusing negations  (`!isInactive`). Same for `hasElements` (not `isEmpty`) and `isEnabled` (not `isDisabled`).
* Avoid further uncommon prefixes, such as `does`, `are`, `was`, `will`, `should`.


| Rule           | Bad ❌                                            | Better ✔    | 
|:---------------|:--------------------------------------------------|:------------|
| Consider `can` | `isAllowedToWalk`, `hasWalkAbility`, `isWalkable` | `canWalk`        |
| Avoid `not`    | `isNotEmpty`, `!isEmpty`                          | `hasElements`    |
| Avoid `are`:   | `areAllLightsOn`, `isAllLightsOn` , `allLightsOn` | `isEachLightOn` |
| Avoid `was/had`| `wasSend`, `hasBeenSent`, `hadArrived`            | `isSent`         |
| Avoid `does`   | `doesUseIO`, `mightUseIO`      | `isUsingIO`, `canUseIO` |

**[⬆ back to top](#meaningful-names)**

