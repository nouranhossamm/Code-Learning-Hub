#  PHP Notes

A structured reference covering PHP fundamentals — output, data types, strings, arrays, variables, constants, and operators.

---

##  Table of Contents

###  1. Getting Started
- [1.1 Echo](#11-echo)
- [1.2 Print](#12-print)
- [1.3 Comments](#13-comments)

###  2. Data Types & Conversion
- [2.1 PHP Data Types](#21-php-data-types)
- [2.2 gettype()](#22-gettype)
- [2.3 Type Juggling & Automatic Type Conversion](#23-type-juggling--automatic-type-conversion)
- [2.4 Type Casting](#24-type-casting)
- [2.5 var_dump()](#25-var_dump)

###  3. Strings
- [3.1 Strings and Escaping](#31-strings-and-escaping)
- [3.2 nl2br()](#32-nl2br)
- [3.3 Heredoc & Nowdoc](#33-heredoc--nowdoc)
- [3.4 Difference Between ' ' and " " with Variables](#34-difference-between---and---with-variables)
- [3.5 String Operators: Concatenation and `.=`](#35-string-operators-concatenation-and-)

###  4. Arrays
- [4.1 print_r()](#41-print_r)
- [4.2 Array with Keys](#42-array-with-keys)
- [4.3 Array without Keys](#43-array-without-keys)
- [4.4 Array with One Key](#44-array-with-one-key)
- [4.5 Array Value Override](#45-array-value-override)

###  5. Variables & References
- [5.1 The Rules of Naming a Variable](#51-the-rules-of-naming-a-variable)
- [5.2 Loosely Typed Languages](#52-loosely-typed-languages)
- [5.3 Variable Variables and " "](#53-variable-variables-and--)
- [5.4 Assign Variable by Reference](#54-assign-variable-by-reference)
- [5.5 References Aren't Pointers](#55-references-arent-pointers)
- [5.6 Predefined Variables](#56-predefined-variables)

###  6. Constants
- [6.1 Constants in PHP](#61-constants-in-php)
- [6.2 Predefined Constants](#62-predefined-constants)
- [6.3 Magic Constants](#63-magic-constants)
- [6.4 Reserved Words](#64-reserved-words)

###  7. Operators
- [7.1 Arithmetic Operators](#71-arithmetic-operators)
- [7.2 Identity & Negation](#72-identity--negation)
- [7.3 Assignment Operators](#73-assignment-operators)
- [7.4 Comparison Operators](#74-comparison-operators)
- [7.5 The `<>` Operator](#75-the--operator)
- [7.6 Spaceship Operator (`<=>`)](#76-spaceship-operator-)
- [7.7 Strings with Comparison Operators](#77-strings-with-comparison-operators)
- [7.8 Pre and Post Increment & Decrement Operators](#78-pre-and-post-increment--decrement-operators)
- [7.9 Logical Operators](#79-logical-operators)
- [7.10 Xor Operator](#710-xor-operator)

---

##  1. Getting Started

### 1.1 Echo
Displays one or more strings, variables, or HTML content to the browser.

```php
<?php
echo "Hello, World!";
echo "<br>";
echo "Welcome to PHP!";
?>
```

### 1.2 Print
Displays a single string or variable to the browser. It works similarly to `echo`, but can only output **one** argument.

```php
<?php
print "Hello, World!";
?>
```

### 1.3 Comments
Comments explain code, improve readability, or temporarily disable code during testing. They are ignored by the PHP interpreter.

**Single-line** — uses `//` or `#`:
```php
<?php
// This is a single-line comment
echo "Hello, World!";
# This is also a single-line comment
echo "Welcome to PHP!";
?>
```

**Multi-line** — uses `/* */`:
```php
<?php
/*
This is a
multi-line comment.
*/
echo "Hello, World!";
?>
```


---

##  2. Data Types & Conversion

### 2.1 PHP Data Types
Data types define the kind of value a variable can store.

| # | Type | Description | Example |
|---|------|-------------|---------|
| 1 | **String** | A sequence of characters | `$name = "Nouran";` |
| 2 | **Integer** | Whole numbers, no decimals | `$age = 24;` |
| 3 | **Float (Double)** | Numbers with decimal points | `$price = 99.99;` |
| 4 | **Boolean** | `true` or `false` | `$isStudent = true;` |
| 5 | **Array** | Multiple values in one variable | `$colors = ["Red","Green","Blue"];` |
| 6 | **Object** | Data & methods from a class | `$car = new Car();` |
| 7 | **NULL** | A variable with no value | `$value = null;` |
| 8 | **Resource** | Reference to an external resource (file, DB connection) | `$file = fopen("f.txt","r");` |

```php
<?php
class Car {
    public $brand = "Toyota";
}
$car = new Car();
echo $car->brand;

$file = fopen("example.txt", "r");
var_dump($file);
fclose($file);
?>
```

### 2.2 gettype()
Returns the current data type of a variable as a string (`"integer"`, `"string"`, `"boolean"`, `"double"`, `"array"`, `"object"`, `"NULL"`). Useful for debugging since PHP is loosely typed.

```php
<?php
$a = 10;
$b = "Hello";
$c = 3.14;
$d = true;
$e = null;
$f = [1, 2, 3];

echo gettype($a); // integer
echo gettype($b); // string
echo gettype($c); // double
echo gettype($d); // boolean
echo gettype($e); // NULL
echo gettype($f); // array
?>
```

### 2.3 Type Juggling & Automatic Type Conversion
PHP is **loosely typed** — it automatically converts a variable's type based on context. This is called **type juggling**.

```php
<?php
$x = "5"; // string
$y = 10;  // integer

$result = $x + $y; // PHP converts "5" to integer 5 automatically
echo $result;           // 15
echo gettype($result);  // integer

// Concatenation forces conversion to string
$num = 5;
$text = "Value: " . $num;
echo $text; // Value: 5
?>
```
> ⚠️ Type juggling can cause unexpected results, e.g. `"5 apples" + 3` evaluates to `8`, because PHP extracts the leading numeric part of the string.

### 2.4 Type Casting
Type casting is **manually** converting a variable's type using a cast operator in parentheses. Unlike type juggling (automatic), casting is explicit and intentional.

```php
<?php
$str = "123";
$num = (int)$str;       // casts string to integer
echo gettype($num);      // integer

$float = (float)"12.5";
echo $float;             // 12.5

$bool = (bool)0;
var_dump($bool);         // bool(false)

$arr = (array)"Hello";
print_r($arr);           // Array ( [0] => Hello )

$string = (string)100;
echo gettype($string);   // string
?>
```
Common cast operators: `(int)`, `(integer)`, `(bool)`, `(boolean)`, `(float)`, `(double)`, `(string)`, `(array)`, `(object)`.

### 2.5 var_dump()
Displays structured information about one or more variables, including their **data type** and **value**. More detailed than `echo` or `print_r()` — commonly used for debugging.

```php
<?php
$a = "Hello";
$b = 25;
$c = 3.14;
$d = true;
$e = [1, "two", 3.0];

var_dump($a); // string(5) "Hello"
var_dump($b); // int(25)
var_dump($c); // float(3.14)
var_dump($d); // bool(true)
var_dump($e);
/*
array(3) {
  [0]=> int(1)
  [1]=> string(3) "two"
  [2]=> float(3)
}
*/
?>
```


---

##  3. Strings

### 3.1 Strings and Escaping
Escape sequences allow special characters inside **double-quoted** strings.

| Escape | Meaning |
|--------|---------|
| `\n` | New line |
| `\t` | Tab |
| `\\` | Backslash |
| `\"` | Double quote |
| `\$` | Dollar sign (prevents variable interpolation) |

```php
<?php
echo "She said \"PHP is fun!\"\n";
echo "Column1\tColumn2\n";
echo "Path: C:\\xampp\\htdocs\n";

$price = 100;
echo "The price is \$price\n"; // prints literal: The price is $price
echo "The price is $price\n";  // prints interpolated: The price is 100
?>
```
> Escape sequences only work inside **double-quoted** strings or heredoc — not in single-quoted strings.

### 3.2 nl2br()
Inserts HTML line breaks (`<br>`) before every newline (`\n`) in a string — useful for displaying multi-line text (e.g. from a textarea or database), since HTML ignores plain `\n`.

```php
<?php
$text = "Line one\nLine two\nLine three";
echo nl2br($text);
// Output (rendered in browser):
// Line one<br />
// Line two<br />
// Line three
?>
```

### 3.3 Heredoc & Nowdoc
Alternative ways to define multi-line strings without escaping quotes.

**Heredoc (`<<<`)** — works like double-quoted strings; variables & escapes are interpolated:
```php
<?php
$name = "Nouran";
$text = <<<EOT
Hello, $name!
This is a heredoc example.
It supports "quotes" and $variables directly.
EOT;
echo $text;
?>
```

**Nowdoc (`<<<'...'`)** — works like single-quoted strings; no interpolation:
```php
<?php
$name = "Nouran";
$text = <<<'EOT'
Hello, $name!
This is a nowdoc example.
Variables like $name are NOT interpolated here.
EOT;
echo $text;
?>
```
> The closing identifier (`EOT`) must start at the beginning of the line (modern PHP allows indentation, as long as it's consistent) and can be any name you choose.

### 3.4 Difference Between ' ' and " " with Variables
- **Single quotes (`' '`)** — literal string; variables and most escapes are **not** parsed (except `\\` and `\'`).
- **Double quotes (`" "`)** — variables and escape sequences (`\n`, `\t`, etc.) are interpolated.

```php
<?php
$name = "Nouran";

echo 'Hello, $name!';   // Hello, $name!  (literal, no interpolation)
echo "Hello, $name!";   // Hello, Nouran! (variable is interpolated)

echo 'Line1\nLine2';    // Line1\nLine2   (no real newline)
echo "Line1\nLine2";    // Line1
                         // Line2          (real newline)
?>
```
> Single-quoted strings skip parsing, so they're slightly faster — preferred when no interpolation is needed.

### 3.5 String Operators: Concatenation and `.=`

**Concatenation (`.`)** joins two strings into one:
```php
<?php
$first = "Hello";
$second = "World";
$result = $first . " " . $second;
echo $result; // Hello World
?>
```

**Concatenation Assignment (`.=`)** appends to an existing variable — shorthand for `$a = $a . "text"`:
```php
<?php
$message = "Hello";
$message .= ", World!";
$message .= " Welcome to PHP.";
echo $message; // Hello, World! Welcome to PHP.
?>
```


---

##  4. Arrays

### 4.1 print_r()
Displays human-readable information about a variable — especially arrays and objects, showing keys/values in a structured, indented format. Unlike `var_dump()`, it does **not** show data types.

```php
<?php
$person = [
    "name" => "Nouran",
    "age" => 24,
    "skills" => ["PHP", "JavaScript"]
];

print_r($person);
/*
Array
(
    [name] => Nouran
    [age] => 24
    [skills] => Array
        (
            [0] => PHP
            [1] => JavaScript
        )
)
*/

// Return as string instead of printing directly
$output = print_r($person, true);
echo $output;
?>
```

### 4.2 Array with Keys
An **associative array** — each value is assigned a specific, named key instead of a default numeric index.

```php
<?php
$student = [
    "name" => "Ahmed",
    "age" => 22,
    "major" => "Computer Science"
];

echo $student["name"]; // Ahmed
echo $student["age"];  // 22
?>
```

### 4.3 Array without Keys
An **indexed array** — PHP automatically assigns numeric keys starting from `0`.

```php
<?php
$fruits = ["Apple", "Banana", "Mango"];

echo $fruits[0]; // Apple
echo $fruits[1]; // Banana
echo $fruits[2]; // Mango
?>
```

### 4.4 Array with One Key
An array can hold a single key/value pair (associative) or a single element (indexed).

```php
<?php
// Associative array with one key
$data = ["username" => "nouran24"];
echo $data["username"]; // nouran24

// Indexed array with one element
$single = ["OnlyOne"];
echo $single[0]; // OnlyOne
?>
```

### 4.5 Array Value Override
If the same key is used more than once, the **last value assigned overrides** the previous one(s).

```php
<?php
$user = [
    "name" => "Sara",
    "age" => 20,
    "name" => "Mona" // overrides the first "name" value
];

print_r($user);
/*
Array
(
    [name] => Mona
    [age] => 20
)
*/

// Same applies to numeric indexes
$nums = [0 => "A", 1 => "B", 0 => "C"];
print_r($nums);
/*
Array
(
    [0] => C
    [1] => B
)
*/
?>
```



---

##  5. Variables & References

### 5.1 The Rules of Naming a Variable
1. Must start with a **`$`** sign, followed by the name.
2. After `$`, the name must start with a **letter or an underscore** (`_`) — not a number.
3. Can only contain **letters, numbers, and underscores** (`A-z`, `0-9`, `_`). No spaces or special characters.
4. Variable names are **case-sensitive** (`$name` and `$Name` are different variables).

```php
<?php
$name = "Valid";       // valid
$_age = 25;            // valid (starts with underscore)
$user1 = "Valid too";  // valid (number not at start)

// $1name = "Invalid";     // starts with a number
// $user-name = "Invalid"; // contains a hyphen
// $user name = "Invalid"; // contains a space

$Name = "Case A";
$name = "Case B";
echo $Name; // Case A
echo $name; // Case B (different variable — case-sensitive)
?>
```

### 5.2 Loosely Typed Languages
PHP is **loosely typed (dynamically typed)**:
- No need to declare a variable's data type when creating it.
- Type is determined **automatically** at runtime based on the assigned value.
- A variable's type can **change** during execution just by assigning a different value type.

```php
<?php
$data = 10;        // integer
echo gettype($data); // integer

$data = "Hello";   // now a string
echo gettype($data); // string

$data = 3.14;      // now a float
echo gettype($data); // double

$data = true;      // now a boolean
echo gettype($data); // boolean
?>
```
> Contrast with **strictly/strongly typed languages** (Java, C), where a variable's type must be explicitly declared and can't change afterward.

### 5.3 Variable Variables and " "
A **variable variable** lets you use one variable's value as the *name* of another, using `$$`.

```php
<?php
$name = "age";
$$name = 25; // creates a new variable called $age with value 25

echo $age;   // 25
echo $$name; // 25 (accessing it via the variable variable)
?>
```

Simple interpolation like `"$$name"` doesn't work as expected in double-quoted strings — curly braces are required:

```php
<?php
$name = "age";
$age = 25;

echo "$$name";   // $25  (WRONG — $ is literal, then $name is interpolated)
echo "${$name}"; // 25   (correct, but deprecated in PHP 8.2+)
echo "{$$name}"; // 25   (correct, alternative syntax)
?>
```
> Best practice: build variable variables **outside** strings, then interpolate the resulting variable normally:
```php
<?php
$name = "age";
$age = 25;
$value = $$name;
echo "The value is $value"; // The value is 25
?>
```

### 5.4 Assign Variable by Reference
By default, PHP assigns variables **by value** (copies). Using `&` assigns **by reference**, so both variables point to the same data.

```php
<?php
$a = 10;
$b = $a;   // assign by value (copy)
$b = 20;
echo $a;   // 10 (unchanged)

$c = 10;
$d = &$c;  // assign by reference
$d = 20;
echo $c;   // 20 (changed — $d references $c)
?>
```

References are useful when passing variables into functions so the function can modify the original:
```php
<?php
function addFive(&$num) {
    $num += 5;
}

$value = 10;
addFive($value);
echo $value; // 15
?>
```

### 5.5 References Aren't Pointers
A PHP reference is just an alias in the symbol table — **not a memory address** you can inspect or do arithmetic on.

```php
<?php
$a = 1;
$b = &$a; // $b is another name for $a, not a pointer to it

$b = 2;
echo $a; // 2

// Unsetting a reference only removes that alias, not the underlying value
unset($b);
echo $a; // 2 (still exists, only the $b alias was removed)
?>
```
> With true pointers you can inspect an address and do pointer arithmetic; with PHP references, you can only alias variables.

### 5.6 Predefined Variables
PHP provides several **superglobal** variables, automatically available in every scope.

| Variable | Purpose |
|----------|---------|
| `$_GET` | Data sent via the URL query string |
| `$_POST` | Data sent via an HTML form (POST method) |
| `$_SERVER` | Server and execution environment info |
| `$_SESSION` | Session-stored data |
| `$_COOKIE` | Cookie data |
| `$_FILES` | Uploaded file data |
| `$_ENV` | Environment variables |
| `$GLOBALS` | Access to all global-scope variables |

```php
<?php
// Reading the current script's file name
echo $_SERVER['PHP_SELF'];

// Reading a value submitted via GET (e.g. page.php?id=5)
echo $_GET['id'] ?? 'No ID provided';

var_dump(isset($_SERVER['REQUEST_METHOD']));
echo $_SERVER['REQUEST_METHOD'] ?? 'CLI'; // GET, POST, or CLI when run from terminal
?>
```


---

##  6. Constants

### 6.1 Constants in PHP
A constant is an identifier for a value that **cannot change** once defined. Defined with `define()` or `const` — no `$` prefix, conventionally UPPERCASE.

```php
<?php
define("SITE_NAME", "My Website");
const MAX_USERS = 100;

echo SITE_NAME; // My Website
echo MAX_USERS; // 100

// MAX_USERS = 200; // Error: cannot reassign a constant
?>
```
> `const` is evaluated at compile time (used mainly at the top level or inside classes); `define()` is evaluated at runtime and can be used conditionally.

### 6.2 Predefined Constants
PHP ships with built-in constants describing the environment (version, OS, error levels, etc.).

```php
<?php
echo PHP_VERSION;       // e.g. 8.3.6
echo PHP_OS;             // e.g. Linux or WINNT
echo PHP_INT_MAX;        // largest supported integer
echo PHP_INT_MIN;        // smallest supported integer
echo PHP_FLOAT_EPSILON;  // smallest representable float difference
echo E_ALL;              // constant used to report all error types
?>
```

### 6.3 Magic Constants
Special predefined constants whose value depends on **where** they're used. Surrounded by double underscores.

| Magic Constant | Returns |
|-----------------|---------|
| `__LINE__` | Current line number in the file |
| `__FILE__` | Full path and filename of the file |
| `__DIR__` | Directory of the file |
| `__FUNCTION__` | Current function name |
| `__CLASS__` | Current class name |
| `__METHOD__` | Current class method name |
| `__NAMESPACE__` | Current namespace |

```php
<?php
echo "Line: " . __LINE__ . "\n";
echo "File: " . __FILE__ . "\n";
echo "Directory: " . __DIR__ . "\n";

function greet() {
    echo "Function name: " . __FUNCTION__;
}
greet(); // Function name: greet
?>
```

### 6.4 Reserved Words
Keywords with special meaning to PHP — cannot be used as class, function, or method names.

```
if, else, elseif, while, do, for, foreach, switch, case, break, continue,
function, return, class, extends, implements, public, private, protected,
static, const, echo, print, include, require, namespace, use, try, catch,
finally, throw, new, global, array, list, isset, unset, and, or, xor, not
```

```php
<?php
// Invalid — "class" is a reserved word, can't be used as a function name
// function class() { }

// Fine — reserved words are only restricted as identifiers,
// not as plain strings or array keys
$data = ["class" => "PHP101"];
echo $data["class"]; // PHP101
?>
```


---

##  7. Operators

### 7.1 Arithmetic Operators
| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `+` | Addition | `5 + 2` | `7` |
| `-` | Subtraction | `5 - 2` | `3` |
| `*` | Multiplication | `5 * 2` | `10` |
| `/` | Division | `5 / 2` | `2.5` |
| `%` | Modulus (remainder) | `5 % 2` | `1` |
| `**` | Exponentiation | `5 ** 2` | `25` |

```php
<?php
$a = 10;
$b = 3;

echo $a + $b;  // 13
echo $a - $b;  // 7
echo $a * $b;  // 30
echo $a / $b;  // 3.3333...
echo $a % $b;  // 1
echo $a ** $b; // 1000
?>
```

### 7.2 Identity & Negation
**Identity** compares value **and** type using `===` / `!==` — no type juggling. **Negation** flips a number's sign (`-`) or a boolean's value (`!`).

```php
<?php
// Identity (strict comparison)
var_dump(5 === "5"); // false (different types)
var_dump(5 === 5);   // true  (same value and type)
var_dump(5 !== "5"); // true  (not identical)

// Negation
$num = 10;
echo -$num; // -10

$isActive = true;
var_dump(!$isActive); // bool(false)
?>
```

### 7.3 Assignment Operators
| Operator | Example | Equivalent To |
|----------|---------|---------------|
| `=` | `$a = 5` | Assigns 5 to `$a` |
| `+=` | `$a += 3` | `$a = $a + 3` |
| `-=` | `$a -= 3` | `$a = $a - 3` |
| `*=` | `$a *= 3` | `$a = $a * 3` |
| `/=` | `$a /= 3` | `$a = $a / 3` |
| `%=` | `$a %= 3` | `$a = $a % 3` |
| `**=` | `$a **= 3` | `$a = $a ** 3` |
| `.=` | `$a .= "text"` | `$a = $a . "text"` |

```php
<?php
$a = 10;
$a += 5;  // 15
$a -= 3;  // 12
$a *= 2;  // 24
$a /= 4;  // 6
$a %= 4;  // 2
echo $a;  // 2
?>
```

### 7.4 Comparison Operators
| Operator | Name | Description |
|----------|------|--------------|
| `==` | Equal | True if values are equal (type juggling applied) |
| `===` | Identical | True if values and types are equal |
| `!=` | Not equal | True if values are not equal |
| `<>` | Not equal (alternate) | Same as `!=` |
| `!==` | Not identical | True if values or types differ |
| `<` | Less than | |
| `>` | Greater than | |
| `<=` | Less than or equal to | |
| `>=` | Greater than or equal to | |
| `<=>` | Spaceship | Returns `-1`, `0`, or `1` |

```php
<?php
var_dump(5 == "5");   // true  (values equal, type juggling applied)
var_dump(5 === "5");  // false (types differ)
var_dump(5 != 3);     // true
var_dump(5 <> 3);     // true
var_dump(5 !== "5");  // true
var_dump(5 < 10);     // true
var_dump(5 >= 5);     // true
?>
```

### 7.5 The `<>` Operator
An alternate syntax for `!=` (not equal), inherited from SQL-style syntax. Works identically to `!=` in PHP.

```php
<?php
$a = 5;
$b = 8;

var_dump($a <> $b); // true  (5 is not equal to 8)
var_dump($a != $b); // true  (identical result)

$c = 5;
var_dump($a <> $c); // false (5 equals 5)
?>
```

### 7.6 Spaceship Operator (`<=>`)
Returns:
- `-1` if the left value is **less than** the right
- `0` if they're **equal**
- `1` if the left value is **greater than** the right

Especially useful in custom sort callbacks (e.g. `usort()`).

```php
<?php
echo 1 <=> 2; // -1
echo 2 <=> 2; //  0
echo 3 <=> 2; //  1
echo "a" <=> "b"; // -1 (works with strings too)

// Sorting an array of numbers descending
$numbers = [5, 2, 8, 1];
usort($numbers, fn($a, $b) => $b <=> $a);
print_r($numbers); // [8, 5, 2, 1]
?>
```

### 7.7 Strings with Comparison Operators
- If **both** strings are numeric (e.g. `"10"` and `"9"`), PHP compares them **numerically**.
- If at least one is non-numeric, PHP compares character by character (lexicographically, by ASCII value).

```php
<?php
var_dump("10" == "9");       // false — 10 != 9 numerically
var_dump("10" > "9");        // true  (numeric comparison: 10 > 9)
var_dump("abc" == "abc");    // true  (identical strings)
var_dump("abc" < "abd");     // true  (lexicographic: 'c' < 'd')
var_dump("10" == "1e1");     // true  (both interpreted numerically: 10 == 10)
var_dump("apple" == "Apple"); // false (case-sensitive)
?>
```
> Since PHP 8, comparisons between a **number and a non-numeric string** convert the number to a string first — e.g. `0 == "abc"` is now `false` (it was `true` in PHP 7).

### 7.8 Pre and Post Increment & Decrement Operators
- **Pre (`++$x` / `--$x`)** — changes the value **first**, then returns it.
- **Post (`$x++` / `$x--`)** — returns the **current** value first, then changes it.

```php
<?php
$a = 5;
echo ++$a; // 6 (incremented first, then displayed)
echo $a;   // 6

$b = 5;
echo $b++; // 5 (displayed first, then incremented)
echo $b;   // 6

$c = 5;
echo --$c; // 4 (decremented first, then displayed)

$d = 5;
echo $d--; // 5 (displayed first, then decremented)
echo $d;   // 4
?>
```

### 7.9 Logical Operators
| Operator | Name | Example | Description |
|----------|------|---------|--------------|
| `&&` or `and` | AND | `$a && $b` | True if both are true |
| `\|\|` or `or` | OR | `$a \|\| $b` | True if at least one is true |
| `!` | NOT | `!$a` | Inverts the boolean value |
| `xor` | XOR | `$a xor $b` | True if exactly one is true (not both) |

```php
<?php
$a = true;
$b = false;

var_dump($a && $b); // false
var_dump($a || $b); // true
var_dump(!$a);       // false
var_dump($a xor $b); // true (exactly one is true)
?>
```
> `and`/`or` have **lower precedence** than `&&`/`||`, which can affect how expressions evaluate with `=`. It's generally safer to use `&&` and `||` in conditional logic.

### 7.10 Xor Operator
Returns `true` only if **exactly one** operand is `true`.

```php
<?php
var_dump(true xor false);  // true  (exactly one is true)
var_dump(true xor true);   // false (both true)
var_dump(false xor false); // false (both false)

// Only allow access if exactly one condition is met
$hasVoucher = true;
$isMember = false;
var_dump($hasVoucher xor $isMember); // true — eligible for a one-time discount
?>
```

