---
currentSection: v1
currentItem: classesandobjects
pageflow_prev_url: index.html
pageflow_prev_text: Classes And Objects
---

# InvokeMethod

<div class="callout info" markdown="1">
Since v1.2016041901
</div>

## Description

Use `InvokeMethod` to call a protected or private method.

## Public Interface

`InvokeMethod` has the following public interface:

```php
// how to import
use GanbaroDigital\UnitTestHelpers\V1\ClassesAndObjects\InvokeMethod;

class InvokeMethod
{
    /**
     * Call protected/private method of a class
     *
     * Use ONLY for testing purposes
     *
     * @param string $className
     *               class we want to call
     * @param string $methodName
     *               method we want to call
     * @param array  $params
     *               args to pass into the method
     *
     * @return mixed
     *         return value from calling $methodName on $classname
     */
    public static function onClass($className, $methodName, array $params = array());

    /**
     * Call protected/private method of an object.
     *
     * Use ONLY for testing purposes
     *
     * @param object $object
     *               object we want to call
     * @param string $methodName
     *               method we want to call
     * @param array  $params
     *               args to pass into the method
     *
     * @return mixed
     *         return value from calling $methodName on $object
     */
    public static function onObject($object, $methodName, array $params = array());
}
```

## Throws

`InvokeMethod` can throw the following exception(s):

* [`MethodIsNotStatic`](../Exceptions/MethodIsNotStatic.html) - if you attempt to use `InvokeMethod::onClass` to call a non-static method.

## Notes

None at this time.

## See Also

Nothing at this time.
