## Lua basics

This is some basic information on how Lua scripting works. Think of it as an introduction and a tutorial.
If you want to broaden your knowledge I highly recommend checking out the [official Lua documentation](https://www.lua.org/pil/contents.html) as it contains much more detailed information.

&nbsp;

### Variables

Variables in Lua can store different [types of data](https://www.lua.org/pil/2.html), such as integers, strings, and floats. Similar to many other programming languages, Lua has local and [global](https://www.lua.org/pil/1.2.html) variables. However, unlike most programming languages, Lua automatically determines the data type of a variable (e.g., int, string, float) without explicitly specifying it, similar to JavaScript's `var` or C++'s `auto` keyword. Here is an example of how variables are defined in Lua:

``` lua
My_variable = "my text"
local my_local_variable = "my text"
```

#### Local variables

The `local` keyword in Lua indicates that a variable, such as `my_local_variable` in this case, is local and only accessible within the currently active function or, if it is outside of a function, within the current script file. 

Example of a `local` variable definition:

``` lua title="local variables.lua"
local function fun()
	local first_var = 1
	local second_var = "two"
end

print(second_var) -- script will not run as "second_var" is only
-- defined in the function and not in the whole script file. 
```

``` lua title="more locals.lua"
local third_var = "three"
local fourth_var = 4

local function fun()
	print(third_var) -- script will run because third_var
					 -- is defined in the current context.
end
```


#### Global variables

If the `local` keyword is skipped and a value is directly assigned to a variable name, it becomes a global variable. This means that other scripts running on the same machine can access its value.

``` lua title="script1.lua"
local text = "i am a variable" -- local variable, accessible only inside script1.lua
moretext = "i have more text" -- global variable

local function fun()
	less_text = "less text!" -- global variable, value assigned in
			-- function called fun(), can be accessed anywhere in
			-- this script and other scripts running on the same machine
end
```

``` lua title="script2.lua"
print(text)
print(moretext)
print(less_text)
```

If we tried running these two scripts (first we run `script1.lua`, then `script2.lua`) the second script will throw an error, because the variable `text` is not defined in its scope.

``` lua title="script2.lua (edited)"
-- print(text) -- comment out the line as variable text is undefined
print(moretext)
print(less_text)
```

This example will compile and output `i have more text` and `less text!` into the console, because `script2.lua` can read the text in `moretext`and `less_text` as they are global variables.

???+ warning "Global variables"
	To avoid conflicts with other scripts, global variables should only be used when writing scripts that are designed to be accessed by other scripts, for example APIs/libraries.

	Additionally, you should always try to avoid using variable names that often appear in other scripts (like `menu`, `x`, `y` etc.). If you really want to use variables like `menu`, consider capitalising the first letter (`Menu`) or use underscores in front of the variable names along with first letter capitalisation (`_Menu`).

	When writing public libraries or APIs you should make your code as readable as possible. Don't use difficult to understand names (`var_35` or `_ba94ol`) and instead use longer ones (`can_button_be_clicked`, `is_value_override_enabled` or `current_player_movement_speed`) that would carry more meaning. You have autocomplete, why not make use of it?

&nbsp;

### Variable naming
More information is available in the Lua documentation [[1]](https://www.lua.org/pil/1.3.html). Just like in C++ and other programming languages, when creating variables you must follow these rules:

* Names can contain letters, digits and underscores
* Names must begin with either a letter or an underscore (`_`)
* Names are case sensitive (myVar and myvar are different variables)
* Names cannot contain whitespaces (` `) or special characters like `!`, `#`, `%`, etc.
* Reserved words (like Lua keywords, such as `local` or `for`) cannot be used as names

<br>
The following are **VALID** examples of variable names:

``` lua
local myVar				-- starts with a letter, has no spaces or special characters
local number_variable	-- starts with a letter, has no spaces and has an underscore
local _var				-- starts with an underscore, has no spaces
local lineOf_text1125	-- starts with a letter, has no spaces, has numbers and an underscore
```
	
<br>
The following are **INVALID** examples of variable names:

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
	
	???+ warning "Your code, your style"
		You don't have to use any style mentioned in this documentation/tutorial. You are free to choose whatever style you desire - it could be the official C++ style, Google's C++ style or anything else, just make sure that it is easy for you to understand and write in.

	<h3>Example style 1</h3>
	
	* for variables, start with a lowercase letter and capitalise every other word, for example `local myVariableHere`
	* for functions, start with a capital letter and capitalise every other word, for example `local function DoMathEquation()`
	
	<h3>Example style 2</h3>
	
	* for variables, start with a lowercase letter and put an underscore in between each word, for example `local my_variable_here`
	* for functions, start with a capital letter and put an underscore in between each word, for example `local function Do_math_equation()`

???+ warning "Naming styles"
	When you choose a naming style, always stick to it. That way, you will eventually get used to writing using only that style without ever having to think.
	<br>
	It is also important to note, that using multiple different styles in one project / file should be avoided. This also applies to whenever you edit someone else's code - stick to their style or, if the code is simple, rewrite it in your own style and **stick to it**.
	
&nbsp;
	
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

&nbsp;

### Other features of Lua
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