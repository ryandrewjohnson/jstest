## 1. Suppose you have an HTTP endpoint /orders...

Please see my working example at:


[http://codepen.io/ryandrewjohnson/pen/CvLAd](http://codepen.io/ryandrewjohnson/pen/CvLAd)



## 2. Suppose getData is a function that takes...

Nothing would be printed by the following because forEach is called on an empty Array. This is because runMultipleQueries adds data to the results Array on an asynchronous callback, while the results Array is returned synchronously.

For a functioning version of the fix that uses three $http requests in for an array of 'quereis' see [http://codepen.io/ryandrewjohnson/pen/Cmztf](http://codepen.io/ryandrewjohnson/pen/mztf)

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

##3. Consider the following Angular template:
This issue occurs because we are attempting to set a value directly on the child $scope object in ChildCtrl. Because a child $scope uses prototypical inheritance as soon as we set the value property on the child $scope we lose the ability to write to the parent $scope. 

To fix this issue we need a property e.g(model) added to the parent $scope to store our value data. This way we can read an write to model propery on $scope without losing the prototypical inheritance.

Please see my working fix at:


[http://codepen.io/ryandrewjohnson/pen/oxzya](http://codepen.io/ryandrewjohnson/pen/oxzya)



##4. Suppose we have a function...
The only way I could gain access to the actual error object being thrown by getData is to pass that as a parameter to makeErrorHandler as well as the message.

```javascript
getData(query, function(result) {	// handle the success case}, makeErrorHandler(err, 'Could not get data.'));
function makeErrorHandler(err, msg) {	sendErrorToServer(err);
	showMessage(message);}
```

## 5. Suppose we want a function delay(msec)...

Please see my working example at:

[http://codepen.io/ryandrewjohnson/pen/jaknu](http://codepen.io/ryandrewjohnson/pen/jaknu)



##6. Write a function that takes an array of integers...

Please see my working example at:

[http://codepen.io/ryandrewjohnson/pen/jyecd](http://codepen.io/ryandrewjohnson/pen/jyecd)
