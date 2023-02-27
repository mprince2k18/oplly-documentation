# PHP Coding Standards

Online resources already exist that describe a standard approach to writing code in the PHP language. Once such guide is PSR (eg.: [PSR-12: Extended Coding Style - PHP-FIG](https://www.php-fig.org/psr/psr-12/)  )  which is mandatory reading for all developers within the organisation.

The organisation also has the following code standards which reenforce / clarify particular standards.

## Strict types
All new PHP files should start with:

```php
<?php
declare(strict_types=1)
```
## Naming Conventions
Irrespective of the type, all elements should have a descriptive name that provides the reader with intuitive understanding (within the context of the surrounding code) or the purpose. Readability is extremely important and provides efficiency within the organisation for processes such as code reviews and bug investigations.

References: https://betterprogramming.pub/string-case-styles-camel-pascal-snake-and-kebab-case-981407998841?gi=9f738c894f6b  

### Variables
New variables in PHP files should use Camel Case
```php
$accountId
```
### Functions
Function names should be in Camel Case.

```php
function doSomething(): void
{
  // method body
}
```
### Classes
Class names should be in Pascal Case.
```php
public class PayFakeRepository
{
  // Class definition
}
```
### Constants
Never assign a static value to a variable. Instead, declare a constant with a descriptive name. This will allow readers of the code to identify the meaning of the value (use comments as well if needed).

Constants should be in uppercase with words separated by an underscore.
```php
const SYSTEM_USER_ID = 0;
```
### Comments
Commenting code is always a good idea. The more information felt necessary to convey the intention of a code block, the better. Comments should be kept professional and to the point. Never comment out code. Instead, just remove it. Never store sensitive information in code comments. 

### DocBlock Usage
Adding docBlocks for functions is mandatory except where function signature already contains all information (eg.: all parameters have a type defined and the return type has been specified as well.)

```php
public function myFunction(int $accountID, string $name): bool
```
All class properties/fields should have the @var annotation to help the IDE figure out the type.

```php
class MyClass
{
  /**
   * @var int
   */
  protected $fieldName
}
 ```

DocBlocks are mandatory for functions when the function throws an exception as that cannot be inferred from the function signature.

```php
/**
 * @throws AccountNotFoundException
 */
public function getAccountById(int $id): Account
{
...
}
```

For Eloquent Model classes a class level docBlock defining all the database fields with a @property annotation is mandatory.

```php
/**
 * @property int $id
 * @property string $name
 * ...
 */
class Account extends Model
{
  ...
}
```
### Constructors
Constructor code should never contain business logic. It should only be used to initialise variable.
Creating objects or calculating values should be in their own methods and not in the contructor.

### Models
Model classes should not contain any business logic. All logic needs to be added to a Repository or Service class dealing with the Model.

### Dependency Injection
Controllers, services, providers should use Dependency Injection instead of Facades to make sure object composition is always easily testable.
