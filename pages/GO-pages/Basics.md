#### Let's start code
Get started with Hello, World.

1. Go to the desire directory & create a new directory as `hello` & open in VS code
```bash

mkdir hello

cd hello

code .

```

2. Enable dependency tracking for your code
	When your code imports packages contained in other modules, you manage those dependencies through your code's own module. That module is defined by a go.mod file that tracks the modules that provide those packages. That go.mod file stays with your code, including in your source code repository.

	In actual development, the module path will typically be the repository location where your source code will be kept. For example, the module path might be `github.com/mymodule`. If you plan to publish your module for others to use, the module path *must* be a location from which Go tools can download your module.

	For the purposes of practice, just use `example/hello`.

```bash

go mod init practice/hello

```

3. Now create a new GO file, `hello.go`

4. Write a simple `hello world!` code  

```go

package main
import "fmt"


func main() {
	fmt.Println("Hello, World!")
}

```

5. Explanation
- `package main`: Every Go program is part of a package. The `main` package is where the Go runtime looks for the entry point of the program.

- `import "fmt"`: This line imports the `fmt` package, which provides formatting functions like `Println`.

- `func main()`: The `main` function is the entry point of the program, where execution starts.

- `fmt.Println`: This function prints the message to the console.


6. Run Your Code
```bash

go run hello.go

```

### Taking Input

```go

package main

import "fmt"

func main() {

	var name string //variable
	fmt.Println("What is your name?")

	fmt.Print("> ")

	fmt.Scan(&name) //taking input from user

	fmt.Println(">> Greetings, "+name)
}

```

  ---
## Declare Variables

#### 1. **With `var` keyword:**

**syntax**
```go

var *variable1 type = value //with type

var variable2 = value //with out type*

```

**📑 Note**

1. can declare without assigning value.
2. after assigning a value(suppose string), can’t re-assign with a different datatype value(int or float32 or bool).
3. after assigning a value(suppose string), can re-assign with the same datatype value(string).
4. `var` can be used inside a function or outside of a function, in other words as a local variable or global variable

#### 2. **with `:=` sign:**

**syntax**
```go

variablename := value

```

**📑 Note**
1. can’t declare without assigning value.
2. after assigning a value(suppose string), can’t re-assign with a different datatype value(int or float32 or bool).
3. after assigning a value(suppose string), can re-assign with the same datatype value(string).
4. `:=` can be used inside a function only, in other words as a local variable.

#### 3. **with `const` keyword:**
**syntax**

```go

const variable1 type = value //with type

const variable2 = value //with out type

```

**📑 Note**
1. can’t declare without assigning value.
2. after assigning a value(suppose string), can’t re-assign with a different datatype value(int or float32 or bool).
3. after assigning a value(suppose string), can’t re-assign with the same datatype value(string).
4. `const` can be used inside a function or outside of a function, in other words as a local variable or global variable

---
## Data Types

#### 1. **numeric**
a. **Integer** - this data types are used to store a whole number without decimals, like 10, -110, or 1503450. The integer data type has two categories:

- **Signed integers** - can store both positive and negative values

```go

var x int = 500

var y int = -4500

```

Go has five keywords/types of signed integers -

| type    | size                      | range                                                                                       |
| ------- | ------------------------- | ------------------------------------------------------------------------------------------- |
| `int`   | can be 32 bits or 64 bits | 2147483648 to 2147483647 in 32 bit OR -9223372036854775808 to 9223372036854775807 in 64 bit |
| `int8`  | 8 bits or 1 byte          | -128 to 127                                                                                 |
| `int16` | 16 bits or 4 byte         | -32768 to 32767                                                                             |
| `int32` | 32 bits or 4 byte         | -2147483648 to 2147483647                                                                   |
| `int64` | 64 bits or 8 byte         | -9223372036854775808 to 9223372036854775807                                                 |

- **Unsigned integers** - can only store non-negative values

```go

var x uint = 500

var y uint = 4500

```

Go has five keywords/types of signed integers -

| type     | size                      | range                                                            |
| -------- | ------------------------- | ---------------------------------------------------------------- |
| `uint`   | can be 32 bits or 64 bits | 0 to 4294967295 in 32 bit OR 0 to 18446744073709551615 in 64 bit |
| `uint8`  | 8 bits or 1 byte          | 0 to 255                                                         |
| `uint16` | 16 bits or 4 byte         | 0 to 65535                                                       |
| `uint32` | 32 bits or 4 byte         | 0 to 4294967295                                                  |
| `uint64` | 64 bits or 8 byte         | 0 to 18446744073709551615                                        |

