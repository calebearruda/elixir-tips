# elixir-tips

The collection of Elixir Tips and Tricks...

## Part 1

### 1. Multiple [ OR ]

This is just the other way of writing Multiple **OR** conditions. This is not the recommended approach because in regular approach when the condition evaluates to **true** , it stops executing the remaining conditions which saves time of evaluation unlike this approach which evaluates all conditions first in list. This is just bad but good for discoveries. 

<script src="https://gist.github.com/blackode/9e3d873ad803ef6d4f653d8bf2e1b028.js"></script>

### 2. i( term) Elixir Term Type and Meta Data

Prints information about the data type of any given term. Try that in `iex` and see the magic.

```elixir
iex> i(1..5)
```

### 3. iex Custom Configuration - iex Decoration

Save the following file as `.iex.exs` in your `~` home directory and see the magic.

<script src="https://gist.github.com/blackode/5728517116d7a4d08f0a4faddd8c145a.js"></script>



![img](https://cdn-images-1.medium.com/max/800/1*iy-IELdB8fjTo5H0sABlBQ.png)

### 4. Creating Custom Sigils and Documenting

Each `x` sigil call respective `sigil_x` definition

<script src="https://gist.github.com/blackode/15ddca326d604fbef68ae833504ac37e.js"></script>

### 5. Custom Error Definitions

5. Custom Error Definitions

#### Define Custom Error

```elixir
defmodule BugError do
   defexception message: "BUG BUG .." # message is the default
end
```

**Usage**

```elixir
$ iex bug_error.ex
iex> raise BugError
** (BugError) BUG BUG ..
iex> raise BugError, message: "I am Bug.." #here passing the message dynamic
** (BugError) I am Bug..
```

### 6. Get a Value from Nested Maps Easily

<script src="https://gist.github.com/blackode/c19472093bedff864a5e6363784dd026.js"></script>

Getting a Value from Nested Maps

### 7. With Statement Benefits

The special form `with` is used to chain a sequence of matches in order and finally return the result of `do:` if all the clauses match. However, if one of the clauses does not match, its result of the miss matched expression is immediately returned.

```elixir
iex> with 1 <- 1+0,
          2 <- 1+1,
          do: IO.puts "all matched"
"all matched"
```

```elixir
iex> with 1 <- 1+0,
          2 <- 3+1,
          do: IO.puts "all matched"
4
## since  2 <- 3+1 is not matched so the result of 3+1 is returned.Writing Protocols**
```

### 8. Writing Protocols

#### Define a Protocol

A **Protocol** is a way to dispatch to a particular implementation of a function based on the type of the parameter.
The macros `defprotocol` and `defimpl` are used to define Protocols and Protocol implementations respectively  for different types in the following example.

```
defprotocol Triple do    
  def triple(input)  
end  

defimpl Triple, for: Integer do    
  def triple(int) do     
    int * 3   
  end  
end   

defimpl Triple, for: List do
  def triple(list) do
    list ++ list ++ list   
  end  
end 
```

#### Usage

Load the code into `iex` and execute

```
iex> Triple.triple(3) 
9
Triple.triple([1, 2])
[1, 2, 1, 2,1,2]
```

### 9. Ternary Operator

There is no ternary operator like `true ? "yes" : "no"` . So, the following is suggested.

```elixir
"no" = if 1 == 0, do: "yes", else: "no"
```

### 10. Advantage of Kernel.||

When using pipelines, sometimes we break the pipeline for `or` operation. 
For example:

```
result = :input
|> do_something
|> do_another_thing
```

```
# Bad
result = (result || :default_output)
|> do_something_else
```

Indeed, `||` is only a shortcut for `Kernel.||` . We can use `Kernel.||` in the pipeline instead to avoid breaking the pipeline.

The code above will be:

```
result = :input
|> do_something
|> do_another_thing
|> Kernel.||(:default_output)  #<-- This line
|> do_something_else
```

This above tip is from [qhwa](https://medium.com/@qhwa_85848)

