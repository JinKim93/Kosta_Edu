### git 관리시작
- git init

### git변경사항 확인
- git status

### git이라는 캡슐에 파일 담기
- git add 파일이름

### git이라는 캡슐에 모든파일 담기
- git add . 

### 상기작업 후 항상 git status 명령어로 상태확인하자 

### 캡슐을묻기(새로운 버전으로 만든다)
- git commit

### commit 메시지와 함께 작성해서 캡슐묻기
- git commit -m "first commit"

### commit 로그확인
- git log


## 프로젝트 과거시점으로 돌리기 (Reset VS Revert)

### Reset
- 해당 과거로 돌아간 다음 이후 행적은 지운다 

![image](https://user-images.githubusercontent.com/82345970/179450304-0bf615dc-b2bd-4d6a-b3e3-de717b7e66c0.png)

### Revert
- 내역을 삭제하는게 아니라, 이 때의 변화를 거꾸로 수행하는 캡슐을 하나 넣음
- 예를들어 여기서 추가한게 있으면 삭제하고, 변경한 게 있으면 그걸 반대로 수행
- 결과적으로 표시한 부분과 같은 상태로 돌아감

![image](https://user-images.githubusercontent.com/82345970/179450778-fd340d76-a85a-43e2-9452-485f4c3a2627.png)

### jinkim branch 생성
- git branch jinkim

### branch 목록확인
- git branch

### branch jinkim -> main으로 이동하기
- git switch main

### branch main -> jinkim으로 이동하기
- git switch jinkim

### branch 삭제하기
- git branch -d (삭제할 브랜치명)

### branch 이름바꾸기
- git branch -m (기존 브랜치명) (새 브랜치명)

## merge VS rebase

### merge

![image](https://user-images.githubusercontent.com/82345970/179452518-429d2df2-6f57-4803-8b37-418c093e8295.png)

### rebase

![image](https://user-images.githubusercontent.com/82345970/179452689-fa6d0841-a223-41e2-a28b-64af45cc15e6.png)

### jinkim 브랜치를 main브랜치로 merge
1. main브랜치도 이동
2. git merge jinkim

### merge는 reset으로 되돌리기 가능 

### 병합된 브랜치삭제
- git branch -d jinkim

### merge 중단하기
- git merge --abort

## CLI환경에서 깃허브(repository에 올리기)

1. git init
2. git status 상태확인
3. git add .
4. git commit -m "커밋메시지"
5. git remote add origin https://github.com/JinKim93/shoppinmall_kj.git
6. git branch -M main
7. git push -u origin main






