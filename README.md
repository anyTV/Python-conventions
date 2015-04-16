# Python Coding Conventions

List of standards for the most commonly used codes and patterns in Python. Conventions will allow developers to create code bases that will be easier for other developers to read and understand.


Use `pylint` and `pep8` for checking if the codes follow standard. To install, run this commands:
<!-- language:console -->
	pip install pylint
	pip install pep8
	
If you are using Sublime, you can integrate pylint and pep8 through SublimeLinter. See instructions for [SublimeLinter-pylint](https://github.com/SublimeLinter/SublimeLinter-pylint) and [SublimeLinter-pep8](https://github.com/SublimeLinter/SublimeLinter-pep8).

Use Python PEP8 Autoformat to automatically format your code to pep8 standards. See [docs](https://bitbucket.org/StephaneBunel/pythonpep8autoformat) for instructions.


### Naming Convention

1. General Naming Guide

	- Be descriptive with naming without being too wordy
	- Avoid names using single character as much as possible. 

2. Global Variable Names, Functions, Packages and Modules

	- Package names should be in lower case.
	- Use underscore if multiple words are needed. `my_cool_package`
	- Avoid Global Variables!

3. Classes

	- Classes should follow the UpperCaseCamelCase convention. `MyVeryOwnClass`
	- Exception Classes should end in 'Error'
	
4. Instance Variables and Method Names

	- Lowercase with words separated by underscores as necessary to improve readability. `my_var`, `run_method`
		- Non-public instance variables should begin with a single underscore. `_im_hidden`
	
5. Constants

	- Constant names must be fully capitalized.
	- Words in a constant name should be separated by an underscore. `MY_NEW_CONSTANT`

###Code Layout

1. Maximum line length is 72 characters.
2. Blank lines 
	
	- Separate top-level function and class definitions with `two blank lines`.
	- Method definitions **inside a class** are separated by a `single blank line`.
	- Use blank lines in functions, sparingly, to indicate logical sections.
	
3. Indentation
	
	Use 4 spaces per indentation level. `Hanging indents`, code that is a continuation of the line above, should be indented to the next level.
	```python
		
		#Good
		
		# Aligned with opening delimiter.
		foo = long_function_name(var_one, var_two,
                         		var_three, var_four)

		# More indentation included to distinguish this from the rest.
		def long_function_name(
        		var_one, var_two, var_three,
        		var_four):
    		print(var_one)

		# Hanging indents should add a level.
		foo = long_function_name(
    		var_one, var_two,
    		var_three, var_four)
		
		#Bad
		
		# Arguments on first line forbidden when not using vertical alignment.
		foo = long_function_name(var_one, var_two,
    		var_three, var_four)

		# Further indentation required as indentation is not distinguishable.
		def long_function_name(
    		var_one, var_two, var_three,
    		var_four):
    		print(var_one)
   	```	    		
	
	The closing brace/bracket/parenthesis on multi-line constructs may be lined up under the first character of the line that starts the multi-line construct
	```python
		
		my_list = [
    		1, 2, 3,
    		4, 5, 6
		]
		
		result = some_function_that_takes_arguments(
    		'a', 'b', 'c',
    		'd', 'e', 'f'
		)
	```

4. Imports
	- Imports should occur at the top of the module, after any module docstring
	- Use of absolute imports is much more recommended. Wildcard imports should be avoided
	- Standard imports, those that uses the `import` keyword, should each be in a separate file

	```python
			
		#Good
			
		import os
		import sys
			
		#Bad
			
		import os, sys
	```
	
	- Imports should be grouped in the following order:
		1. standard library imports
		2. related third party imports
		3. local application/library specific imports	
5. Whitespaces

	Avoid extraneous whitespace in the following situations:
	
	```python
		
		#Good
		spam(ham[1], {eggs: 2})
		spam(1)
		
		#Bad  
		spam( ham[ 1 ], { eggs: 2 } )
		spam (1)
		
		
		#Good
		if x == 4: print x, y; x, y = y, x
		
		x = 1
		y = 2
		long_variable = 3
		
		#Bad
		if x == 4 : print x , y ; x , y = y , x
		
		x             = 1
		y             = 2
		long_variable = 3
		
		
		#Good
		ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
		ham[lower:upper], ham[lower:upper:], ham[lower::step]
		ham[lower+offset : upper+offset]
		ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
		ham[lower + offset : upper + offset]		
		#Bad
		ham[lower + offset:upper + offset]
		ham[1: 9], ham[1 :9], ham[1:9 :3]
		ham[lower : : upper]
		ham[ : upper]
		
		#Good
		dct['key'] = lst[index]		
		
		#Bad
		dct ['key'] = lst [index]
		
	```	

6. Other Code Patterns
	
	Surround operators with white spaces. If operators with different priorities are used, you can group them using spaces.
	
	```python
		
		#Good 
		
		i = i + 1
		submitted += 1
		x = x*2 - 1				#grouped operators
		hypot2 = x*x + y*y
		c = (a+b) * (a-b)
		
		#Bad
		
		i=i+1
		submitted +=1
		x = x * 2 - 1
		hypot2 = x * x + y * y
		c = (a + b) * (a - b)
	```
		
	Don't use spaces around the = sign when used to indicate a keyword argument or a default parameter value.
	
	```python
		
		#Good
		
		def complex(real, imag=0.0):
			return magic(r=real, i=imag)
			
		#Bad
		
		def complex(real, imag = 0.0):
			return magic(r = real, i = imag)
	
	```
    	
	Don't put multi-clause statements on the same line, especially when dealing with if, for ,while , try, catch.
	
	```python
    	
    		#Really Bad
    	
    		if foo == 'blah': do_blah_thing()
			else: do_non_blah_thing()

			try: something()
			finally: cleanup()

			do_one(); do_two(); do_three(long, argument,
                             list, like, this)

			if foo == 'blah': one(); two(); three()
		
	```	
	 
	Use `is not` operator rather than `not ... is`
	
	```python
	
		#Good 
	
		if foo is not None:
		
		#Bad
		
		if not foo is None:
	```
		
	Always use a def statement instead of an assignment statement that binds a lambda expression directly to an identifier.
	
	```python
		#Good
		
		def f(x): return 2*x
		
		#Bad
		
		f = lambda x: 2*x
		
	```	
		
	When catching exceptions, mention specific exceptions whenever possible instead of using a bare `except:` clause. Derive exceptions from Exception rather than BaseException
	
	```python
	
		try:
    		import platform_specific_module
		
		# defines the exception 'ImportError' 
		# instead of just using the except which will accept BaseException
		except ImportError:						
    		platform_specific_module = None	
		
	```
	
	When binding caught exceptions to a name, prefer the explicit name binding syntax
		
	```python
		
		try:
    		process_data()
		
		# raise DataProcessingFailedError, str(exc) is not supported in Python 3
		except Exception as exc:
    		raise DataProcessingFailedError(str(exc))
	```
	
	Be consistent in return statements. Either all return statements in a function should return an expression, or none of them should. If any return statement returns an expression, any return statements where no value is returned should explicitly state this as return `None` , and an explicit return statement should be present at the end of the function.

	```python
		
		#Good
		
		def foo(x):
    		if x >= 0:
        		return math.sqrt(x)
    		else:
        		return None

		def bar(x):
    		if x < 0:
        		return None
    		return math.sqrt(x)

		#Bad
		
		def foo(x):
    		if x >= 0:
        		return math.sqrt(x)

		def bar(x):
    		if x < 0:
        		return
    		return math.sqrt(x)
	```
    		
	Use `.startswith()` and `.endswith()` instead of string slicing to check for prefixes or suffixes.
    	
	```python
	
		#Good
		
		if foo.startswith('bar'):
		
		#Bad
		
		if foo[:3] == 'bar':
	    	
	```
    	
	Object type comparisons should always use isinstance() instead of comparing types directly.
    
	```python
    	
		#Good
		
		if isinstance(obj, int):
		
		#Bad
		
		if type(obj) is type(1):
	```
    	
	For sequences, (strings, lists, tuples), use the fact that empty sequences are false.
    
	```python
	
		#Good
		
		if not seq:
		if seq:
		
		#Bad
		
		if len(seq):
		if not len(seq):	
	```
    	
	Don't compare boolean values to True or False using `==`
    
	```python
		
		#Good
		
		if greeting:
		
		#Bad
		
		if greeting == True:
		if greeting is True:
		
	```
--------------------------------------------------------------------------------

References:

- [Pep8](https://www.python.org/dev/peps/pep-0008/#string-quotes) - Style Guide for Python Code
- Google Python Style [Guide](https://google-styleguide.googlecode.com/svn/trunk/pyguide.html)
- Python Coding Conventions by AnthonyReid99	 [link](http://visualgit.readthedocs.org/en/latest/index.html#)