#### 2. **float -** this data types are used to store positive and negative numbers with a decimal point, like 10.10, -2.53, or 4397.34587.

Go float data type has two keywords -

| type | size | range |
| --------- | ----------------- | ----------------------- |
| `float32` | 32 bits or 4 byte | -3.4e+38 to 3.4e+38. |
| `float64` | 64 bits or 8 byte | -1.7e+308 to +1.7e+308. |

#### 3. **string**
The `string` data type is used to store a sequence of characters (text). String values must be surrounded by double quotes.

```go

var txt1 string = "Hello World"

```

#### 4. **boolean**
A boolean data type is declared with the `bool` keyword and can only take the values `true` or `false`. The default value of a boolean data type is `false`.

```go

var bool1 bool = true

var bool2 bool

```

---

## Operations

### Arithmetic operation

| Operator | Name | Description | example |
| -------- | -------------- | -------------------------------- | ------- |
| + | Addition | adds values together | x + y |
| - | Substraction | Subtracts one value from another | x - y |
| \* | Multiplication | Multiplies two values | x \* y |
| / | Division | divides one value by another | x / y |
| % | Modulus | return the divison remainder | x % y |

### **Comparison Operators**

| Operator | Name | example |
| -------- | ------------------ | ------- |
| == | Equal tp | x == y |
| ! = | not equal | x ! = y |
| > | greater than | x > y |
| < | less than | x < y |
| > = | greater than euqal | x > = y |
| < = | less than equal | x < = y |  

### Logical operator

  
| Operator | Name | Description | example |
| -------- | ----------- | ---------------------------------------------------------- | ------------------- |
| && | Logical AND | returns true if both statement are true | x < 11 && x < 20 |
| |  Logical OR | returns true if one of the statements is true |
| ! | Logical NOT | reverse the result, returns true if false or false if true | !(x < 11 && x < 20) |

  
### Bitwise operators

| Operator | Name | Description | example |
| -------- | -------------------- | --- | ------- |
| & | AND | Sets each bit to 1 if both bits are 1 | x & y |
| | OR | Sets each bit to 1 if one of two bits is 1 |
| ^ | XOR | Sets each bit to 1 if only one of two bits is 1 | x ^ y |
| << | Zero fill left shift | Shift left by pushing zeros in from the right | x << 3 |
| >> | zero fll right shift | Shift right by pushing copies of the leftmost bit in from the left, and let the rightmost bits fall off | x >> 4 |

```
📌 NOTE : for any missing operator check the code, can't use OR(|) operator because markdown table consider it as a row end

```

---

## Condition Statement

Conditional statements are used to perform different actions based on different conditions.
A condition can be either `true` or `false`.
Go supports the usual comparison operators from mathematics:

- Less than `<`

- Less than or equal `<=`

- Greater than `>`

- Greater than or equal `>=`

- Equal to `==`

- Not equal to `!=`


Additionally, Go supports the usual logical operators:

- Logical AND `&&`

- Logical OR `||`

- Logical NOT `!`

You can use these operators or their combinations to create conditions for different decisions.

#### Go has the following conditional statements:

- Use `if` to specify a block of code to be executed, if a specified condition is true
- Use `else` to specify a block of code to be executed, if the same condition is false
- Use `else if` to specify a new condition to test, if the first condition is false

```go

var age int;

fmt.Printf("What's your age? \n>")
fmt.Scan(&age)

if(age == 18) {
	fmt.Println(">> You are ready to get your Driver License")
} else if(age > 18) {
	fmt.Println(">> You are eligible for a Driver License")
} else {
	fmt.Println(">> Too young to Drive!! Come back when you are 18 years old")
}

```


- Use `switch` to specify many alternative blocks of code to be executed  

	- Single Case switch
```go

var day int;
fmt.Printf("Give Day Number(1 to 7)? \n>")
fmt.Scan(&day)

switch day {

	case 1:
		fmt.Println(">> Sunday")

	case 2:
		fmt.Println(">> Monday")

	case 3:
		fmt.Println(">> Tuesday")

	case 4:
		fmt.Println(">> Wednesday")

	case 5:
		fmt.Println(">> Thursday")

	case 6:
		fmt.Println(">> Friday")

	case 7:
		fmt.Println(">> Saturday")

	default:
		fmt.Println(">> Not a day!!!!")

}

```
  

