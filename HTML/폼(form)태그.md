## 폼(form)태그
- 폼 태그는 텍스트 필드, 라디오 버튼, 체크 박스, 전송 버튼 등이 위치하게 함
- 사용자가 브라우저에 입력한 정보를 submit 버튼을 누르면 지정한 url로 정보를 전송

```html
<form method = "get" action = "confirm.php">
</form>
```

## 폼 태그 속성
- 폼은 사용자로부터 입력한 데이터를 처리해야 하기 때문에 기본적으로 통신방식을 설정하고, 처리하는 루틴을 읽어와야함
- **method** : 통신방법을지정, **get,post**방식 두가지가 있다.<br/>**get 방식**은 1KB이상의 데티러를 처리할때 사용, **post방식**은 1KB미만의 데이터를 처리할때 사용 
- **action** : 입력된 정보를 처리하는 프로그램의 경로를 지정

## 입력(input)태그
- 입력태그는 입력 양식 중 가장 기본적인 형태로 타입 속성값에 따라 여러가지 형태로 출력을 할수 있다 

## 입력 태그 속성
![image](https://user-images.githubusercontent.com/82345970/163739700-1df6f1e3-54e7-4f34-a080-dc9a4d017141.png)

### 텍스트(Text) 필드
- 임의의 문자를 입력 받을 때 사용하는 필드
```html
<input type="text" name="my_id">
```
- type 속성은 비단 텍스트 필드 뿐만 아니라 , 폼 태그 내에서는 필수적 속성
 
### 텍스트(Text) 필드 부가적 속성
![image](https://user-images.githubusercontent.com/82345970/163739784-51662907-4835-4386-8dff-d81a1591ea10.png)

