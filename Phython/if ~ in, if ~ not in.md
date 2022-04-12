# if ~ in / if ~ not in
- if A in B:  B안에 A가 있으면 참
- if A not in B: B안에 A가 없다면 참
- B에는 리스트, 튜플, 문자열을 사용할 수 있다

```py
arr_list = [1,2,3,4,5]
if 9 not in arr_list:
    print("9가 없다")
else: 
    print("9가 있다")
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162905850-4b8f5b17-81fd-4d56-bcc7-96c938649561.png)

```py
string = "Hello"
if "a" not in string:
    print("a가 문자열 안에 없다")

if 'e' in string:
    print("e가 문자열 안에 있다")    
    
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162906150-1557c420-e4f7-4ee3-a2e5-b1299e1ffbe1.png)


    
