jQuery.IO
===

A jQuery plug-in for transforming data between different formats:

- JavaScript objects
- html forms
- json strings
- query strings

Convert a form
----------

### To a JavaScript object

	$.io.form($('form')).object();

	{
		user: {
			name: 'Sam',
			interests: ['1', '2']
		}
	}

### To a query string

	$.io.form($('form')).query();

	'user%5Bname%5D=Sam&user%5Binterests%5D%5B%5D=1&user%5Binterests%5D%5B%5D=2'

	// this is equivalent to:

	$('form').serialize();

### To a json string

	$.io.form($('form')).json();

	'{"user":{"id":"1","name":"Sam","interests":["1","2","3"]}}'

Convert Query strings
------------

### To a JavaScript object

	var source = 'user%5Bname%5D=Sam&user%5Binterests%5D%5B%5D=1&user%5Binterests%5D%5B%5D=2';
	$.io.query(source).object();

	{
		user: {
			name: 'Sam',
			interests: ['1', '2']
		}
	}

### To a json string

	var source = 'user%5Bname%5D=Sam&user%5Binterests%5D%5B%5D=1&user%5Binterests%5D%5B%5D=2';
	$.io.query(source).json();

	'{"user":{"id":"1","name":"Sam","interests":["1","2","3"]}}'

Convert Json
--------

### To a JS object

	var source = '{"user":{"id":"1","name":"Sam","interests":["1","2","3"]}}';
	$.io.json(source).object();

	{
		user: {
			name: 'Sam',
			interests: ['1', '2']
		}
	}

	// this is equivalent to:
	JSON.parse(source)


### To a query string

	var source = '{"user":{"id":"1","name":"Sam","interests":["1","2","3"]}}';
	$.io.json(source).query();

	'user%5Bname%5D=Sam&user%5Binterests%5D%5B%5D=1&user%5Binterests%5D%5B%5D=2'

Convert JavaScript Objects
-----------

### To a query string

	var source = 	{
		user: {
			name: 'Sam',
			interests: ['1', '2']
		}
	}
	$.io.object(source).query();

	'user%5Bname%5D=Sam&user%5Binterests%5D%5B%5D=1&user%5Binterests%5D%5B%5D=2'

### To a json string

	var source = 	{
		user: {
			name: 'Sam',
			interests: ['1', '2']
		}
	}

	$.io.object(source).json();

	'{"user":{"id":"1","name":"Sam","interests":["1","2","3"]}}'

	// this is equivalent to:
	JSON.stringify(source);

Limits
--------

Given a query like &a=101, io at the moment doesn't try to figure out if 101 is a number or a string, so it will just return a string if converted to an object. e.g. {a: '101'}

Testing
-------

	npm init
	grunt

Acknowledgements
-------------

- Bitovi (CanJS) - for some of the code I 'borrowed' for converting forms into objects.

License
-------

Copyright (c) 2013 Sebastian Porto
Licensed under the MIT license.