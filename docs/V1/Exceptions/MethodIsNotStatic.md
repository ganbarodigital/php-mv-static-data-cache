---
currentSection: v1
currentItem: exceptions
pageflow_prev_url: index.html
pageflow_prev_text: Exceptions
---

# MethodIsNotStatic

<div class="callout info" markdown="1">
Since v1.2016041901
</div>

## Description

`MethodIsNotStatic` is an exception thrown when an attempt is made to access a method statically, but that method is not a static method.

## Public Interface

`MethodIsNotStatic` has the following public interface:

```php
// our base class and interface(s)
use GanbaroDigital\ExceptionHelpers\V1\BaseExceptions\ParameterisedException;
use GanbaroDigital\HttpStatus\Specifications\HttpStatusProvider;
use GanbaroDigital\UnitTestHelpers\V1\Exceptions\UnitTestHelpersException;

// return types from our method(s)
use GanbaroDigital\HttpStatus\StatusValues\RequestError\UnprocessableEntityStatus;

// how to import
use GanbaroDigital\UnitTestHelpers\V1\Exceptions\MethodIsNotStatic;

// our public interface
class MethodIsNotStatic
  extends ParameterisedException
  implements UnitTestHelpersException, HttpStatusProvider
{
    /**
     * create a throwable exception
     *
     * @param  string $className
     *         the class we were asked to invoke
     * @param  string $methodName
     *         the method on $className that was not static
     * @return MethodIsNotStatic
     */
    public static function newFromClassAndMethod($className, $methodName);

    /**
     * which HTTP status code do we map onto?
     * @return UnprocessableEntityStatus
     */
    public function getHttpStatus();
}
```

## How To Use

### Creating Exceptions To Throw

Call `MethodIsNotStatic::newFromClassAndMethod()` to create a throwable exception:

```php
throw MethodIsNotStatic::newFromClassAndMethod(MyClass::class, 'unhappyMethod');
```

### Catching The Exception

`MethodIsNotStatic` extends or implements a rich set of classes and interfaces. You can use any of these to catch any thrown exceptions:

```php
// example 1: we catch only MethodIsNotStatic exceptions
use GanbaroDigital\UnitTestHelpers\V1\Exceptions\MethodIsNotStatic;

try {
    throw MethodIsNotStatic::newFromClassAndMethod(MyClass::class, 'unhappyMethod');
}
catch(MethodIsNotStatic $e) {
    // ...
}
```

```php
// example 2: catch all exceptions thrown by the Unit Test Helpers library
use GanbaroDigital\UnitTestHelpers\V1\Exceptions\MethodIsNotStatic;
use GanbaroDigital\UnitTestHelpers\V1\Exceptions\UnitTestHelpersException;

try {
    throw MethodIsNotStatic::newFromClassAndMethod(MyClass::class, 'unhappyMethod');
}
catch(UnitTestHelpersException $e) {
    // ...
}
```

```php
// example 3: catch all exceptions where there was a problem with the
// parameter(s) passed into the method
use GanbaroDigital\HttpStatus\Specifications\RequestError;
use GanbaroDigital\UnitTestHelpers\V1\Exceptions\MethodIsNotStatic;

try {
    throw MethodIsNotStatic::newFromClassAndMethod(MyClass::class, 'unhappyMethod');
}
catch(RequestError $e) {
    $httpStatus = $e->getHttpStatus();
    // ...
}
```

```php
// example 4: catch all exceptions that map onto a HTTP status
use GanbaroDigital\HttpStatus\Specifications\HttpStatusProvider;
use GanbaroDigital\UnitTestHelpers\V1\Exceptions\MethodIsNotStatic;

try {
    throw MethodIsNotStatic::newFromClassAndMethod(MyClass::class, 'unhappyMethod');
}
catch(HttpStatusProvider $e) {
    $httpStatus = $e->getHttpStatus();
    // ...
}
```

```php
// example 5: catch all runtime exceptions
use GanbaroDigital\UnitTestHelpers\V1\Exceptions\MethodIsNotStatic;
use RuntimeException;

try {
    throw MethodIsNotStatic::newFromClassAndMethod(MyClass::class, 'unhappyMethod');
}
catch(RuntimeException $e) {
    // ...
}
```

## Notes

None at this time.

## See Also

* [`HttpStatusProvider` interface](http://ganbarodigital.github.io/php-http-status/httpStatusProviders.html)
