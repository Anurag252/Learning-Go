# Learning-Go
Go still expects there to be a single workspace for third-party Go tools installed via go install (see “Getting Third-Party Go Tools”). By default, this workspace is located in $HOME/go, with source code for these tools stored in $HOME/go/src and the compiled binaries in $HOME/go/bin. You can use this default or specify a different workspace by setting the $GOPATH environment variable.

The go run command does in fact compile your code into a binary. However, the binary is built in a temporary directory. The go run command builds the binary, executes the binary from that temporary directory, and then deletes the binary after your program finishes. This makes the go run command useful for testing out small programs or using Go like a scripting language.

`go build hello.go`
This creates an executable called hello (or hello.exe on Windows) in the current directory. Run it and you unsurprisingly see Hello, world! printed on the screen.

The name of the binary matches the name of the file or package that you passed in. If you want a different name for your application, or if you want to store it in a different location, use the -o flag. For example, if we wanted to compile our code to a binary called “hello_world,” we would use:

`go build -o hello_world hello.go`

The go install command takes an argument, which is the location of the source code repository of the project you want to install, followed by an @ and the version of the tool you want (if you just want to get the latest version, use @latest). It then downloads, compiles, and installs the tool into your $GOPATH/bin directory.

The Go development tools include a command, `go fmt`, which automatically reformats your code to match the standard format. It does things like fixing up the whitespace for indentation, lining up the fields in a struct, and making sure there is proper spacing around operators.

`goimports -l -w`

The -l flag tells goimports to print the files with incorrect formatting to the console. The -w flag tells goimports to modify the files in-place. The . specifies the files to be scanned: everything in the current directory and all of its subdirectories.

However, Go developers never put the semicolons in themselves; the Go compiler does it for them following a very simple rule described in Effective Go:

The go fmt command won’t fix braces on the wrong line, because of the semicolon insertion rule. Like C or Java, Go requires a semicolon at the end of every statement. However, Go developers never put the semicolons in themselves; the Go compiler does it for them following a very simple rule described in Effective Go:

If the last token before a newline is any of the following, the lexer inserts a semicolon after the token:

An identifier (which includes words like int and float64)

A basic literal such as a number or string constant

One of the tokens: “break,” “continue,” “fallthrough,” “return,” “++,” “--,” “),” or “}”

go lint --< coding styles

