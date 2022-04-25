## Function 객체
- 함수를 객체처럼 사용할 수 있다

## Function 객체의 사용 형태
- new 연산자를 사용하여 Function 객체의 인스턴스를 생성
```html
var func = new Function(전달인자1, 전달인자2, ..., 계산식);
```
- Function 객체에 여러개의 전달인자를 대입하기도 하고, 계산식을 대입하기도 함
- 두 수를 입력받아 그 합을 구하고 반환하는 myAdd라는 함수의 형태는 다음과 같다
```html
function myAddd(x,y)
{
  var hap = x+y;
  return hap;
}
```
- Function 객체를 사용한 형태로 변경
```html
var myAdd = new Function('x,y','return(x+y)');
```

## Number 객체
- Number는 숫자형 타입 객체
- Number 객체의 제공 속성을 사용할 경우나 문자열을 숫자로 형변환 하는 경우

## Number 객체의 사용 형태
- new 연산자를 사용하여 Number 객체의 인스턴스르 생성
```html
var objNum = new Number("1234");
```
- Number 객체의 전달인자인 ""안에 숫잠ㄴ 들어와야 하고, 그 이외의 문자가 들어가면 숫자가 아니므로 NAN이 출력된다<br> -> 표현할수 없는 데이터는 NAN 으로 표시


