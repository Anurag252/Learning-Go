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