go vet -- > This includes things like passing the wrong number of parameters to formatting methods or assigning values to variables that are never used  

 golangci-lint. It combines golint, go vet, and an ever-increasing set of other code quality tools. Once it is installed, you run golangci-lint with the command:
 
 ![image](https://user-images.githubusercontent.com/4143476/138606066-38c53570-ac51-4e1e-bdff-4ad676ae7494.png)
 
 makefile example :- here target:pre-requisite is the format
 
 # Literal
 A literal in Go refers to writing out a number, character, or string. There are four common kinds of literals that you’ll find in Go programs. (There’s a rare fifth kind of literal that we’ll cover when discussing complex numbers.)
 
 To make it easier to read longer integer literals, Go allows you to put underscores in the middle of your literal. This allows you to, for example, group by thousands in base ten (1_234)

Rune literals represent characters and are surrounded by single quotes. Unlike many other languages, in Go single quotes and double quotes are not interchangeable. Rune literals can be written as single Unicode characters ('a'), 8-bit octal numbers ('\141'), 8-bit hexadecimal numbers ('\x61'), 16-bit hexadecimal numbers ('\u0061'), or 32-bit Unicode numbers ('\U00000061'). There are also several backslash escaped rune literals, with the most useful ones being newline ('\n'), tab ('\t'), single quote ('\''), double quote ('\"'), and backslash ('\\').


There are two different ways to indicate string literals. Most of the time, you should use double quotes to create an interpreted string literal (e.g., type "Greetings and Salutations"). These contain zero or more rune literals, in any of the forms allowed. The only characters that cannot appear are unescaped backslashes, unescaped newlines, and unescaped double quotes. If you use an interpreted string literal and want your greetings on a different line from your salutations and you want “Salutations” to appear in quotes, you need to type "Greetings and\n\"Salutations\"".

If you need to include backslashes, double quotes, or newlines in your string, use a raw string literal. These are delimited with backquotes (`) and can contain any literal character except a backquote. When using a raw string literal, we write our multiline greeting like so:

`Greetings and
"Salutations"`

Go lets you use an integer literal in floating point expressions or even assign an integer literal to a floating point variable. This is because literals in Go are untyped; they can interact with any variable that’s compatible with the literal. 

Booleans
The bool type represents Boolean variables. Variables of bool type can have one of two values: true or false. The zero value for a bool is false:

Numeric Types
Go has a large number of numeric types: 12 different types (and a few special names) that are grouped into three categories.

A byte is an alias for uint8; it is legal to assign, compare, or perform mathematical operations between a byte and a uint8. However, you rarely see uint8 used in Go code; just call it a byte.

The second special name is int. On a 32-bit CPU, int is a 32-bit signed integer like an int32. On most 64-bit CPUs, int is a 64-bit signed integer, just like an int64. Because int isn’t consistent from platform to platform, it is a compile-time error to assign, compare, or perform mathematical operations between an int and an int32 or int64 without a type conversion

There are two other special names for integer types, rune and uintptr.details about them later



The reason why int64 and uint64 are the idiomatic choice in this situation is that Go doesn’t have generics (yet) and doesn’t have function overloading. Without these features, you’d need to write many functions with slightly different names to implement your algorithm. Using int64 and uint64 means that you can write the code once and let your callers use type conversions to pass values in and convert data that’s returned.

You can see this pattern in the Go standard library with the functions FormatInt/FormatUint and ParseInt/ParseUint in the strconv package. There are other situations, like in the math/bits package, where the size of the integer matters. In those cases, you need to write a separate function for every integer type.

You can combine any of the arithmetic operators with = to modify a variable: +=, -=, *=, /=, and %=.

Just like the arithmetic operators, you can also combine all of the logical operators with = to modify a variable: &=, |=, ^=, &^=, <<=, and >>=.

You can use all the standard mathematical and comparison operators with floats, except %. Floating point division has a couple of interesting properties. Dividing a nonzero floating point variable by 0 returns +Inf or -Inf (positive or negative infinity), depending on the sign of the number. Dividing a floating point variable set to 0 by 0 returns NaN (Not a Number).

There isn’t a lot to the complex number support in Go. Go defines two complex number types. complex64 uses float32 values to represent the real and imaginary part, and complex128 uses float64 values. 

Strings in Go are immutable; you can reassign the value of a string variable, but you cannot change the value of the string that is assigned to it.

Go also has a type that represents a single code point. The rune type is an alias for the int32 type, just like byte is an alias for uint8. As you could probably guess, a rune literal’s default type is a rune, and a string literal’s default type is a string.

 Go doesn’t allow automatic type promotion between variables. You must use a type conversion when variable types do not match. Even different-sized integers and floats must be converted to the same type to interact. This makes it clear exactly what type you want without having to memorize any type conversion rules (see Example 2-2).
 
 `var x int = 10
var y float64 = 30.2
var z float64 = float64(x) + y
var d int = x + int(y)`

variable declaration :- 

`var x int = 10`
`var x, y int = 10, 20`


var (
    x    int
    y        = 20
    z    int = 30
    d, e     = 40, "hello"
    f, g string
)


The most common declaration style within functions is :=. Outside of a function, use declaration lists on the rare occasions when you are declaring multiple package-level variables.

You should rarely declare variables outside of functions, in what’s called the package block (see “Blocks”). Package-level variables whose values change are a bad idea. When you have a variable outside of a function, it can be difficult to track the changes made to it, which makes it hard to understand how data is flowing through your program. This can lead to subtle bugs. As a general rule, you should only declare variables in the package block that are effectively immutable.

Using const
 const in Go is very limited. Constants in Go are a way to give names to literals. They can only hold values that the compiler can figure out at compile time. This means that they can be assigned:

Numeric literals

true and false

Strings

Runes

The built-in functions complex, real, imag, len, and cap

Expressions that consist of operators and the preceding values

iota  can be used with const
here are no immutable arrays, slices, maps, or structs, and there’s no way to declare that a field in a struct is immutable. This is less limiting than it sounds. Within a function, it is clear if a variable is being modified, so immutability is less important. In “Go Is Call By Value”, we’ll see how Go prevents modifications to variables that are passed as parameters to functions.

Constants can be typed or untyped. An untyped constant works exactly like a literal; it has no type of its own, but does have a default type that is used when no other type can be inferred. A typed constant can only be directly assigned to a variable of that type.


In general, leaving a constant untyped gives you more flexibility

Another Go requirement is that every declared local variable must be read. It is a compile-time error to declare a local variable and to not read its value.

Go requires identifier names to start with a letter or underscore, and the name can contain numbers, underscores, and letters. Go’s definition of “letter” and “number” is a bit broader than many languages. Any Unicode character that is considered a letter or digit is allowed.

In many languages, constants are always written in all uppercase letters, with words separated by underscores (names like INDEX_COUNTER or NUMBER_TRIES). Go does not follow this pattern. This is because Go uses the case of the first letter in the name of a package-level declaration to determine if the item is accessible outside the package.

Within a function, favor short variable names. The smaller the scope for a variable, the shorter the name that’s used for it. It is very common in Go to see single-letter variable names. For example, the names k and v (short for key and value) are used as the variable names in a for-range loop. If you are using a standard for loop, i and j are common names for the index variable. There are other idiomatic ways to name variables of common types; we will mention them as we cover more parts of the standard library.

When naming variables and constants in the package block, use more descriptive names. The type should still be excluded from the name, but since the scope is wider, you need a more complete name to make it clear what the value represents

## Chapter 3. Composite Types
Arrays are not used directly
All of the elements in the array must be of the type that’s specified (this doesn’t mean they are always of the same type). There are a few different declaration styles. 

`var x [3]int` array declaration

`var x = [3]int{10, 20, 30}`

If you have a sparse array (an array where most elements are set to their zero value), you can specify only the indices with values in the array literal:

`var x = [12]int{1, 5: 4, 6, 10: 100, 15}`
This creates an array of 12 ints with the following values: [1, 0, 0, 0, 0, 4, 6, 0, 0, 0, 100, 15].

When using an array literal to initialize an array, you can leave off the number and use … instead:

`var x = [...]int{10, 20, 30}`
You can use == and != to compare arrays:

`var x = [...]int{1, 2, 3}`
`var y = [3]int{1, 2, 3}`
`fmt.Println(x == y)` // prints true
Go only has one-dimensional arrays, but you can simulate multidimensional arrays:

`var x [2][3]int`

Go considers the size of the array to be part of the type of the array. This makes an array that’s declared to be [3]int a different type from an array that’s declared to be [4]int. This also means that you cannot use a variable to specify the size of an array, because types must be resolved at compile time, not at runtime.

What’s more, you can’t use a type conversion to convert arrays of different sizes to identical types. Because you can’t convert arrays of different sizes into each other, you can’t write a function that works with arrays of any size and you can’t assign arrays of different sizes to the same variable.

Go arrays are not used directly but used for backing Slices

## Slices

slice declaration `var x = []int{10, 20, 30}`

we can also specify only the indices with values in the slice literal:

`var x = []int{1, 5: 4, 6, 10: 100, 15}`

You can simulate multidimensional slices and make a slice of slices:

`var x [][]int`

var x []int here , zero value of slice is nil


A slice is the first type we’ve seen that isn’t comparable. It is a compile-time error to use == to see if two slices are identical or != to see if they are different. The only thing you can compare a slice with is nil:


The reflect package contains a function called DeepEqual that can compare almost anything, including slices. It’s primarily intended for testing, but you could use it to compare slices if you needed to.


## inbuilt functions :- 
len
append
`var x []int`
`x = append(x, 10)`

used to grow slices

The append function takes at least two parameters, a slice of any type and a value of that type. It returns a slice of the same type. The returned slice is assigned back to the slice that’s passed in.


var x = []int{1, 2, 3}
x = append(x, 4)

`x = append(x, 5, 6, 7)`

`y := []int{20, 30, 40}`
`x = append(x, y...)`

slice is like arraylist that increases the array capacity by twice 

better to allocate slice using make

make
We’ve already seen two ways to declare a slice, using a slice literal or the nil zero value. While useful, neither way allows you to create an empty slice that already has a length or capacity specified. That’s the job of the built-in make function. It allows us to specify the type, length, and, optionally, the capacity. Let’s take a look:

`x := make([]int, 5)`

`x = append(x, 10)`


The 10 is placed at the end of the slice, after the zero values in positions 0–4 because append always increases the length of a slice. The value of x is now [0 0 0 0 0 10], with a length of 6 and a capacity of 10 (the capacity was doubled as soon as the sixth element was appended).

We can also specify an initial capacity with make:

`x := make([]int, 5, 10)`
This creates an int slice with a length of 5 and a capacity of 10.

