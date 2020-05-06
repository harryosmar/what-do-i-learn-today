# Go Tips

## Routines

- The **main function** is a go routine
  ```go
    import (
	    "fmt"
    )
    
    func main() {
	    fmt.Printf("I'm also a go routine")
    }
  ```
  The main function indeed runs in its own go routine! Even more important to know is that once the main function returns, it **closes all other go routines** that are currently running. 
- each go routine is a **thread**
- go routines communicate with each other using the **channel**
- channel blocking :
  - sender : once go routine sends on a channel then the go routine will be blocked/waiting **until another go routine receive** what sent to the channel
  - receiver : if the **channel is empty** the receiver go routine will be blocked/waiting
  - Unbuffered Channels : 1 slot. Default .
    ```go
      myChan := make(chan string)
    ```
  - Buffered Channels : define number of slots available for the channel. It's usefull when the sender sends to channel more faster the receiver.
    ```go
      // asumption the receiver slower 3 times than sender
      myChan := make(chan string, 3)
    ```


## pointer

- Methods and pointer indirection
	-  Methods with **pointer receivers** take either a value or a pointer as the receiver when they are called
		```go
			type Vertex struct {
				X, Y float64
			}
			
			func (v *Vertex) Abs() float64 {
				return math.Sqrt(v.X*v.X + v.Y*v.Y)
			}
			
			var v Vertex
		```
		`v.Abs()` is interpreted as `(&v).Abs().`
	-  Methods with **value receivers** take either a value or a pointer as the receiver when they are called
		```go
			type Vertex struct {
				X, Y float64
			}
			
			func (v Vertex) Abs() float64 {
				return math.Sqrt(v.X*v.X + v.Y*v.Y)
			}
			
			var v Vertex
			p := &v
		```
		`p.Abs()` is interpreted as `(*p).Abs().`
- In general, all methods on a given type should have either value or pointer receivers, but not a mixture of both.
