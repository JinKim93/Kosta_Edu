## console 객체
- **브라우저의 console 객체와 매우 유사**
- console.time, console.timeEnd : 시간로깅
- console.error : 에러 로깅
- console.log : 평범한 로그
- console.dir : 객체 로깅
- console.trace : 호출스택 로깅

### console.time 예제
```js
console.time('시간측정');
for(let i =0; i < 100000; i++){}
console.timeEnd('시간측정');
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/171073567-bb5c5e2c-13df-4b0c-9bf8-e16d61cb937c.png)

### 타이머 메서드
- set 메서드에 claer 메서드가 대응됨
- set 메서드의 리턴 값(아이디)을 clear 메서드에 넣어 취소
- **setTimeout(콜백함수, 밀리초)** : 주어진 밀리초(1000분의 1초) 이후에 콜백함수를 실행합니다
- **setinterval(콜백함수, 밀리초)** : 주어진 밀리초마다 콜백 함수를 반복 실행합니다
- **setimmediate(콜백함수)** : 콜백함수를 즉시 실행함
- **clearTimeout(아이디)** : setTimeout을 취소함
- **clearinterval(아이디)** : setinterval을 취소함
- **clearimmediate(아이디)** : setimmediate를 취소함
- setTimeout(콜백,0)보다 **setimmediate권장**
