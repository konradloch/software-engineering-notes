### Go

#### Slices
- be aware of recreating whole slice when capacity is fulified
- when using slice as a buffer then specify length
- when you want to copy array (for mapping for example) create the same new array
- for other situations create slice with zero length and specified capacity.
- slices of slice shares memory
- using slice of slice, use full slice expression [low:high:max], then after appending new elements - new slice will be created. Copy function also might be used.

- making slice, means start pointing at value we want from origin slice/array
- slice is copied to function as a pointer, lenght and capacity. modifying slice will modify oroginal and a copy, but appedning new elements will be only visible in copy because data is shared but lenght and capacity can't be modified.
-  Your function’s documentation should specify if it modifies the slice’s contents.



#### Strings
- Go uses a sequence of bytes to represent a string. It means slice and len() operates on bytes (UTF-8 has from 1 to 4 bytes)

#### Map
- Maps equality cannot by check by /=/= , only nilability can be checked.
- The key for a map can be any comparable type. This means you cannot use a slice or a map as the key for a map.
- Use a map when the order of elements doesn’t matter. Use a slice when the order of elements is important.
- iterating over map probably always will be in different order to prevent people who assumed static order in Maps and prevent Hash Dos.


#### Set
Set not exist as separate type. It has to be implemented or library should be used.

#### Blocks
- inside inner block, variables are shadowing (using := but not using = ) it means that we got their value from outter block but when we modify them then it make no change in outer block
- some build-in types, constatns and functions are not definied as Go keywords. They are evaluated (_predeclared identifier_) in universe block.
- shadows might be found by shadow lib.

#### IF
- If condiditon dones't have parantheseis
- there is ability to declare varaible which will be avalible only in if block.
	-  `if n := rand.Intn(10); n == 0 {}`
	- use this feature only for variables which needs this scope

#### FOR
- Use a for-range loop to access the runes in a string in order. The key is the number of bytes from the beginning of the string, but the type of the value is rune.
- The for-range value is a copy
- using continue and break is ok. Most of the "dangers" associated with using break or continue in a for loop are negated if you write tidy, easily-readable loops. If the body of your loop spans several screen lengths and has multiple nested sub-blocks, yes, you could easily forget that some code won't be executed after the break. If, however, the loop is short and to the point, the purpose of the break statement should be obvious.
- An infinite for loop is also used to implement some versions of the iterator pattern
- main point is to write the most elegnant ans short code as possible

#### switch
-  if there are multiple values that should trigger the exact same logic? In Go, you separate multiple matches with commas, like we do when matching 1, 2, 3
- fallthrough keywoard shouldbe used to make dependencies beetween cases.
- blank switches are like if else block
- Favor blank switch statements over if/else chains when you have multiple related cases. Using a switch makes the comparisons more visible and reinforces that they are a related set of concerns.

#### Functions
- Multiple Return Values Are Multiple Values, not like tuple in Python
- Use _ whenever you don’t need to read a value that’s returned by a function.
- named return variables are under shadowing
- If your function returns values, never use a blank return. It can make it very confusing to figure out what value is actually returned.
- functions are values
-  Error handling is what separates the professionals from the amateurs.
-  function type might be definied like struct
-  Using `defer` can feel strange if you are used to a language that uses a block within a function to control when a resource is cleaned up, like the `try/catch/finally` blocks in Java,
-  Every type in Go is a value type. It’s just that sometimes the value is a pointer.

#### pointers
- pointers use nil as a zero/null value (this is a reason why slices and maps has nil defualt values (because pointer usage))
- constant exist only at compile time, so poinitg is unvalibale, to handle this problem use a helper function to turn a constant value into a pointer.
- for update value under pointer use *p = value
- Rather than populating a struct by passing a pointer to it into a function, have the function instantiate and return the struct
- if you are passing megabytes of data between functions, consider using a pointer even if the data is meant to be immutable.
- Use a pointer value for fields in the struct that are nullable.
- When not working with JSON (or other external protocols), resist the temptation to use a pointer field to indicate no value. While a pointer does provide a handy way to indicate no value, if you are not going to modify the value, you should use a value type instead, paired with a boolean.
- The reason you can pass a slice of any size to a function is that the data that’s passed to the function is the same for any size slice: two `int` values and a pointer. The reason that you can’t write a function that takes an array of any size is because the entire array is passed to the function, not just a pointer to the data.
- A common source of bugs in C programs is returning a pointer to a local variable. In C, this results in a pointer pointing to invalid memory. The Go compiler is smarter. When it sees that a pointer to a local variable is returned, the local variable’s value is stored on the heap.

#### GC
- Jeff Dean, the genius behind many of Google’s engineering successes, co-wrote a paper in 2013 called The Tail at Scale. It argues that systems should be optimized for latency, to keep response times low. The garbage collector used by the Go runtime favors low latency. Each garbage collection cycle is designed to take less than 500 microseconds. However, if your Go program creates lots of garbage, then the garbage collector won’t be able to find all of the garbage during a cycle, slowing down the collector and increasing memory usage.

