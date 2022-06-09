# rpi-infrared
 A library used for interacting with infrared remote controls in go
 
 # This repository has been transferred to the [Smarthome](https://github.com/smarthome-go/infrared) organization.

## Installation / Setup
To install the library, execute the following command
```
go get github.com/MikMuellerDev/rpiif  
```
You can then import the library in your project using following code
```go
import "github.com/MikMuellerDev/rpiif"
```

## Getting started
### Creating a new *instance*
Before codes can be scanned, create a new module struct:
```go
ifScanner := rpiif.Scanner
```
The `ifScanner` struct now allows you to use the library

### Setting up the input pin
After you have created a new struct, run the `Setup` function to tell the library on which pin in should listen to incoming infrared signals  
This can be achieved by using `Scanner.Setup(pin)`
```go
ifScanner.Setup(4)
```
Make sure to implement proper error handling.
For reference, take a look at the [Example](#example).

### Using the scanner
To scan for codes, use the following function:
```go
receivedCode, err := ifScanner.Scan()
```
The scan function will wait until a code is received, then return it.
Due to this, it is to be noted that the `Scan` function is blocking, which means you probably want to run this in a separate goroutine.
The `Scan` method returns the received code as a `hex` string.
Make sure to implement proper error handling.
For another reference, take a look at the [Example](#example).


## Example
```go
package main

import (
	"fmt"

	"github.com/MikMuellerDev/rpiif"
)

func main() {
	ifScanner := rpiif.Scanner
	if err := ifScanner.Setup(4); err != nil {
		panic(err.Error())
	}
	receivedCode, err := ifScanner.Scan()
	if err != nil {
		panic(err)
	}
	fmt.Println(receivedCode)
}
```
