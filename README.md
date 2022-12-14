# Clean Code PHP

Clean code is code that is `easy to understand` and `easy to change`.
Even bad code can function. But if code isn't clean, it can bring a development organization to its knees.

## Table of Contents

  1. [Introduction](./htmls/introdction.md)
  2. [Variables](./htmls/variables.md)
     * [Use meaningful and pronounceable variable names](./htmls/variables.md#use-meaningful-and-pronounceable-variable-names)
     * [Use the same vocabulary for the same type of variable](./htmls/variables.md#use-the-same-vocabulary-for-the-same-type-of-variable)
     * [Use searchable names (part 1)](./htmls/variables.md#use-searchable-names-part-1)
     * [Use searchable names (part 2)](./htmls/variables.md#use-searchable-names-part-2)
     * [Avoid nesting too deeply and return early (part 1)](./htmls/variables.md#avoid-nesting-too-deeply-and-return-early-part-1)
     * [Avoid nesting too deeply and return early (part 2)](./htmls/variables.md#avoid-nesting-too-deeply-and-return-early-part-2)
     * [Avoid Mental Mapping](./htmls/variables.md#avoid-mental-mapping)
     * [Don't add unneeded context](./htmls/variables.md#dont-add-unneeded-context)
  3. [Naming](./htmls/naming.md)
     * [Avoid disinformation]()
     * [Adjust the length of a name to the size of its scope]()
     * [Methods should have verb names]()
     * [Classes should have noun names]()
     * [Boolean Variables/Functions should have a is/has/can prefix.]()
  4. [Comparison](./htmls/comparison.md#comparison)
     * [Use identical comparison](./htmls/comparison.md#use-identical-comparison)
     * [Null coalescing operator](./htmls/comparison.md#null-coalescing-operator)
  5. [Comments](./htmls/comments.md)
     * [Multiline Comment vs. Single-Line Comment]()
     * [Nonlocal Comment]()
     * [Never, Ever, Ever Comment Out Code!]()
     * [Don’t Make Comments Harder Than the Code]()
     * [Never Comment the Obvious]()
     * [Always try to explain yourself in code]()
     * [Avoid redundant comments]()
     * [Give up mandated comments]()
     * [Don't make noise]()
     * [Avoid closing brace comments]()
     * [Avoid position markers]()
     * [Avoid HTML comments]()
     * [Don't give too much information]()
     * [Explaining Unclear Code]()
     * [TODO Comments]()
     * [Use reference links for codes]()
  6. [Functions](./htmls/functions.md)
     * [Use default arguments instead of short circuiting or conditionals](./htmls/functions.md#use-default-arguments-instead-of-short-circuiting-or-conditionals)
     * [Function arguments (2 or fewer ideally)](./htmls/functions.md#function-arguments-2-or-fewer-ideally)
     * [Function names should say what they do](./htmls/functions.md#function-names-should-say-what-they-do)
     * [Functions should only be one level of abstraction](./htmls/functions.md#functions-should-only-be-one-level-of-abstraction)
     * [Don't use flags as function parameters](./htmls/functions.md#dont-use-flags-as-function-parameters)
     * [Avoid Side Effects](./htmls/functions.md#avoid-side-effects)
     * [Don't write to global functions](./htmls/functions.md#dont-write-to-global-functions)
     * [Encapsulate conditionals](./htmls/functions.md#encapsulate-conditionals)
     * [Avoid negative conditionals](./htmls/functions.md#avoid-negative-conditionals)
     * [Avoid conditionals](./htmls/functions.md#avoid-conditionals)
     * [Avoid type-checking (part 1)](./htmls/functions.md#avoid-type-checking-part-1)
     * [Avoid type-checking (part 2)](./htmls/functions.md#avoid-type-checking-part-2)
     * [Remove dead code](./htmls/functions.md#remove-dead-code)
  7. [Objects and Data Structures](./htmls/objects.md)
     * [Use object encapsulation](./htmls/objects.md#use-object-encapsulation)
     * [Make objects have private/protected members](./htmls/objects.md#make-objects-have-privateprotected-members)
  8. [Classes](./htmls/classes.md)
     * [Prefer composition over inheritance](./htmls/classes.md#prefer-composition-over-inheritance)
     * [Avoid fluent interfaces](./htmls/classes.md#avoid-fluent-interfaces)
     * [Prefer final classes](./htmls/classes.md#prefer-final-classes)
  9. [SOLID](./htmls/solid.md)
     * [Single Responsibility Principle (SRP)](./htmls/solid.md#single-responsibility-principle-srp)
     * [Open/Closed Principle (OCP)](./htmls/solid.md#openclosed-principle-ocp)
     * [Liskov Substitution Principle (LSP)](./htmls/solid.md#liskov-substitution-principle-lsp)
     * [Interface Segregation Principle (ISP)](./htmls/solid.md#interface-segregation-principle-isp)
     * [Dependency Inversion Principle (DIP)](./htmls/solid.md#dependency-inversion-principle-dip)
  10. [Don’t repeat yourself (DRY)](./htmls/dry.md)
  


