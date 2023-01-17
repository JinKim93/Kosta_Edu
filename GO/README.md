## GO 언어
### GO는 export할 함수는 첫글자 대문자로 작성 -> 첫글자가 대문자이면 다른 패키지로부터 export 된거다

## 상수
### 상수는 값 변경 안됨 
```go
package main

import "fmt"

func main() {

	const name string = "jkim"
	name = "jkim2"
	fmt.Println(name)
}
```
## 변수
### 축약형은 함수 안에서만 사용이 가능하다.
```go
package main

import "fmt"


var name bool = false
var name2 string ="hi"
func main() {

	//name := "jkim"
	var name string = "jkim" 
	fmt.Println(name)

}

}
```
## 함수
```go
package main

import "fmt"

/*
func multiply(a int, b int) int {

	return a * b
}
*/
func multiply (a,b int) int {
	return a*b
}

func main() {

	fmt.Println(multiply(3,2))
}
```
