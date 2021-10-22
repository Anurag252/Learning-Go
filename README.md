# Learning-Go
Go still expects there to be a single workspace for third-party Go tools installed via go install (see “Getting Third-Party Go Tools”). By default, this workspace is located in $HOME/go, with source code for these tools stored in $HOME/go/src and the compiled binaries in $HOME/go/bin. You can use this default or specify a different workspace by setting the $GOPATH environment variable.

The go run command does in fact compile your code into a binary. However, the binary is built in a temporary directory. The go run command builds the binary, executes the binary from that temporary directory, and then deletes the binary after your program finishes. This makes the go run command useful for testing out small programs or using Go like a scripting language.

`go build hello.go`
This creates an executable called hello (or hello.exe on Windows) in the current directory. Run it and you unsurprisingly see Hello, world! printed on the screen.

The name of the binary matches the name of the file or package that you passed in. If you want a different name for your application, or if you want to store it in a different location, use the -o flag. For example, if we wanted to compile our code to a binary called “hello_world,” we would use:

`go build -o hello_world hello.go`

The go install command takes an argument, which is the location of the source code repository of the project you want to install, followed by an @ and the version of the tool you want (if you just want to get the latest version, use @latest). It then downloads, compiles, and installs the tool into your $GOPATH/bin directory.

The Go development tools include a command, `go fmt`, which automatically reformats your code to match the standard format. It does things like fixing up the whitespace for indentation, lining up the fields in a struct, and making sure there is proper spacing around operators.
