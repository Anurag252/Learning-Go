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

If you are sure you know the exact size you want, you can specify the length and index into the slice to set the values. This is often done when transforming values in one slice and storing them in a second. The downside to this approach is that if you have the size wrong, you’ll end up with either zero values at the end of the slice or a panic from trying to access elements that don’t exist.

In other situations, use make with a zero length and a specified capacity. This allows you to use append to add items to the slice. If the number of items turns out to be smaller, you won’t have an extraneous zero value at the end. If the number of items is larger, your code will not panic.

The Go community is split between the second and third approaches. I personally prefer using append with a slice initialized to a zero length. It might be slower in some situations, but it is less likely to introduce a bug.

A slice expression creates a slice from a slice. It’s written inside brackets and consists of a starting offset and an ending offset, separated by a colon (:). If you leave off the starting offset, 0 is assumed. Likewise, if you leave off the ending offset, the end of the slice is substituted.


`x := []int{1, 2, 3, 4}
y := x[:2]
z := x[1:]
d := x[1:3]
e := x[:]
fmt.Println("x:", x)
fmt.Println("y:", y)
fmt.Println("z:", z)
fmt.Println("d:", d)
fmt.Println("e:", e)`

When you take a slice from a slice, you are not making a copy of the data. Instead, you now have two variables that are sharing memory. This means that changes to an element in a slice affect all slices that share that element. Let’s see what happens when we change values.

x[a:b] --> means from a to b-1

What’s going on? Whenever you take a slice from another slice, the subslice’s capacity is set to the capacity of the original slice, minus the offset of the subslice within the original slice. This means that any unused capacity in the original slice is also shared with any subslices.

To avoid complicated slice situations, you should either never use append with a subslice or make sure that append doesn’t cause an overwrite by using a full slice expression. 

The full slice expression includes a third part, which indicates the last position in the parent slice’s capacity that’s available for the subslice. Subtract the starting offset from this number to get the subslice’s capacity. Example 3-8 shows lines three and four from the previous example, modified to use full slice expressions.



`y := x[:2:2]
z := x[2:4:4]`

Slices aren’t the only thing you can slice. If you have an array, you can take a slice from it using a slice expression. This is a useful way to bridge an array to a function that only takes slices. However, be aware that taking a slice from an array has the same memory-sharing properties as taking a slice from a slice. If you run the following code on The Go Playground:

`x := [4]int{5, 6, 7, 8}
y := x[:2]
z := x[2:]
x[0] = 10
fmt.Println("x:", x)
fmt.Println("y:", y)
fmt.Println("z:", z)`

copy
If you need to create a slice that’s independent of the original, use the built-in copy function. 

The copy function takes two parameters. The first is the destination slice and the second is the source slice. It copies as many values as it can from source to destination, limited by whichever slice is smaller, and returns the number of elements copied. The capacity of x and y doesn’t matter; it’s the length that’s important.


You could also copy from the middle of the source slice:

`x := []int{1, 2, 3, 4}
y := make([]int, 2)
copy(y, x[2:])`

The copy function allows you to copy between two slices that cover overlapping sections of an underlying slice:

x := []int{1, 2, 3, 4}
num = copy(x[:3], x[1:])
fmt.Println(x, num)

You can use copy with arrays by taking a slice of the array. You can make the array either the source or the destination of the copy.

## Strings and Runes and Bytes
Under the covers, Go uses a sequence of bytes to represent a string

These bytes don’t have to be in any particular character encoding, but several Go library functions (and the for-range loop that we discuss in the next chapter) assume that a string is composed of a sequence of UTF-8-encoded code points.

`str := "Hello world"
	fmt.Println(str[0])`
 
 this gives 72 as output
 
 `var s string = "Hello, :blush:"
var bs []byte = []byte(s)
var rs []rune = []rune(s)
fmt.Println(bs)
fmt.Println(rs)`

this outputs 
`[72 101 108 108 111 44 32 240 159 140 158]
[72 101 108 108 111 44 32 127774]`

