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