- Multi Case switch
```go

var day int;
fmt.Printf("Give Day Number(1 to 7)? \n>")
fmt.Scan(&day)

switch day {

	case 2,3,4,5,6:
		fmt.Println(">> Week Day -> means work day")

	case 1,7:
		fmt.Println(">> Weekend -> means enjoy day")

	default:
		fmt.Println(">> Not a day!!!!")
}

```


## Loop

The `for` loop is the only loop available in Go.
The `for` loop loops through a block of code a specified number of times.
### For loop

```go

for i := 0; i < 10; i++ { // for initilise; loop condition; update statement
	fmt.Println(i)
}

```

#### Nested for loop

```go

for i := 1; i <= 5; i++ {
	for j := 1; j <= i; j++ {
		fmt.Printf("*")
}
	fmt.Println()
}

```

#### Range

The `range` keyword is used to more easily iterate through the elements of an array, slice or map. It returns both the index and the value.

```go

colors := [5]string{"white", "black", "red", "green", "blue"}; //array of string

for idx, val := range colors {

	fmt.Println(idx, "->", val)

}

```

  
---
##  Functions

A function is a block of statements that can be used repeatedly in a program.
### Naming Rules for Function

- A function name must start with a letter
- A function name can only contain alpha-numeric characters and underscores (`A-z`, `0-9`, and `_` )
- Function names are case-sensitive. A function starts with a small letter means it’s a Private function and starts with a capital letter, which means it’s a Public function.
- A function name cannot contain spaces
- If the function name consists of multiple words, techniques introduced for multi-word variable naming can be used

### Create a Function

- Use the `func` keyword.
- Specify a name for the function, followed by parentheses ().
- Finally, add code that defines what the function should do, inside curly braces {}.

```go

func FunctionName() {

// code block

}

```

### Call a Function

```go

package main

import ("fmt")

func hello() {
	fmt.Println("Greetings & Hello World! to you")
}

func main() {
	hello() //call the function, also we can call it as many time we want.
}

```

### **Parameters and Arguments**

Information can be passed to functions as a parameter. Parameters act as variables inside the function

```go

func FunctionName(param1 type, param2 type, param3 type) {
// code block
}

```
example

```go

package main

import ("fmt")

func hello(name string) {
	fmt.Println("Greetings & Hello World! to ", name)
}

func main() {
	hello(Arghya) //call the function, also we can call it as many time we want.
}

```

### **Return Values**
If you want the function to return a value, you need to define the data type of the return value (such as `int`, `string`, etc), and also use the `return` keyword inside the function.

```go

func FunctionName(param1 type, param2 type) type {

// code to be executed

return output

}

```
example

```go

package main

import ("fmt")

func add(x int, y int) int {
	return x + y
}

  

func main() {
	fmt.Println(add(1, 2))
}

```

### **Named Return Values**

```go

// Here, we name the return value as result (of type int), and return the value with a naked return (means that we use the return statement without specifying the variable name)

package main

import ("fmt")

func add(x int, y int) (result int) {
	result = x + y
	return
}

func main() {
	fmt.Println(add(1, 2))
}

```

### **Multiple Named Return Values**

```go

package main

import ("fmt")

func isEven(a int) (result int, evenOdd string) {

	result = a%2
	if (result == 0) {
		evenOdd = "it's even"
		return
	} else {
	evenOdd = "it's odd"
	return
	}
}

func main() {

	a := 117
	val, ans := isEven(a)
	fmt.Println(a,"% 2 =", val )
	fmt.Println(a,">", ans )
}

```

---
## Array

Arrays are used to store multiple values of the same type in a single variable, instead of declaring separate variables for each value.
#### Declare an Array

1. **with length**
```go

var arrayName = [length]datatype{values}

  

//example

var arr1 = [5]int{1,11,111,1111,11111}

```


2. **without length**
```go

var arrayName = [...]datatype{values}

  

//example

var arr2 = [...]int{1,11,111,1111}

```

#### Initialize

in go when we initialize any array, at first it contain 0 values only.
1. **Not initialize**
```go

arr3 := [5]int{} // output -> [0,0,0,0,0]

```

2. **Partially initialize**
```go

arr4 := [5]int{1,2} //output -> [1,2,0,0,0]

```

