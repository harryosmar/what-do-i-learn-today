# 15 Feb 2019

## PHP

### Share property across the same objects

> The `same object` means : the objects instantiated from the same `class`

> Question : What is the use of this "shared property" ?

> Answers : 
- To make sure all objects get the latest updated "property" value.
- It can also be used as *caching layer* accross objects. eg: only the 1st object run the *process of fetching data* then store the data in *shared property*. The next objects just used the *shared property*.


Example
 
[`Person`](https://github.com/harryosmar/sample-phpunit-test/blob/static-property/src/Person.php) object will have properties : `name`, `ability`.

- Property `ability` will be shared for all objects [`Person`](https://github.com/harryosmar/sample-phpunit-test/blob/static-property/src/Person.php). So each object [`Person`](https://github.com/harryosmar/sample-phpunit-test/blob/static-property/src/Person.php) will have the same `ability`.
- Each object [`Person`](https://github.com/harryosmar/sample-phpunit-test/blob/static-property/src/Person.php) can add a new `ability`, and because the `ability` is shared,  others objects will get the same ability too. 

Check this unit test : https://github.com/harryosmar/sample-phpunit-test/blob/static-property/tests/unit/PersonTest.php

