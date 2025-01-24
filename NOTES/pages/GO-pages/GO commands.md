## `go mod init <module_name>`
-  Equivalent of `npm init` in Go
- `go mod init` is used to initialize a new module.
- It creates a new `go.mod` file in the current directory.
- The `go.mod` file contains information about the module, its dependencies, and the Go version.
---
## `go run <main_file.go>`
-  Equivalent of `npm run start` in Go
- `go run` is used to compile and run a Go program.
- It compiles the program and executes it.
---
## `go get <package_name>`
- Equivalent of `npm install <package_name>` in Go
- `go get` is not a package manager.
- `go get` is used to download and install packages from remote repositories.
- It does not handle versioning.
- This command fetches the package and its dependencies (if any)
---
## go.mod file
- It contains information about the module, its dependencies, and the Go version.
- Equivalent of `package.json` in Go
---
## `go mod tidy`
- Equivalent of `npm install` in Go
- `go mod tidy` is used to add missing and remove unused modules.
- It updates the go.mod file to use the latest version of the dependencies.
---
## ``