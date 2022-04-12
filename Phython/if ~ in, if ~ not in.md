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

### kim으로 되 있는 문자열 제외 후 출력
```py
df_list = ["kim_a","kim_b","kim_c","kim_k","seo_a","seo_b","seo_c","seo_s"]
for col in df_list:
    if "kim" not in col:
        print(col)
```
### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162908899-fcc63444-5a94-4193-9639-ea2c9c4b4686.png)

### 리스트 중 선택 안 할 리스트 제외 후 출력 
```py
df_list = ["kim_a","kim_b","kim_c","kim_k","seo_a","seo_b","seo_c","seo_s"]
unselect_list = ["kim_a","seo_a"]

for col in df_list:
    if col not in unselect_list:
        print(col)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162909464-e8c5c9a5-f71a-4fb7-a501-47fc39aa0c39.png)




    
