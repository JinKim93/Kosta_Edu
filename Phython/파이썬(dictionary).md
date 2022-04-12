# dictionary
- 편의점의 바코드(상품명과 가격정보가 한 쌍으로 관리)
- 삼각김밥 : 1000원
- 컵라면 : 800원
- 키와 값의 쌍으로 데이터 관리

```py
딕셔너리변수 = {키1 : 값1, 키2 : 값2, 키3 : 값3}
```

### 딕셔너리 추가
```py
product = {"컵라면" : 800, "삼각깁밥" : 1000, "소세지" : 1500}
print(product)
product["오뎅"] = 2000
product["닭다리"] = 3000
product["아이스크림"] = 1000
print(product)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162899744-0b8806b4-da0a-405b-9e24-d890dc191bb2.png)


### dictionary VS 리스트
- 딕셔너리는 [] -> 대괄호
- 리스트는 {} -> 중괄호

### 딕셔너리 삭제

```py
del(딕셔너리이름['키']
```

```py
product = {"컵라면" : 800, "삼각깁밥" : 1000, "소세지" : 1500}
print(product)
product["오뎅"] = 2000
product["닭다리"] = 3000
product["아이스크림"] = 1000
print(product)

del(product['컵라면'])
print(product)
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162900234-a4140efb-6e31-49a0-8574-9ac1cdb800d7.png)

### 키를 통해 값에 접근하는 get()함수

```py
딕셔너리이름.get(키)
```
### 딕셔너리의 모든 키를 반환하는 keys() 함수
```py
딕셔너리이름.keys()
```

### 딕셔너리의 모든 값을 반환하는 values() 함수
```py
딕셔너리이름.values()
```

### 딕셔너리 함수(get(),keys(),values())
```py
product = {"컵라면" : 800, '삼각깁밥' : 1000, "소세지" : 1500}
print(product)
product["오뎅"] = 2000
product["닭다리"] = 3000
product["아이스크림"] = 1000
print(product)

del(product['컵라면'])
print(product)

print(product.get('소세지'))
print(product.keys()) #리스트로 리턴
print(product.values())
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162901326-bf239bf3-9875-4689-b2e5-b50d48d3717d.png)

### ### 딕셔너리 함수(keys(),values() 출력시 dict_keys, dict_values 안나오게 하는법)
```py
product = {"컵라면" : 800, '삼각깁밥' : 1000, "소세지" : 1500}
print(product)
product["오뎅"] = 2000
product["닭다리"] = 3000
product["아이스크림"] = 1000
print(product)

del(product['컵라면'])
print(product)

print(product.get('소세지'))
print(list(product.keys())) #리스트로 리턴
print(list(product.values()))
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162901511-a7d23098-90ea-42c5-b382-fd7d8a112b78.png)

### 딕셔너리 안에 있는 키값 검사(in 기능 사용)
```py
product = {"컵라면" : 800, '삼각깁밥' : 1000, "소세지" : 1500}

item = input('상품을 입력하세요 : ')
if(item in product):
    print("상품이 있습니다")
else:
    print("존재하지 않습니다")
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162902519-cc2f5f9e-896d-49d0-aa6d-2308579b8b6f.png)

### 나라 이름 입력하면 나라의 수도 이름이 출력되는 프로그램 
```py
capital = {'네팔' : '카트만두',
        '대한민국' : '서울',
        '일본' : '도쿄',
        '중국' : '베이징',
        '이탈리아' : '로마',
        '러시아' : '모스크바',
        '독일' : '베를린',
        '미국' : '워싱턴',
        '프랑스' : '파리',
        '영국' : '런던' }

while(True):
    contry = input(str(list(capital.keys())) + "나라의 수도는 무엇일까요?")
    if contry in capital:
        print(contry, "의 수도는", capital.get(contry),'입니다' )
                
    elif contry == "exit":
        break
    else:
        print("그런 나라가 없습니다")       
```

### 출력결과
![image](https://user-images.githubusercontent.com/82345970/162904721-7b7665de-82ae-4c59-98f7-7d4f7429a6e2.png)