dont convert string to int at each location , it will be changed to ascii 


_UTF-8 is the most commonly used encoding for Unicode. Unicode uses four bytes (32 bits) to represent each code point, the technical name for each character and modifier. Given this, the simplest way to represent Unicode code points is to store four bytes for each code point. This is called UTF-32. It is mostly unused because it wastes so much space. Due to Unicode implementation details, 11 of the 32 bits are always zero. Another common encoding is UTF-16, which uses one or two 16-bit (2-byte) sequences to represent each code point. This is also wasteful; much of the content in the world is written using code points that fit into a single byte. And that’s where UTF-8 comes in.

UTF-8 is very clever. It lets you use a single byte to represent the Unicode characters whose values are below 128 (which includes all of the letters, numbers, and punctuation commonly used in English), but expands to a maximum of four bytes to represent Unicode code points with larger values. The result is that the worst case for UTF-8 is the same as using UTF-32. UTF-8 has some other nice properties. Unlike UTF-32 and UTF-16, you don’t have to worry about little-endian versus big-endian. It also allows you to look at any byte in a sequence and tell if you are at the start of a UTF-8 sequence, or somewhere in the middle. That means you can’t accidentally read a character incorrectly.

The only downside is that you cannot randomly access a string encoded with UTF-8. While you can detect if you are in the middle of a character, you can’t tell how many characters in you are. You need to start at the beginning of the string and count. Go doesn’t require a string to be written in UTF-8, but it strongly encourages it. We’ll see how to work with UTF-8 strings in upcoming chapters.

Fun fact: UTF-8 was invented in 1992 by Ken Thompson and Rob Pike, two of the creators of Go.
_

Rather than use the slice and index expressions with strings, you should extract substrings and code points from strings using the functions in the strings and unicode/utf8 packages in the standard library.

## Maps
`var nilMap map[string]int` declaration --> nil map

with brackets `totalWins := map[string]int{} `

here we can read write only after assignment with brackets

initializing struct :- `teams := map[string][]string {
    "Orcas": []string{"Fred", "Ralph", "Bijou"},
    "Lions": []string{"Sarah", "Peter", "Billie"},
    "Kittens": []string{"Waldo", "Raul", "Ze"},
}`

If you know how many key-value pairs you intend to put in the map, but don’t know the exact values, you can use make to create a map with a default size:

`ages := make(map[int][]string, 10)`

### The comma ok Idiom
`m := map[string]int{
    "hello": 5,
    "world": 0,
}
v, ok := m["hello"]
fmt.Println(v, ok)`

Deleting from maps 

`m := map[string]int{
    "hello": 5,
    "world": 10,
}
delete(m, "hello")`

### Using Maps as Sets
use map of string and boolean

Some people prefer to use struct{} for the value when a map is being used to implement a set. (We’ll discuss structs in the next section.) The advantage is that an empty struct uses zero bytes, while a boolean uses one byte.

The disadvantage is that using a struct{} makes your code more clumsy. You have a less obvious assignment, and you need to use the comma ok idiom to check if a value is in the set:

`intSet := map[int]struct{}{}
vals := []int{5, 10, 2, 5, 8, 7, 3, 9, 1, 2, 10}
for =, v := range vals {
    intSet[v] = struct{}{}
}
if -, ok := intSet[5]; ok {
    fmt.Println("5 is in the set")
}`




Once a struct type is declared, we can define variables of that type:

var fred person


A struct literal can be assigned to a variable as well:

`bob := person{}`

There are two different styles for a nonempty struct literal. A struct literal can be specified as a comma-separated list of values for the fields inside of braces:

`julia := person{
    "Julia",
    40,
    "cat",
}`


When using this struct literal format, a value for every field in the struct must be specified, and the values are assigned to the fields in the order they were declared in the struct definition.

also possible :- 
`beth := person{
    age:  30,
    name: "Beth",
}`

do not mix these two ways , else error

A field in a struct is accessed with dotted notation:

`bob.name = "Bob"
fmt.Println(beth.name)`

