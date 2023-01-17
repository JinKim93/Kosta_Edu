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

```go
//여러 이름을 출력하시오

package main

import "fmt"

func repeatMe(words ...string) {

	fmt.Println(words)

}

func main() {

	repeatMe("hi","hello","nice")
}
```

## defer
```go
//naked return function

package main

import (
	"fmt"
	"strings"
)

//defer function이 끝났을때 추가적으로 무엇인가 동작하도록 하는함수
func lenAndUpper(name string) (length int, uppercase string) {

	defer fmt.Println("hi")
	length = len(name)
	uppercase = strings.ToUpper(name)
	return 
}

func main() {

	totallength, upperName := lenAndUpper("jkim")
	fmt.Println(totallength, upperName)
	
}
```

## for문 range 활용
```go
//naked return function

package main

import (
	"fmt"
)

func superAdd(numbers ...int) int {

	for index, number := range numbers{
		fmt.Println(index, number)
	}
	return 1

}

func main() {

	//var total int =
	superAdd(1, 2, 3, 4, 5)

}
```
```go
package main

import "fmt"

func addloop(numbers ...int) {

	for index, number := range(numbers) {
		fmt.Println(index, number)
	}

}

func main() {

	addloop(1,2,3,4,5)
}
```
```go
package main

import "fmt"

func addloop(numbers ...int) {


for i:= 0 ; i < len(numbers); i++ {

	fmt.Println(numbers[i])
}

	

}

func main() {

	addloop(1,2,3,4,5)
}
```



