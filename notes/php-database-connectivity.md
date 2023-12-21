# PHP Database Connectivity

## PHP Data Objects (PDO)

[PHP](php) Data Objects is an extension, a **data-access abstraction layer** (**DB vendor agnostic**) that allows you to use the same functions to issue queries and fetch data regardless of the database you are using.

Note that you cannot perform any database functions using the PDO extension by itself. You must use a **database-specific PDO driver** to access a database server. PDO, PDO_MYSQL and the PDO_SQLITE driver are enabled by default. You may need to enable the PDO driver for your database of choice.

**PDO**, **PDO_MYSQL** and the **PDO_SQLITE** driver are enabled by default. You may need to enable the PDO driver for your database of choice.

## Database Support

All those drivers do not have to be available on your system. To find out which drivers you currently have, use following:

```php
print_r(PDO::getAvailableDrivers())
```

`PDO::getAvailableDrivers` returns an array of available PDO drivers. If no drivers are available, it returns an empty array.

To use the driver, you can use `dl()` to load it at runtime or enable it in `php.ini` as in (below `php_pdo.dll`):

`extension=php_pdo.dll`

`extension=php_pdo_firebird.dll`

`extension=php_pdo_informix.dll`

`extension=php_pdo_mysql.dll`

...

`extension=php_pdo_odbc.dll`

`extension=php_pdo_pgsql.dll`

`extension=php_pdo_sqlite.dll`

### Database Access Steps

- **Connect** - Could vary depending on the database type.
- **Query** - The same for all database types.
- **Close** - The same for all database types.

## Connecting to a Database

Different databases may have slightly different connection methods:

```php

$db = new PDO('mysql:host=localhost;dbname:db', $user, $pass);
$db = new PDO('sqlite:my/database/path/database.db');

```

## SQL Injections

A type of attack, insertions or injections of either a partial or complete SQL query being made via the data input OR transmitted from the client (e.g. browser) to the web application.

- Can read sensitive data from the database
- Modify database data (insert/update/delete).
- Execute administration operations on the database (such as shutdown the DBMS).
- Recover the content of a given file existing on the DBMS file system or write files into the file system.
- In some cases, issue commands to the operating system.

**Make sure you sanitize and validate ALL user input.**

## Prepared Statements

A prepared statement is a query template (parameterized queries) used to create queries that are more secure, have better performance, and are more convenient to write.

A query template is a query with placeholders. For example:

```sql
INSERT INTO people (last_name, first_name) VALUES (?, ?);
SELECT * FROM people WHERE last_name=?;
```

The **?** placeholders are used in places that could have literal input data (do not
use it for table or column names).

The placeholder can also be a named one:

```sql
INSERT INTO people (last_name, first_name) VALUES (:lname, :fName);
SELECT * FROM people WHERE last_name=:lname;
```

The prepared statement execution consists of two stages:

**PREPARE**

A query template is created and sent to the database server. The server parses, compiles, and performs query optimization on the SQL statement template, and stores the result without executing it.

```php
// prepare the statement (named placeholders)
$statement = $db->prepare("
INSERT INTO people (last_name, first_name)
VALUES (:lName, :fName)
");
```

**EXECUTE**

At a later time, the application binds the values to the parameters and sends them to the server. The server executes the statement with the bound values.

```php
// bind & execute the prepared statement
$statement->execute(array(':lName' => $lastName,':fName' => $firstName));
```

### Prepared Statements Example 1

```php
// prepare the statement (unnamed placeholders)
$statement = $db->prepare("
INSERT INTO people (last_name, first_name) VALUES (?, ?)");

// bind parameters (unnamed placeholders)
$statement->bindParam(1, $lastName, PDO::PARAM_STR);
$statement->bindParam(2, $firstName, PDO::PARAM_STR);

// execute the prepared statement
$statement->execute();
```

`public PDO::prepare(...): PDOStatement|false` - Prepares a statement for execution and returns a statement object.

`public PDOStatement::bindParam(...): true|false` - Binds a PHP variable to a corresponding placeholder in the SQL statement. Returns true on success or false on failure.

### Prepared Statements Example 2

```php
// prepare the statement (unnamed placeholders)
$statement = $db->prepare("
INSERT INTO people (last_name, first_name)
VALUES (?, ?)
");

// bind & execute the prepared statement
$statement->execute(array($lastName, $firstName));
```

`public PDOStatement::execute(?array $params = null): bool` - Executes the prepared statement.

`$params` - An array of values with as many elements as there are bound parameters in
the SQL statement.

**Returns** true on success or false on failure.

### Prepared Statements Example 3

```php
// prepare the statement (named placeholders)
$statement = $db->prepare("
INSERT INTO people (last_name, first_name)
VALUES (:lName, fName)");

// bind parameters (named placeholders)
$statement->bindParam(':lname', $lastName, PDO::PARAM_STR);
$statement->bindParam(':fName', $firstName, PDO::PARAM_STR);

// execute the prepared statement
$statement->execute();
```

`public PDO::prepare(...): PDOStatement|false` - Prepares a statement for execution and returns a statement object.

`public PDOStatement::bindParam(...): true|false` - Binds a PHP variable to a corresponding placeholder in the SQL statement.

**Returns** true on success or false on failure.

### Prepared Statements Example 4

```php
// prepare the statement (named placeholders)
$statement = $db->prepare("
INSERT INTO people (last_name, first_name)
VALUES (:lName, :fName)
");

// bind & execute the prepared statement
$statement->execute(array(':lName' => $lastName,':fName' =>
$firstName));
```

## C.R.U.D Operations

### CreateRUD

Works only with **associative arrays**. The keys of your array need to match the named placeholders (you may omit the colon). If you have an array of arrays, you can iterate over them, and simply call the execute with each array of data.

Another feature of named placeholders is the ability to insert objects into your DB, assuming the properties match the named fields. By casting the object to an array in the execute, the properties are treated as array keys.

### CReadUD

The data is obtained via the fetch() (gets one row at a time) or fetchAll() (gets all rows as an array). You may also specify the format of the data being obtained by using one of these constants:

- **PDO::FETCH_ASSOC** returns an array indexed by column name.

- **PDO::FETCH_BOTH** (default) returns an array indexed by both column name and number.

- **PDO::FETCH_BOUND** assigns the values of columns to the variables set with the bindColumn() method.

- **PDO::FETCH_CLASS** assigns the values of columns to properties of the named class. If matching properties do not exist, those will be created. This option allows to fetch data directly into a class of your choosing. When used, the properties of your object are set BEFORE the constructor is called - if properties matching the column names don't exist, those properties will be created (as public) for you.

- **PDO::FETCH_INTO** updates an existing instance of the named class.

- **PDO::FETCH_LAZY** combines **PDO::FETCH_BOTH**/**PDO::FETCH_OBJ**, creating the object variable names as they are use.

- **PDO::FETCH_NUM** returns an array indexed by column number.

- **PDO::FETCH_OBJ** returns an anonymous object with property names that correspond to the column names.

## CRUpdateD

Updating data in a database using PDO is straightforward. You prepare your SQL update statement, binding placeholders to the values you want to update. This method is secure and prevents SQL injection. The placeholders in the SQL statement are replaced by the actual values when the `execute()` method is called.

### CRUDelete

Deleting data is similar to updating. You prepare your delete statement with placeholders, then execute the statement with the appropriate values. This ensures safe deletion of only the intended records.

Remember to handle exceptions and errors appropriately in your code to manage database connection issues or problems with executing SQL statements. This approach promotes robust and secure database interactions in your applications.