### Anonymous Structs
used in marshaling/unmarshling and testing
`pet := struct {
    name string
    kind string
}{
    name: "Fido",
    kind: "dog",
}`

slices and maps , functions , channel feilds are non-comaparable

Whether or not a struct is comparable depends on the struct’s fields. Structs that are entirely composed of comparable types are comparable

overriding operator is not possible * check

 Go does allow you to perform a type conversion from one struct type to another if the fields of both structs have the same names, order, and types.
 
 `type secondPerson struct {
    name string
    age  int
}`

Anonymous structs add a small twist to this: if two struct variables are being compared and at least one of them has a type that’s an anonymous struct, you can compare them without a type conversion if the fields of both structs have the same names, order, and types. You can also assign between named and anonymous struct types if the fields of both structs have the same names, order, and types:


## Blocks, Shadows, and Control Structures

A shadowing variable is a variable that has the same name as a variable in a containing block. For as long as the shadowing variable exists, you cannot access a shadowed variable

a locaal variable will shadow global variable
also there will be no error
`func main() {
    x := 10
    fmt.Println(x)
    fmt := "oops"
    fmt.Println(fmt)
}`

here fmt is shadowed , even though its import statement

to detect shadow variable use shadow linter from golang

go has only 25 keywords , others come from universe block 
int, string , true, false etc come from universe blick 
its possible to shadow them as well , 

`fmt.Println(true)
true := 10
fmt.Println(true)`

prints 10
shadow linter does not detect , universal block shadows

in If dont put paranthesis

special syntax to declaare and do an if
`if n := rand.Intn(10); n == 0 {
    fmt.Println("That's too low")
} else if n > 5 {
    fmt.Println("That's too big:", n)
} else {
    fmt.Println("That's a good number:", n)
}`

here n is defined and it is accesible everywhere inside an if block

Technically, you can put any simple statement before the comparison in an if statement. This includes things like a function call that doesn’t return a value or assigning a new value to an existing variable. 


## for, Four Ways

- A complete, C-style for
`for i := 0; i < 10; i++ {
    fmt.Println(i)
}`
 no parenthesis around the parts of the for
 you must use := to initialize the variables; 
 Second, just like variable declarations in if statements, you can shadow a variable here.
 
- A condition-only for

`i := 1
for i < 100 {
        fmt.Println(i)
        i = i * 2
}`

- An infinite for

`func main() {
    for {
        fmt.Println("Hello")
    }`
    
    

- for-range

You can only use a for-range loop to iterate over the built-in compound types and user-defined types that are based on them.

`evenVals := []int{2, 4, 6, 8, 10, 12}
for i, v := range evenVals {
    fmt.Println(i, v)
}`

`evenVals := []int{2, 4, 6, 8, 10, 12}
for _, v := range evenVals {
    fmt.Println(v)
}`

here its index and value and for maps it would be key and values

order of k/v pair is random to avoid hashDOS attack , except There is one exception to this rule. To make it easier to debug and log maps, the formatting functions (like fmt.Println) always output maps with their keys in ascending sorted order.

for-range on strings iterate over runes and not bytes

The for-range value is a copy
You should be aware that each time the for-range loop iterates over your compound type, it copies the value from the compound type to the value variable. Modifying the value variable will not modify the value in the compound type.

As is the case with if statements, you don’t put parenthesis around the value being compared in a switch.
Also like an if statement, you can declare a variable that’s scoped to all of the branches of the switch statement. In our case, we are scoping the variable word to all of the cases in the switch statement.
All of the case clauses (and the optional default clause) are contained inside a set of braces. But you should note that you don’t put braces around the contents of the case clauses. You can have multiple lines inside a case (or default) clause and they are all considered to be part of the same block.

By default, cases in switch statements in Go don’t fall through. This is more in line with the behavior in Ruby or (if you are an old-school programmer) Pascal.

This prompts the question: if cases don’t fall through, what do you do if there are multiple values that should trigger the exact same logic? In Go, you separate multiple matches with commas, like we do when matching 1, 2, 3, and 4 or 6, 7, 8, and 9. That’s why we get the same output for both a and cow.

