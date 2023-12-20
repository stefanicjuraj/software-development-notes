# PHP

PHP is an acronym for **PHP: Hypertext Preprocessor**.

It is an open-source scripting language that is mostly used for web development.

The PHP script (code) can be executed from the command line, but also on the server (in the case of web development).

PHP files have extension `.php`.

Aside of the PHP code, PHP files may also contain text, HTML, CSS, and JavaScript code.

A PHP script can be placed anywhere in the HTML document.

A PHP script starts with A PHP script starts with `<?php` and ends with `?>`.

## PHP Workflow

1. The client sends a request to the web server.
2. The web server locates the requested file and, if found, sends it to the PHP interpreter.
3. The PHP interpreter parses the requested file for PHP directives. The PHP interpreter executes any PHP directives found in the file and replaces those directives with the result of that directive’s execution.
4. The PHP interpreter sends back the parsed file (static HTML page) to the web server.
5. The web server sends the webpage back to the client.

## Script vs Program

**Scripting** languages are usually interpreted at runtime rather than compiled. A script only runs in response to an event. It has little, or no user interaction after that initial event so a PHP script does not run until a web page is requested. Then it launches, follows its instructions from top to bottom and quits until another action launches the script again.

A **program** runs even when not responding to events. It continues to run and to wait for an interaction whether that interaction comes from a user making choices, or from other programs or input.

## Comments

```php
// This is a single-line comment

# This is also a single-line comment

/*
 This is a multiple-lines comment
*/

/*
 * This multiple-lines comment looks even better
 */
```

## Variables: Naming Convention

Variable names have to begin with a dollar sign (`$`).

The dollar sign must be followed by a letter or an underscore. The remainder can be any combination of letters, numbers, and underscores (`A-z`, `0-9`, and `_` ).

The variable name is case-sensitive, so `$username` is a different variable than `$UserName`.

There are different ways to separate words in variable names. The large majority of developers tend to use the **camelCase** notation. Most PHP developers tend to **use_underscores**. CSS property names **use-dashes**.

## Variables: Data Types

### Scalar Types

- **Boolean** - `TRUE` or `FALSE`
- **Integer** - Whole numbers: e.g., `1`, `-13`, `131313`
- **Float** (Double) - Numbers with decimal notations: e.g., `13.13`
- **String** - Words: e.g., “`Hello world`”, or “`13`”

### Compound Types

- **Array** - A collection of keys with their values.
- **Object** - The basics for object-oriented programming.

### Special Types

- **NULL** - Defines a variable with no value.
- **resource** - Holds a reference to an external resource: functions, databases, files, or other resources outside of PHP.

## Variables: Declaration & Initialization

PHP is a loosely typed language – you do not have to define which data type the variable is.

PHP recognizes the type of data being stored into a variable at the time it is being assigned, be that a string, a number, etc.

```php

$firstName = "Juraj";
$lastName = "Stefanic";

$year = 2013;
$number = 13;

```

When working with strings, you can enclose literals in either single or double quotes. This allows you to enclose one kind of quote inside another.

```php
$q = 'T.A. Edison: "There is time for everything"';
```

## Variables & Quotes

PHP substitutes a variable name within a double-quoted string with that variable's value. Variable substitution is not being performed within the single quotes.

```php
$quote= "There is time for everything";
echo "My favorite quote is $quote.";
```

**Output**: *My favorite quote is "There is time for everything"*.

```php
$quote= "There is time for everything";
echo 'My favorite quote is $quote.
```

**Output**: *My favorite show is $quote*.

## Variable Scope

Variables can be declared anywhere in the script. 

Recall: The scope of a variable is the part of the script where the variable can be referenced/used.

PHP has three different variable scopes: **local**, **global**, **static**.

A variable declared outside a function has a **GLOBAL SCOPE** - can only be accessed outside a function.

A variable declared within a function has a **LOCAL SCOPE** - can only be accessed within that function.

A **STATIC VARIABLE** is a variable that exists only in a local function scope, and it does not lose its value when that function is completed.

## Constants

A constant is an identifier/name for a scalar value.

Constants are automatically global and can be used across the entire script.

By convention, constant identifiers are always uppercase. 

A constant name should start with a letter or underscore, followed by any number of letters, numbers, or underscores. 

To create a constant, use the define() function.

```php
<?php
define("Greeting", "Welcome");
echo
?>
```

When using a constant, there is NO (`$`) sign.

As of **PHP 5.3.0**, you can define a constant by using the the `const` keyword (const keyword was used for class constants).

As of **PHP 5.6** it is possible to define array constant using `const` keywords and as of **PHP 7** array constants can also be defined using `define()`.

```php
<?php
const HELLO = 'Hello World';
echo HELLO;
?>
```

The value of a constant cannot change during the execution of the script except for magic constants.

## Arrays

Arrays are known as **compound data types**. What it means is that they are more complex in structure than simple scalar data types such as strings and integers.

In PHP, there are three types of arrays:

- **Indexed Arrays** - Arrays with numerical keys.
- **Associative Arrays** - Arrays with named keys.
- **Multidimensional Arrays** - Arrays containing one or more arrays.

## Superglobals

Superglobals are built-in variables, usually arrays, that are always available in all scopes.

`$_POST` and `$_GET` belong to this specific group of variables.

`$GLOBALS` is an associative array that references all variables available in global scope.

Other superglobals: `$_SERVER`, `$_FILES`, `$_COOKIE`, `$_SESSION`, `$_REQUEST`, `$_ENV`.

## Functions

Functions are defined using the reserved word **function** followed by a unique name that should begin with a letter or an underscore character, followed by any number of letters, underscores, or numbers.

Round brackets **()** that follow the function name are used to pass in any parameters. Curly braces **{}** are used to surround any code that is to be contained within the function.

```php
function saySomething($string) {
  echo $string;
}
```

PHP supports **passing arguments by value (the default)**, **passing arguments by reference**, and **default argument values**.

## Includes

It is possible to import and evaluate the content of an external PHP file into your current script. There are four statements:

- **include** - includes the contents of the file. If the file does not exist or is inaccessible, a warning is issued, but the PHP continues executing the current script.
- **include_once** ― same as include, except that an extra check is made to assure the file hasn't been imported already. In case the file has been imported, the PHP will not re-include the content.
- **require** ― similar to include except upon failure PHP will stop executing the current script.
- **require_once** ― same as require but with an extra check to ensure the content is imported only once.

```php
include 'externalFile.php'
```

OR

```php
include ('externalFile.php');
```

Included files inherit the variable scope of the include's location.

Included files drop out of PHP parsing mode and into HTML mode.

After the file is included, PHP parsing mode is restored.

Included files do not have to have any particular extension (common practice: `.inc`, OR `.php`). 

Include files do not have to be on the same server, and can be fetched with http.