3. **Fully initialize**
```go

arr5 := [5]int{1,2,3,4,5} //output -> [1,2,3,4,5]

```

4. **Initialize specific element**
```go

arr6 := [5]int{1:10,3:55} //output -> [0,10,0,55,0]

```

#### Access & change

once an array is declared with a length we can’t change the length, but we can access & change the values of an array

```go

arr6[0] = 111 //output -> [111,10,0,55,0]

```

  ---
## Slice

Slices are similar to arrays, but are more powerful and flexible. Like arrays, slices are also used to store multiple values of the same type in a single variable. However, unlike arrays, the length of a slice can grow and shrink as you see fit.

  #### Declare an Array
1. **Common Declearation**
```go

var sliceName = []datatype{values}

//example
var sli1 = []int{1,11,111,1111,11111}

```

2. **Create a slice with an array**
```go

var arrayName = [length]datatype{values}

var sliceName = myarray[start:end]


//example

var arr1 = [6]int{10,20,30,40,50,60}

var sli2 = arr1[3:6]

```

3. **Create a slice make() function**
```go

var sliceName = make([]type, length, capacity)

  

//example

var sli3 = make([]int, 5,10)

```

#### Append

You can append elements to the end of a slice using the `append()`function

1. **Append Elements**
```go

sliceName = append(slice_name, element1, element2, ...)  

//example
var sli4 = []int{2,4,6,8}

sli4 = append(sli4, 10, 20) // [2,4,6,8,10,20]

```

2. **Append another slice**

```go

sliceName = append(sliceName, slice1...)

//example
sli4 = append(sli4, sli1...) //output -> [2 4 6 8 10 20 1 11 121 1221 11211]

```

#### Access & change
it will be the same technique as array.

---  
## Struct

A struct (short for structure) is used to create a collection of members of different data types, into a single variable. In other words, it’s a replication of `class` in GO lang.

While arrays are used to store multiple values of the same data type into a single variable, structs are used to store multiple values of different data types into a single variable.

#### Declare a struct
```go

type struct_name struct {
	member1 datatype;
	member2 datatype;
	member3 datatype;
	...
}

  
//example -

type Person struct {
	name string
	age int
	job string
	salary int
}

```

  #### Access members

To access any member of a structure, use the dot operator (.) between the structure variable name and the structure member
```go

package main

import "fmt"

//decleare a Struct

type Job struct {
	role string
	salary int
	experience int
	location string
}

  

func main() {
	var job1 Job
//job1 specification
	job1.role = "backend developer"
	job1.salary = 1200000
	job1.experience = 1
	job1.location = "remote"

//access the elements
	fmt.Println("role >> ", jobs.role)
	fmt.Println("salary >> ", jobs.salary)
	fmt.Println("experience >> ", jobs.experience)
	fmt.Println("location >> ", jobs.location)

}

```

#### **Pass Struct as Function Arguments**

```go

package main

import "fmt"

//decleare a Struct
type Job struct {
	role string
	salary int
	experience int
	location string
}

  

func main() {
	var job1 Job

	//job1 specification
	job1.role = "backend developer"
	job1.salary = 1200000
	job1.experience = 1
	job1.location = "remote"

	//pass struct to a function
	printJobDetails(job1)
}

func printJobDetails(jobs Job) {
	//access the elements
	fmt.Println("role >> ", jobs.role)
	fmt.Println("salary >> ", jobs.salary)
	fmt.Println("experience >> ", jobs.experience)
	fmt.Println("location >> ", jobs.location)
}

```

#### **Method of struct**
```go

package main
import "fmt"


//decleare a Struct
type Job struct {
	role string
	salary int
	experience int
	location string
}

  

func main() {
	var job1 Job

  
	//job1 specification
	job1.role = "backend developer"
	job1.salary = 1200000
	job1.experience = 1
	job1.location = "remote"

	//method of a struct
	job1.printJobDetails()

}

  

//method of a struct

func (j Job) printJobDetails() {

	fmt.Println("role >> ", j.role)
	fmt.Println("salary >> ", j.salary)
	fmt.Println("experience >> ", j.experience)
	fmt.Println("location >> ", j.location)

}

```


---
## Maps

Maps are used to store data values in `key:value` pairs.

A map is an unordered and changeable collection that does not allow duplicates. The default value of a map is nil.

Maps hold references to an underlying hash table.