For the sake of completeness, Go does include a fallthrough keyword, which lets one case continue on to the next one. Please think twice before implementing an algorithm that uses it. If you find yourself needing to use fallthrough, try to restructure your logic to remove the dependencies between cases.


to use break inside a for nested in switch use lable , like this break loop

a blank switch uses a boolean match , all trues are executed

## Chapter 5. Functions
main functions don’t take in any parameters or return any values

`func div(numerator int, denominator int) int {
    if denominator == 0 {
        return 0
    }
    return numerator / denominator
}`

Go doesn’t have: named and optional input parameters.

define a struct that has fields that match the desired parameters, and pass the struct to your function.

If you want to emulate named and optional parameters, define a struct that has fields that match the desired parameters, and pass the struct to your function

`type MyFuncOpts struct {
    FirstName string
    LastName string
    Age int
}

func MyFunc(opts MyFuncOpts) error {
    // do something here
}

func main() {
    MyFunc(MyFuncOpts {
        LastName: "Patel",
        Age: 50,
    })
    My Func(MyFuncOpts {
        FirstName: "Joe",
        LastName: "Smith",
    })
}`

The variadic parameter must be the last (or only) parameter in the input parameter list. You indicate it with three dots (…) before the type. The variable that’s created within the function is a slice of the specified type

`func addTo(base int, vals ...int) []int {
    out := make([]int, 0, len(vals))
    for _, v := range vals {
        out = append(out, base+v)
    }
    return out
}`

while passing params , if calling by passing slice we need to put three dots as well 
fmt.Println(addTo(3, []int{1, 2, 3, 4, 5}...))

## Multiple Return Values

`func divAndRemainder(numerator int, denominator int) (int, int, error) {
    if denominator == 0 {
        return 0, 0, errors.New("cannot divide by zero")
    }
    return numerator / denominator, numerator % denominator, nil
}`

if a function returns multiple values, you must return all of them, separated by commas. Don’t put parentheses around the returned values; that’s a compile-time error.

`result, remainder, err := divAndRemainder(5, 2)`

You must assign each value returned from a function. If you try to assign multiple return values to one variable, you get a compile-time error.

## Named Return Values

`func divAndRemainder(numerator int, denominator int) (result int, remainder int,
                                                                  err error) {
    if denominator == 0 {
        err = errors.New("cannot divide by zero")
        return result, remainder, err
    }
    result, remainder = numerator/denominator, numerator%denominator
    return result, remainder, err
}`

 the name that’s used for a named returned value is local to the function;
 
 no need to explicitly return the named variables
 
 Naked Return -> using blank return , this will return the last assigned values to named arguements //dont use these
 
 Functions are values and hence they can be passed around and stored as values in dictionary
 
 ## Function Type Declarations
 
 `type opFuncType func(int,int) int`
 
 we can define a type and use it to pass around or store in dictionary
 
 ## Anonymous Functions
 
 `func(j int) {
            fmt.Println("printing", j, "from inside of an anonymous function")
        }(i)`
	
	
	
## closure

Functions declared inside of functions are special; they are closures. 

One thing that closures allow you to do is limit a function’s scope. If a function is only going to be called from one other function, but it’s called multiple times, you can use an inner function to “hide” the called function. This reduces the number of declarations at the package level, which can make it easier to find an unused name.

## Returning Functions from Functions
Not only can you use a closure to pass some function state to another function, you can also return a closure from a function. 


## defer
defer statement is delayed till surrounding function is exited

`func DoSomeInserts(ctx context.Context, db *sql.DB, value1, value2 string)
                  (err error) {
    tx, err := db.BeginTx(ctx, nil)
    if err != nil {
        return err
    }
    defer func() {
        if err == nil {
            err = tx.Commit()
        }
        if err != nil {
            tx.Rollback()
        }
    }()
    _, err = tx.ExecContext(ctx, "INSERT INTO FOO (val) values $1", value1)
    if err != nil {
        return err
    }
    // use tx to do more database inserts here
    return nil
}`

