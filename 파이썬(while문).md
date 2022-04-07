# 파이썬 while문

```py
iloop = 0
while iloop < 5:
    print("Programming")
    iloop += 1 #파이썬에서는 증감연산자 쓰면 안됨 -> iloop++

```

### 1부터 10까지의 합

```py
iloop = 0
sum = 0
while iloop < 11:
    sum = sum + iloop
    iloop += 1

print("1부터 10까지의 합은",sum)
```

### 1부터 100까지 홀수의 합

```py
iloop = 0
sum = 0
while iloop < 101:
    if(iloop % 2 == 1):
        sum = sum + iloop
    iloop += 1

print("1부터 100까지의 홀수합은",sum)
```

### 구구단 출력

```py
val = 1
dan = int(input('단수를 입력하세요 : '))
while val < 10:
    #print(dan, '*', val, '=', dan * val)
    print("%d * %d = %d" %(dan,val, dan*val))
    val = val + 1
```

### break문

```py
a = 0
while True:
    if a > 100:
        break
    print('a의 값은 :',a)
    a = a + 1
print('a는 100보다 크다')

```

### continue문

- 어느 구간을 스킵하고 싶을때 continue문 쓴다

```py
a = 0
while a < 100:
    a = a+ 1
    if a > 80 and a < 90: # 81 ~ 89까지 출력 안됨
        continue
    print('a의 값은 :',a)
```





