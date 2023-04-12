## Lua basics

This is some basic information on how Lua scripting works. Think of it as an introduction and a tutorial.
If you want to broaden your knowledge I highly recommend checking out the [official Lua documentation](https://www.lua.org/pil/contents.html) as it contains much more detailed information.

### Variables

Variables hold certain [types of data](https://www.lua.org/pil/2.html). In Lua, just like a lot of other programming languages, there are local and [global](https://www.lua.org/pil/1.2.html) variables. However, unlike most programming languages, in Lua, the data type (int, string, float etc.) is determined automatically (just like in Javascript or in C++ using the `auto` keyword. Here is an example of defining variables:

``` lua
My_variable = "my text"
local my_local_variable = "my text"
```

The keyword `local` indicates that the variable we created, in this case `my_local_variable`, is local and only accessible inside the currently active function (or if it is outside of a function, in the current script file). Skipping the keyword `local` and just assigning a value to a variable name makes it a global variable. What this means is that other scripts running on the same machine can access its value.
``` lua title="script1.lua"
local text = "i am a variable"
moretext = "i have more text"
```

``` lua title="script2.lua"
print(text)
print(moretext)
```

If we tried running these two scripts (first we run `script1.lua` then `script2.lua`) the second script will throw an error, because the variable `text` is not defined in its scope.

``` lua title="script2.lua (edited)"
-- print(text) -- comment out the line as variable text is undefined
print(moretext)
```

This example will compile and output `i have more text` into the console, because `script2.lua` can read the text in `moretext` as it is a global variable.

### Variable naming
More information is available in the Lua documentation [[1]](https://www.lua.org/pil/1.3.html). Just like in C++ and other programming languages, when creating variables you must follow these rules:

* Names can contain letters, digits and underscores
* Names must begin with a letter or an underscore (_)
* Names are case sensitive (myVar and myvar are different variables)
* Names cannot contain whitespaces ( ) or special characters like !, #, %, etc.
* Reserved words (like Lua keywords, such as `local` or `for`) cannot be used as names

<br>
The following are **GOOD** examples of variable names:

``` lua
local myVar				-- starts with a letter, has no spaces or special characters
local number_variable	-- starts with a letter, has no spaces and has an underscore
local _var				-- starts with an underscore, has no spaces
local lineOf_text1125	-- starts with a letter, has no spaces, has numbers and an underscore
```
	
<br>
The following are **BAD** examples of variable names:

``` lua
local 1var2				-- bad, starts with a number
local !hello			-- bad, starts with a special character
local v@r1@b13			-- bad, has special characters
local lineOf text1125	-- bad, has a space
local for				-- bad, for is a reserved word
```

???+ note "Naming styles"
	When you first start coding you might feel a bit lost on how you should name your variables. You might also think that it makes no difference to how the program works and executes commands and you would be correct. Unfortunately, programming is not as easy as you might think. Sometimes you can make a mistake and fixing it requires editing the code. Using a proper naming and coding style will help you understand the code better and detect errors much quicker.
	
	Of course, you can do whatever you desire as it is your code, but sticking to a single proper style makes your code much easier to read and understand. You can try either of these styles and see which is more to your liking.
	
	<h3>Style 1</h3>
	
	* for variables, start with a lowercase letter and capitalise every other word, for example `local myVariableHere`
	* for functions, start with a capital letter and capitalise every other word, for example `local function DoMathEquation()`
	
	<h3>Style 2</h3>
	
	* for variables, start with a lowercase letter and put an underscore in between each word, for example `local my_variable_here`
	* for functions, start with a capital letter and put an underscore in between each word, for example `local function Do_math_equation()`

???+ warning "Naming styles"
	When you choose a naming style, always stick to it. That way, you will eventually get used to writing using only that style without ever having to think.
	<br>
	It is also important to note, that using multiple different styles in one project / file should be avoided. This also applies to whenever you edit someone else's code - stick to their style or, if the code is simple, rewrite it in your own style and **stick to it**.
	
### Functions
More information is available in the Lua documentation [[1]](https://www.lua.org/pil/2.6.html)[[2]](https://www.lua.org/pil/5.html). A function is a group of statements that together perform a task. An example of a function would be the following:

``` lua title="myfirstfunction.lua"
local function addtwo(a, b)
	return a + b
end
```

Let's analyse the code above one step at a time. The first line, `local function addtwo(a, b)` has the `local` keyword, the word `function`, the function name `addtwo` and two parameters `a` and `b`.

* `local` makes the function only accessible in the `myfirstfunction.lua` script file
* `function` tells the interpretor (compiler) that we are defining a function and not a variable
* `addtwo` is a name; it follows the same naming conventions as normal variables
* `(a, b)`, from which `a` and `b` are parameters that must have arguments passed when calling the function; the parentheses tell the interpreter that in the function definition we have two variables `a` and `b`.

<br>
The next line, `return a + b`, is very simple. The keyword `return` means that this is where the function should finish it's job and return a value, in our case it is `a + b`.

* `return` is a keyword used to return a value, essentially the result of the function, for example:
	``` lua title="myfirstfunction.lua"
	local function addtwo(a, b)
		return a + b
	end
	local sum = addtwo(2, 4) -- return value is 6, so `sum` is 6
	print(sum) -- will print 6
	```
	
	???+ note
		Functions don't have to return a value, meaning the return statement is not necessary.
		The keyword `return` can also be used to end the function at any point.
		
* `a + b` is what we want the function to return. Because we called the function `addtwo`, we want it to return a sum of the numbers we gave it.

<br>
You might've just noticed a few new terms - calling a function and passing arguments to functions.

* Calling a function means we are essentially telling the function to start: `addtwo(2, 4)`
* Passing the arguments means we give the function's parameters a value, in this case, `a` will be set to `2` and `b` will be set to `4`
* The return value will be `6` because `2 + 4` is `6`.

<br>
The final line contains a single keyword - `end`. It simply means the end of a function. For example, in Lua we would type:

``` lua
local function func()
	-- code here
	return
end
```

but in C/C++ we don't use `end`, instead we use curly brackets:

``` cpp
void func() {
	// code here
	return;
}
```

Essentially speaking, the `end` keyword works just like the closing brackets in other programming languages (C/C++/Java/Javascript etc).

### Other useful features of Lua
More information is available in the Lua documentation [[1]](https://www.lua.org/pil/4.3.html)[[2]](https://www.lua.org/pil/4.4.html). The keyword `end` is not only used at the end of a function definition, but also in the [`if`](https://www.lua.org/pil/4.3.1.html) statement, along with [`for`](https://www.lua.org/pil/4.3.4.html) and [`while`](https://www.lua.org/pil/4.3.2.html) loops, for example:
``` lua title="if.lua"
local a = 1
if a == 1 then          -- if a is 1 then
    print("a = 1")      -- print `a = 1`
elseif a == 2 then     -- if a is not 1 and is 2 then
    print("a = 2")      -- print `a = 2`
else                    -- if a is not 1 nor 2
    print("a = " .. a)  -- print `a = ?` where ? is the value of a
end
```

``` lua title="forloop.lua"
for i = 1, 10 do
	print(i)
end
```

* `for` starts the loop, `i = 1` creates a local variable `i` and assigns the value `1` to it, `10` means how many times the loop should repeat and `do` is the starting point of the loop
* `print(i)` prints the current value of `i` to the console (1 - 10)
* `end` means the end of the loop

``` lua title="whileloop.lua"
local i = 0
while i < 10 do
    i = i + 1
    print(i)
end
```

* `local i = 0` defines a new variable called `i` and assigns the value `0` to it
* `while` is a loop that executes as long as the following condition (`i < 10`) is true, do is the starting point of the loop
* `i = i + 1` is required as the while loop does not automatically increment `i`
* `print(i)` prints the current value of `i` to the console (1-10)
* `end` means the end of the loop

More detailed code examples [[1]](https://www.lua.org/pil/4.3.html).