- 🇶1. Git에서 branch merge 방법들과 각 방법의 특징을 설명해 주세요.
- 🇶2. Git Flow 브랜치 전략에 대해 설명해 주세요.
<hr>

# 🔍Q1.

> branch merge: 현 branch에서 다른 branch를 합친다.(병합)
- 사용하는 경우:   
    - A 브랜치에서 작업한 내용을 main 브랜치에 반영하기 위해 병합 시
    - A 브랜치에서 작업 중인데 main 브랜치에 최신 변경 사항 적용 시 


**merge 방법**
1. merge
2. squash
3. rebase

## 1. merge
```
git merge <병합할 브랜치>
```
- 기본적으로 사용되며, 두 브랜치 병합 시 과거 생성된 커밋과 히스토리를 유지하면서 병합한다는 특징이 있음

## 2. squash
```
git merge --squash <병합할 브랜치>
```
- 병합할 브랜치의 커밋 메시지들을 합쳐 하나의 커밋 메시지로 만들어 merge
- 여러 커밋 메시지를 합치게 되어 커밋 히스토리가 간결해짐
- 반면 추후 어떤 내용이 변경되었는지 알기 어렵다

## 3. rebase
```
git rebase <재베이스할 브랜치>
```
- 현 브랜치 커밋들이 재베이스할 브랜치의 새 커밋 아이디를 가진 커밋으로 새로 추가
- 히스토리가 깔끔하게 유지되지만, 코드 충돌 가능성이 높음.

# 🔍Q2

## git Flow 브랜치 전략?
- 협업을 위해 branch에서 작업하는데, 이 branch를 규칙없이 생성하면 어떤 기능의 브랜치인지 혼란 야기 가능
-> git Flow 브랜치 전략 필요
- 프로젝트 관리를 위한 git 브랜치를 효과적으로 관리하기 위한 워크플로우

### 종류
- Main 브랜치 
- Develop 브랜치
- Supporting 브랜치
    - Feature 브랜치
    - Release 브랜치
    - Hotfix 브랜치

### Main 브랜치
- 출시 가능한 프로덕션 코드를 모아두는 브랜치

### Develop 브랜치
- 다음 버전 개발을 위한 코드를 모아두는 브랜치. 개발 완료 시 Main 브랜치로 merge

### Feature 브랜치
- 하나의 기능을 개발하기 위한 브랜치. Develop 브랜치에서 생성하며, 기능 개발 완료 시 다시 Develop 브랜치로 merge

### Release 브랜치
- 소프트웨어 배포를 준비하기 위한 브랜치. Develop 브랜치에서 생성하며, 배포 준비 완료 시 Main과 Develop 브랜치에 둘 다 merge 한다.

### Hotfix 브랜치
- 이미 배포된 버전에 문제 발생 시 사용. Main 브랜치에서 생성하며, 문제 해결 시 Main과 Develop 브랜치에 둘다 merge