# 15 Feb 2019

## PHP

### Share property across the same objects

> The `same object` means : the objects instantiated from the same `class`

Example
 
[`Person`](https://github.com/harryosmar/sample-phpunit-test/blob/static-property/src/Person.php) object will have properties : `name`, `ability`.

- Property `ability` will be shared for all objects [`Person`](https://github.com/harryosmar/sample-phpunit-test/blob/static-property/src/Person.php). So each object [`Person`](https://github.com/harryosmar/sample-phpunit-test/blob/static-property/src/Person.php) will have the same `ability`.
- Each object [`Person`](https://github.com/harryosmar/sample-phpunit-test/blob/static-property/src/Person.php) can add a new `ability`, and because the `ability` is shared,  others objects will get the same ability too. 

```
Person
    - name
    - ability
```

Check this unit test : https://github.com/harryosmar/sample-phpunit-test/blob/static-property/tests/unit/PersonTest.php