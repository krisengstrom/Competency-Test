## Senior JS developer competency test

#### Task 1. Floats.

- [x] Please explain why this code `console.log(0.1 + 0.2 == 0.3);` outputs `false` in console? 
- - Floating point numbers are always approximate. The sum won't be exactly 0.3. 
- [x] Please suggest fix to make this expression working as expected.
- - `console.log(parseFloat(0.1 + 0.2).toFixed(2) == 0.3);`

#### Task 2. Sum function.

- [x] Write a `sum` function which will work properly when invoked using either syntax below: 

```javascript
console.log(sum(2,3)); // Outputs 5 
console.log(sum(2)(3)); // Outputs 5
``` 

- [x] Make the function working for any number of arguments.

```javascript
function sum() {

	var args = Array.prototype.slice.call(arguments);
	var sum = args[0];

	function add(arg) {
		sum += arg;
		return add;
	}

	add.toString = function() {
		return sum;
	}

	if (args.length > 1) {
		args.slice(1).forEach(function(arg) {
			add(arg);
		});
	}

	return add;
}

console.log(parseInt(sum(10)(10)(10)));
console.log(parseInt(sum(10, 10, 10)));
``` 


#### Task 3. Loops.

Consider you have code snippet like this: 

```javascript
for (var i = 0; i < 5; i++) {
  var btn = document.createElement('button');
  btn.appendChild(document.createTextNode('Button ' + i));
  btn.addEventListener('click', function(){ console.log(i); });
  document.body.appendChild(btn);
}
```

- [x] What will be the output when user clicks on `Button 1` and why? 
- - It will always be 5 because i is a reference to a variable in the global scope.
- [x] Please, suggest a fix to get the expected behavior.
```javascript
for (var i = 0; i < 5; i++) {
	var btn = document.createElement('button');
	btn.appendChild(document.createTextNode('Button ' + i));
	btn.dataset.index = i; //use a data attribute on the model/element itself
	btn.addEventListener('click', function() {
		console.log(this.dataset.index);
	});
	document.body.appendChild(btn);
}
```

#### Task 4. Cache buster function.

Write a JS function `cachebuster`.
- [x] The function should return new unique value (string or integer) every 5 minutes. See example below.
- [x] Make this function as short as it is possible.


```javascript
function cachebuster() {
	// your code goes here
	var updateInterval = 1000 * 60 * 5; //How often a new code should generate, in milliseconds

	if (!window.uuidHistory)
		window.uuidHistory = [];

	if (window.uuidHistory.length < 1 || Date.now() - window.uuidHistory[window.uuidHistory.length-1].time >= updateInterval) {
		window.uuidHistory.push({
			time: Date.now(),
			uuid: uuid()
		});
	}

	function uuid() {
		var chars = '0123456789abcdefghijklmnopqrstuvwxyz';
		var blocks = [];
		for (var i=0; i<5; i++) {
			var str = '';
			for (var j=0; j<5; j++) {
				str += chars[Math.floor(Math.random() * chars.length)];
			}
			blocks.push(str);
		}
		return blocks.join('-');
	}

	return window.uuidHistory[window.uuidHistory.length-1].uuid;

}

console.log(cachebuster()); // Called immediately, outputs string or integer, e.g. "abcd" or 1234
console.log(cachebuster()); // Called after 1 minutes, outputs the same string: "abcd" or 1234
console.log(cachebuster()); // Called after 2 minutes, still outputs: "abcd" or 1234

// ...

console.log(cachebuster()); // Called after 5 minutes, outputs new unique value: e.g. "abce" or 1235
console.log(cachebuster()); // Called after 6 minutes, outputs previous value: "abce" or 1235

// ...

console.log(cachebuster()); // Called after 10 minutes, outputs another one new unique value, like "abcf" or 1236

```


## Instructions

- Please clone this repo in a new `Bitbucket` (or `GitHub`) private repo.
- Edit `README.md` file to provide answers on tasks `Tasks 1-4`. 
- Implement Angular JS app described in `Task 5` and push changes in your repo.
 

We suppose this test require from 2 to 3 hours. Thanks in advance for your time spent on this test! 