#### Types
- When a type has _any_ pointer receiver methods, a common practice is to be consistent and use pointer receivers for _all_ methods, even the ones that don’t modify the receiver.
- When you use a pointer receiver with a local variable that’s a value type, Go automatically converts it to a pointer type. In this case, c.Increment() is converted to (&c).Increment().
- do not write getter and setter methods for Go structs, unless you need them to meet an interface. Go encourages you to directly access a field. Reserve methods for business logic. The exceptions are when you need to update multiple fields as a single operation or when the update isn’t a straightforward assignment of a new value.
-  Just like nil parameters passed to functions, if you change the copy of the pointer, you haven’t changed the original. This means you can’t write a pointer receiver method that handles nil and makes the original pointer non-nil. If your method has a pointer receiver and won’t work for a nil receiver, check for nil and return an error
-  Types Are Executable Documentation
-  iota Is for Enumerations—Sometimes
-  The software engineering advice “Favor object composition over class inheritance” dates back to at least the 1994 book Design Patterns by Gamma, Helm, Johnson, and Vlissides (Addison-Wesley), better known as the Gang of Four book. While Go doesn’t have inheritance, it encourages code reuse via built-in support for composition and promotion:
-  You can embed any type within a struct, not just another struct. This promotes the methods on the embedded type to the containing struct.

#### Interfaces
- Interfaces specify what callers need. The client code defines the interface to specify what functionality it requires.
- If there’s an interface in the standard library that describes what your code needs, use it!
- Just like you can embed a concrete type in a struct, you can also embed an interface in a struct.
- There is one potential drawback to this pattern. As we discussed in “Reducing the Garbage Collector’s Workload”, reducing heap allocations improves performance by reducing the amount of work for the garbage collector. Returning a struct avoids a heap allocation, which is good. However, when invoking a function with parameters of interface types, a heap allocation occurs for each of the interface parameters. Figuring out the trade-off between better abstraction and better performance is something that should be done over the life of your program. Write your code so that it is readable and maintainable. If you find that your program is too slow and you have profiled it and you have determined that the performance problems are due to a heap allocation caused by an interface parameter, then you should rewrite the function to use a concrete type parameter. If multiple implementations of an interface are passed into the function, this will mean creating multiple functions with repeated logic.
- These situations should be relatively rare. Avoid using interface{}. As we’ve seen, Go is designed as a strongly typed language and attempts to work around this are unidiomatic.
- You can further protect yourself from unexpected interface implementations by making the interface unexported and at least one method unexported. If the interface is exported, then it can be embedded in a struct in another package, making the struct implement the interface. 

#### Functions:
- If your single function is likely to depend on many other functions or other state that’s not specified in its input parameters, use an interface parameter and define a function type to bridge a function to the interface. That’s what’s done in the http package; it’s likely that a Handler is just the entry point for a chain of calls that needs to be configured. However, if it’s a simple function (like the one used in sort.Slice), then a parameter of function type is a good choice.
- https://github.com/google/wire
- In most cases, it is very bad form to ignore the values returned from a function. Please avoid this, except for cases like fmt.Println.

#### method vs functions
- The differentiator is whether or not your function depends on other data. As we’ve covered several times, package-level state should be effectively immutable. Any time your logic depends on values that are configured at startup or changed while your program is running, those values should be stored in a struct and that logic should be implemented as a method. If your logic only depends on the input parameters, then it should be a function.


#### Errors
- There are two very good reasons why Go uses a returned error instead of thrown exceptions. First, exceptions add at least one new code path through the code. These paths are sometimes unclear, especially in languages whose functions don’t include a declaration that an exception is possible. This produces code that crashes in surprising ways when exceptions aren’t properly handled, or, even worse, code that doesn’t crash but whose data is not properly initialized, modified, or stored.
- The second reason is more subtle, but demonstrates how Go’s features work together. The Go compiler requires that all variables must be read. Making errors returned values forces developers to either check and handle error conditions or make it explicit that they are ignoring errors by using an underscore (_) for the returned error value.
- Exception handling may produce shorter code, but having fewer lines doesn’t necessarily make code easier to understand or maintain. As we’ve seen, idiomatic Go favors clear code, even if it takes more lines.Another thing to note is how code flows in Go. The error handling is indented inside an if statement. The business logic is not. This gives a quick visual clue to which code is along the “golden path” and which code is the exceptional condition.
- fmt.Errorf for formatted error message
- The Go philosophy is that it’s better to keep the language simple and trust the developers and tooling than it is to add additional features
- When using custom errors, never define a variable to be of the type of your custom error. Either explicitly return nil when no error occurs or define the variable to be of type error.
- If you want to create a new error that contains the message from another error, but don’t want to wrap it, use fmt.Errorf to create an error, but use the %v verb instead of %w:
- Use errors.Is when you are looking for a specific instance or specific values. Use errors.As when you are looking for a specific type.
- You must call recover from within a defer because once a panic happens, only deferred functions are run.
- Go favors code that explicitly outlines the possible failure conditions over shorter code that handles anything while saying nothing.
- When you have a stack trace in your error, the output includes the full path to the file on the computer where the program was compiled. If you don’t want to expose the path, use the -trimpath flag when building your code. This replaces the full path with the package.

#### Repo, modules, package.
- While you can store more than one module in a repository, it isn’t encouraged. Everything within a module is versioned together. Maintaining two modules in one repository means tracking separate versions for two different projects in a single repository.
- packages should have simple names, withour repatiting and without generic names. It is better to make extract/Names than util/ExtractNames where (packages)/(Function)
- Our sample program was checked in without go.sum and with an incomplete go.mod. This was done so you could see what happens when these files are populated. When committing your own projects to source control, always include up-to-date go.mod and go.sum files. Doing so specifies exactly what versions of your dependencies are being used.

#### Concurency 
- Any time you are reading from a channel that might be closed, use the comma ok idiom to ensure that the channel is still open.

#### TO READ
- https://oreil.ly/v_urr
- https://oreil.ly/juu44
- https://oreil.ly/c_gvC
- https://oreil.ly/UUhGK
- https://oreil.ly/cvLpa
- https://github.com/google/wire
- https://oreil.ly/TiJnS