#### Create a Map

1. **Using var and :=**
```go

var a = map[KeyType]ValueType{key1:value1, key2:value2,...}

b := map[KeyType]ValueType{key1:value1, key2:value2,...}

  

//example

var a = map[string]string{"brand": "Ford", "model": "Mustang", "year": "1964"}

b := map[string]float64{"Arghya": 8.95, "Aritra": 8.88, "Thomas": 4.55, "Miraj": 3.25}

```

2. **Using make()Function**
```go

var a = make(map[KeyType]ValueType)

b := make(map[KeyType]ValueType)

  

//example

var a = make(map[string]string) // The map is empty now

a["brand"] = "Ford"

a["model"] = "Mustang"

a["year"] = "1964"

```

#### Allowed Key Types

The map key can be of any data type for which the equality operator (`==`) is defined. These include:
- Booleans
- Numbers
- Strings
- Arrays
- Pointers
- Structs
- Interfaces (as long as the dynamic type supports equality)

Invalid key types are:
- Slices
- Maps
- Functions

These types are invalid because the equality operator (`==`) is not defined for them.

  

#### Allowed Value Types
The map values can be **any** type.

#### **Update and Add Map Elements**
```go

package main

import ("fmt")

  

func main() {
	var a = make(map[string]string)
	a["brand"] = "Ford"
	a["model"] = "Mustang"
	a["year"] = "1964"

  
	fmt.Println(a)

	a["year"] = "1970" // Updating an element
	a["color"] = "red" // Adding an element

  	fmt.Println(a)
}

```

#### **Remove Element from Map**

```go

package main

import ("fmt")

  

func main() {
	var a = make(map[string]string)
	a["brand"] = "Ford"
	a["model"] = "Mustang"
	a["year"] = "1964"
  
	fmt.Println(a)
  
	delete(a,"year")

	fmt.Println(a)

}

```

  ---
##  comma error syntax

In GO we don’t have any `try-catch` block to handle errors instead, we have comma error syntax to handle errors in code

```go

// this help to get the answer as well as err
ans, err = function()

  
//example
fmt.Println("enter your text >")
reader := bufio.NewReader(os.Stdin)
input, err := reader.ReadString('\n')
fmt.Println(">>",input)

```

But in GO, if we don’t use any variables it throughs error, So most likely the upper code will through us an error because we are not using `err` anywhere

But we can simply avoid `err` variable by putting a `_` . This same method can be used in place of `input` if we don’t need them.

```go

fmt.Println("enter your text >")
reader := bufio.NewReader(os.Stdin)
input, _ := reader.ReadString('\n')
fmt.Println(">>",input)

```

  ---
##  Pointers

Pointers are references to a memory address.

when we are passing a variable we are actually passing a copy of that variable not the actual variable. so if we want to make some change to that variable we can’t see a change.

let’s understand with an example

```go

package main
import "fmt"

  

func main() {
	var x int = 10
	fmt.Println(x) // output -> 10
	changeTheValue(x) // output -> 20
	fmt.Println(x) // output -> 10
}

func changeTheValue(x int) {
	x = 20
	fmt.Println(x)
}

```

as we can see the value of `x` is not changing, that mean `x` inside the `chamgeTheValue` function is an reference of the actual value.

Now if we want to change the actual value we need to use the pointer  

```go

package main
import "fmt"

  

func main() {
	var x int = 10
	var ptr = &x //ptr is address reference of x
	fmt.Println(ptr) // it's shows the memory address of x
	fmt.Println(*ptr) // it's shows the the value in the memory address -> 10
	fmt.Println("------------------")

  
	fmt.Println(x) // output -> 10
	changeTheValue(ptr) // output -> 20
	fmt.Println(x) // output -> 20
}


func changeTheValue(ptr *int) {
	*ptr = 20 // change the actual value of x
	fmt.Println(*ptr)
}

```

  
### Key things to remember

1. **Declare a pointer:** `var ptr *int`, means we are declaring a pointer to store only int type of data. in place of int we can put String, float, boolean etc.

2. **Accessing the memory address:** just simply use the `ptr` to show the memory address,

NOTE - if we don’t put a value in memory, and try to access the memory it only shows us nil or null

3. **Assign or Access the value in Pointer:** `*ptr` is used to access or update or assign the value on that memory address.

4. **Reference to already available value:** `ptr := &x` is the way to access the memory address of a available value.