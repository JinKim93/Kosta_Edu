# 파이썬 for문

![image](https://user-images.githubusercontent.com/82345970/161917817-f00ee749-bd99-40ad-9a29-42645910a240.png)

```py
for num in range(0,5,1):
    print("Programming")
```

```py
for num in range(0,5,1):
    print(num + 1, "Programming")
```
![image](https://user-images.githubusercontent.com/82345970/161919440-993e4d45-67b4-4182-9cdc-3e788d9bca8b.png)


### 1부터 10까지의 합

```py
sum = 0
for i in range(1,11,1):
    sum += i
print("1부터 10까지의 합은 :",sum)
```

### 지구의 자전 주기

```py
for i in range(1,366,1):
    print(i, "일 지났습니다")
```

### 1부터 100까지 짝수의 합

```py
#1부터 100까지 짝수의 합

sum = 0
for i in range(1,101,2):
    sum = sum + i

print("1부터 100까지 짝수의 합은 :",sum)
```

### 구구단출력

```py
dan = int(input('단수를 입력하세요 :'))
for val in range(1,10,1):
    print('%d* %d = %d' % (dan,val, dan * val) )
    
```

### 입력한 숫자의 구구단 출력(출력시 가로로 나오게)

```py
dan = int(input('단수를 입력하세요 :'))
for val in range(1,10,1):
    print('%d*%d = %d' % (dan,val, dan*val), end='   ' )
```    

![image](https://user-images.githubusercontent.com/82345970/161925410-3e6704fb-bea3-46ac-a8ba-36acdda8bb82.png)

### 구구단출력(2단 ~ 9단)
```py
for val in range(2,10,1):
    for val2 in range(1,9,1):
        print('%d*%d = %d' % (val,val2, val*val2), end='   ' )

    print()    
```


        


