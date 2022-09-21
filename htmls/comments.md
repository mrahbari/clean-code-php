Comments

Multiline Comment vs. Single-Line Comment
Whenever possible, try to write long comments as multiline comments.

**Bad:**
```
// This is a long comment
// Which is written as multiple single line comment.
// Always remember it's bad
```

**Good:**
```
/*
This is also another comment which is long
but this comment is written as a multi-line comment
*/
```

### Nonlocal Comment
Here’s an example of bad comment. The default time out is 5000, but it doesn’t specify where this value was set.
```
// if timeout is not set then it defaults to 5000
int timeout = 2000;
```

Never comment about some code that’s not present. Instead, try to provide some context.
```
// if timeout is not set then it defaults to 5000 which is defined in proerties file
int timeout = 2000;
```

### Never, Ever, Ever Comment Out Code!
This is the ugliest practice of all. We sometimes comment out code, thinking we (or someone else) might need that piece of code later.
```
// if(something){
//    doSomething()
// }
```

### Don’t Make Comments Harder Than the Code
Never comment something harder than the code itself. Like the following one:
```
// this is a utility function that provides us the proper validation
// for date and time and check the logic
boolean checkIfDateIsValid()
```

### Never Comment the Obvious
Some comments are so obvious that it’s ridiculous to comment them out.
```
try{
doSomething()
}catch{
// exception caught
}
```


### Always try to explain yourself in code
It only takes a few seconds to clear the majority of your thoughts in code.
In many cases, it’s all about developing a method that tells the same thing as your statement.

Apparently, many programmers have found it uncommon, if ever, to be a good way to describe code. It’s clearly wrong. What are you going to want to see? The following:
```
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) &&
(employee.age > 65))
```
Or you can avoid comment using a function with descriptive as below:
```
if (employee.isEligibleForFullBenefits())
```

### Avoid redundant comments
A comment is redundant if it describes something that adequately describes itself. Comments should say things that the code cannot say for itself.
```
// create directory recursively and save file content
mkdir($uploadDirectory, 0777, true);  
file_put_contents($uploadDirectory.'/'.$filename, $content));
```

### Give up mandated comments
It is just plain silly to have a rule that says that every function and variable must have a comment. Comments like this just clutter up the code.
```
/**
* Returns the static model of the specified AR class.
* @return Order the static model class
  */
  public static function model($className=__CLASS__)
  {
  return parent::model($className);
  }
```

### Don't make noise
  Noise comments restate the obvious and provide no new information. 
```  
/**
* Check whether it is automated request
* @return boolean whether it is automated request
  */
  public function isAutoRequest(): bool
  {
  return isset($_REQUEST['VK_AUTO']) && $_REQUEST['VK_AUTO'] == 'Y';
  }
```

### Avoid closing brace comments
  If you find yourself wanting to mark your closing braces, try to shorten your functions instead.
```  
            $newline .= $c;
        } // end of for
    $output .= $newline . $eol;
  } // end of while
  return $output;
  ```

### Avoid position markers
  There are rare times when they make sense, but in general they are clutter that should be eliminated.
```
  /////////////////////////////////////////////////
  // PROPERTIES, PRIVATE AND PROTECTED
  /////////////////////////////////////////////////
  private $smtp_conn;
  private $error;
  private $helo_rply;
```

### Avoid HTML comments
  It makes the comments hard to read in the one place where they should be easy to read—the editor/IDE.
```
/**
* To use this widget, you may insert the following code in a view:
* <pre>
* $this->widget('ext.widgets.password.XPasswordStrength', [
*     'model' => $model,
*     'attribute' => 'password'
* ]);
* </pre>
*/
```

### Don't give too much information
  Don’t put interesting historical discussions or irrelevant descriptions of details into your comments.
```
  // The encoding process represents 24-bit groups of input bits as
  // output strings of 4 encoded characters. Proceeding from left to right
  // a 24-bit input group is formed by concatenating 3 8-bit input groups.
  // These 24 bits are then treated as 4 concatenated 6-bit groups ...
```  

### Explaining Unclear Code
```
int timeout = 5; // timeout in seconds
```

### TODO Comments
When there are jobs that the programmer thinks should be done, but for some reason can’t do at the moment, it’s good to leave some “To do” notes in the form of //TODO comments. //TODO comments can give a message about what the function’s future should be.
TODOs are a nice IDE feature, but it’s recommended not to check them in, so fix them before
otherwise, they become DONTDOs

```
//TODO: calculation formula must be revise ASAP.
```
