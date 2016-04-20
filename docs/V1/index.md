---
currentSection: v1
currentItem: home
---

# Version 1.x

<div class="callout info" markdown="1">
Since v1.2016042001
</div>

## Description

`StaticDataCache` is a trait. It provides a simple key/value store that is shared amongst all instances of the same class.

## Public Interface

`StaticDataCache` provides a `protected` interface for your class to use.

```php
use GanbaroDigital\StaticDataCache\V1\StaticDataCache;

trait StaticDataCache
{
    /**
     * do we have this result set in the cache?
     *
     * @param  string|int|double $key
     *         the index to search for
     * @return mixed|null
     */
    protected static function getFromCache($key);

    /**
     * store data about a key to speed up repeated calls
     *
     * @param string|int|double $key
     *        the data key to store information about
     * @param mixed $data
     *        the data to store in the cache
     */
    protected static function setInCache($key, $data);

    /**
     * empty out the cache completely
     *
     * this is mostly provided for unit testing purposes
     *
     * @return void
     */
    protected static function resetCache();

    /**
     * return a copy of the cache for inspection
     *
     * this is mostly provided for unit testing purposes
     *
     * @return array
     */
    protected static function getCache();
}
```

## How To Use

### Adding To Your Own Classes

It's very easy to add the `StaticDataCache` to your own classes. Just import the trait, and add it to your class with a `use` statement.

```php
use GanbaroDigital\StaticDataCache\V1\StaticDataCache;

class MyClass
{
    use StaticDataCache;
}
```

### Caching Expensive Operations

The `StaticDataCache` is normally used like this:

* do we already have a result cached? if so, return that
* calculate the result of the operation
* cache the calculated result, and then return that

```php
class MyClass
{
    public function expensiveOperation($data)
    {
        // do we have this in the cache?
        //
        // you need to calculate a key to use
        $retval = static::getFromCache($key);
        if ($retval !== null) {
            return $retval;
        }

        // perform your expensive operation here

        // cache the results
        static::setInCache($key, $value);

        // all done
        return $value;
    }
}
```

### Deciding What To Cache

_Caches_ are an optimisation. They only make sense if the following are true:

* _Called multiple times_: if an operation is rarely called more than once, you probably don't need a cache.
* _Expensive operation_: using the cache means at least one PHP function call (which is very expensive prior to PHP 7.0). Your operation has to be slower than the cost of caching the data.
* _Repeatable operation_: for the same input data, the operation has to produce the same return value. If the return value needs to vary in any way at all, the data isn't suitable for caching.
* _NULL isn't a valid result_: `StaticDataCache::getFromCache()` returns `NULL` if the data you're looking for isn't in the cache. That means that you can't store `NULL` values in the cache.

## Throws

This trait does not throw any exceptions.

## Notes

1. The cache itself is private. You can get a read-only copy of the cache by calling `StaticDataCache::getCache()`.

## See Also

Nothing at this time.
