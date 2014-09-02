## 2. Suppose getData is a function that takes...

Nothing would be printed by the following because forEach is called on an empty Array. This is because runMultipleQueries adds data to the results Array on an asynchronous callback, while the results Array is returned immediatly.

**FIX:**

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

#4 Suppose we have a function...
The only way I could gain access to the actual error object being thrown by getData is to pass that as a parameter to makeErrorHandler as well as the message.

```javascript
getData(query, function(result) {	// handle the success case}, makeErrorHandler(err, 'Could not get data.'));
function makeErrorHandler(err, msg) {	sendErrorToServer(err);
	showMessage(message);}
```