Go always makes a copy of the value of the variable.

call by value is for not only for primitive type also for structs etc

only maps and slices are implemented with pointers , hence they will change in function

maps and slices are also values . Every type in Go is a value type. It’s just that sometimes the value is a pointer.

alternate to pass by value we can pass by pointers (which is again pass by value but valuea re pointers )

## Chapter 6. Pointers
The zero value for a pointer is nil.
`var x int32 = 10
var y bool = true
pointerX := &x
pointerY := &y
var pointerZ *string`

slices 
maps
functions
channels
interfaces 

all are implemeneted by using pointers

pointer arithmatic not allowed in golang

The & is the address operator. It precedes a value type and returns the address of the memory location where the value is stored:

`x := "hello"
pointerToX := &x`

The * is the indirection operator. It precedes a variable of pointer type and returns the pointed-to value. This is called dereferencing:

Before dereferencing a pointer, you must make sure that the pointer is non-nil. Your program will panic if you attempt to dereference a nil pointer:

The built-in function new creates a pointer variable. It returns a pointer to a zero value instance of the provided type:

`var x = new(int)
fmt.Println(x == nil) // prints false
fmt.Println(*x)       // prints 0`

 For structs, use an & before a struct literal to create a pointer instance. You can’t use an & before a primitive literal (numbers, booleans, and strings) or a constant because they don’t have memory addresses; they exist only at compile time. When you need a pointer to a primitive type, declare a variable and point to it:
 
 `x := &Foo{}
var y string
z := &y`


The built-in function new creates a pointer variable. It returns a pointer to a zero value instance of the provided type:
var x = new(int)
fmt.Println(x == nil) // prints false
fmt.Println(*x)       // prints 0

The new function is rarely used. For structs, use an & before a struct literal to create a pointer instance. You can’t use an & before a primitive literal (numbers, booleans, and strings) or a constant because they don’t have memory addresses; they exist only at compile time
When you need a pointer to a primitive type, declare a variable and point to it:


 three points about OOP language ( java , js , ruby )
If you pass an instance of a class to a function and you change the value of a field, the change is reflected in the variable that was passed in.

If you reassign the parameter, the change is not reflected in the variable that was passed in.

If you pass nil/null/None for a parameter value, setting the parameter itself to a new value doesn’t modify the variable in the calling function.

What we are seeing is that every instance of a class in these languages is implemented as a pointer. When a class instance is passed to a function or method, the value being copied is the pointer to the instance. 

When you use a pointer variable or parameter in Go, you see the exact same behaviors. The difference between Go and these languages is that Go gives you the choice to use pointers or values for both primitives and structs. 

passing byy value makes code easy to read and less work for GC

## pointers indicate mutable parameters
Go constants provide names for literal expressions that can be calculated at compile time. There is no mechanism in the language to declare that other kinds of values are immutable.

immutability type is better in terms of bugs free code , but golang's pass by value nature is gurantees immutability 

## Chapter 7. Types, Methods, and Interfaces
In addition to struct literals, you can use any primitive type or compound type literal to define a concrete type. Here are a few examples:

`type Score int
type Converter func(string)Score
type TeamScores map[string]Score`

Go allows you to declare a type at any block level, from the package block down. However, you can only access the type from within its scope.

Just like functions, method names cannot be overloaded. You can use the same method names for different types, but you can’t use the same method name for two different methods on the same type

be aware that methods must be declared in the same package as their associated type; Go doesn’t allow you to add methods to types you don’t control. While you can define a method in a different file within the same package as the type declaration, it is best to keep your type definition and its associated methods together so that it’s easy to follow the implementation.



If your method modifies the receiver, you must use a pointer receiver.

If your method needs to handle nil instances (see “Code Your Methods for nil Instances”), then it must use a pointer receiver.

If your method doesn’t modify the receiver, you can use a value receiver.

in case a method was defined on pointer recieever , calling on value also calls the same method


