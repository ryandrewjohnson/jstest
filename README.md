## 2. If you think this code will print something other than the correct list of results, please suggest a fix.

Nothing would be printed by the following because forEach is called on an empty Array. This is because runMultipleQueries adds data to the results Array on an asynchronous callback, while the results Array is returned immediatly.

*FIX:*

```javascript
	function runMultipleQueries(queries) {
    var promises = [];

    queries.forEach(function(query) {

        promises.push(getData(query));

    });

    return Promise.all(promises);
}

runMultipleQueries(someArrayOfQueries).then(function (results) {
  // all loaded
  console.log(results);
}, function (err) {
  // one or more failed
  console.log(err);
});
```