do not write getter and setter methods for Go structs, unless you need them to meet an interface (we’ll start covering interfaces in “A Quick Lesson on Interfaces”). Go encourages you to directly access a field. Reserve methods for business logic.


handle nil recievers , value types will panic , reference types will work but check null rference


we can convert a method to function

f1 := myAdder.AddTo
fmt.Println(f2(myAdder, 15))


method vs function
Any time your logic depends on values that are configured at startup or changed while your program is running, those values should be stored in a struct and that logic should be implemented as a method. If your logic only depends on the input parameters, then it should be a function.




In the case of a method expression, the first parameter is the receiver for the method; our function signature is func(Adder, int) int.


Declaring a type based on another type

For user-defined types whose underlying types are built-in types, a user-declared type can be used with the operators for those types. As we see in the preceding code, they can also be assigned literals and constants compatible with the underlying type.

iota 👎
const (
    Uncategorized MailCategory = iota
    Personal
    Spam
    Social
    Advertisements
)
here Uncategorized is 0 

Dont use Iota as anyone entering a value at any line can break logic 

better use explicitly typed constants 

`type BitField int

const (
    Field1 BitField = 1 << iota // assigned 1
    Field2                      // assigned 2
    Field3                      // assigned 4
    Field4                      // assigned 8
)`

this type of code is also possible


## “Favor object composition over class inheritance”

``type Employee struct {
    Name         string
    ID           string
}

func (e Employee) Description() string {
    return fmt.Sprintf("%s (%s)", e.Name, e.ID)
}

type Manager struct {
    Employee
    Reports []Employee
}

func (m Manager) FindNewEmployees() []Employee {
    // do business logic
}
``

here Employee is assigned without any name assignment , this makes this as an embedded feild

If the containing struct has fields or methods with the same name as an embedded field, you need to use the embedded field’s type to refer to the obscured fields or methods. If you have types defined like this:

`type Inner struct {
    X int
}

type Outer struct {
    Inner
    X int
}`

You can only access the X on Inner by specifying Inner explicitly:

`o := Outer{
    Inner: Inner{
        X: 10,
    },
    X: 20,
}
fmt.Println(o.X)       // prints 20
fmt.Println(o.Inner.X) // prints 10`


When we embed a type, the methods of that type become methods of the outer type, but when they are invoked the receiver of the method is the inner type, not the outer one. 

Duck typing in Golang

You’ll often hear experienced Go developers say that your code should “Accept interfaces, return structs.”

If you create an API that returns interfaces, you are losing one of the main advantages of implicit interfaces: decoupling. You want to limit the third-party interfaces that your client code depends on because your code is now permanently dependent on the module that contains those interfaces, as well as any dependencies of that module, and so on.

function types can also act as recievers

func can also implement interface


`type LoggerAdapter func(message string)

func (lg LoggerAdapter) Log(message string) {
    lg(message)
}

type Logger interface {
    Log(message string)
}
`




## Errors

Go handles errors by returning a value of type error as the last return value for a function. This is entirely by convention, but it is such a strong convention that it should never be breached. When a function executes as expected, nil is returned for the error parameter. If something goes wrong, an error value is returned instead. The calling function then checks the error return value by comparing it to nil, handling the error, or returning an error of its own

`func calcRemainderAndMod(numerator, denominator int) (int, int, error) {
    if denominator == 0 {
        return 0, 0, errors.New("denominator is 0")
    }
    return numerator / denominator, numerator % denominator, nil
}`

this should be like this only

A new error is created from a string by calling the New function in the errors package. Error messages should not be capitalized nor should they end with punctuation or a newline. In most cases, you should set the other return values to their zero values when a non-nil error is returned. We’ll see an exception to this rule when we look at sentinel errors.

`type error interface {
    Error() string
}`



exceptions are not returned but errors in golang and in golang either read a value or use _ and ignore it

2 ways to declare errorr:-
1.error.New
2.The second way is to use the fmt.Errorf function. This function allows you to use all of the formatting verbs for fmt.Printf to create an error. Like errors.New, this string is returned when you call the Error method on the returned error instance:

