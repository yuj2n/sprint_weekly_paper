- Q1. CSS의 Cascading에 대해 설명해 주세요.
- Q2. 시맨틱 태그를 사용하면 좋은 점을 설명해 주세요.
<hr>

# ❓Q1
![image](https://github.com/user-attachments/assets/7c1a4f06-fe03-4f8c-84b1-ce9de9162894)

**Cascading**: 폭포, 위에서 아래로 쏟아지는의 뜻을 가진 중요한 스타일 적용 규칙.

CSS: Cascading Style Sheet의 약자로 위에서 아래로 떨어지는 스타일 적용을 의미함

CSS를 사용하다보면 같은 요소에 대하여 여러 스타일이 중복되는 경우 존재.
```
<div style='background-color: #white'>
  <p style='background-color: #black'>캐스케이딩</p> /* 이 경우 black이 적용 */
</div>
```
p는 div의 스타일도 상속받고 본인에게 지정된 스타일도 있는 경우, 
어떠한 스타일을 적용할 지에 대한 규칙을 세우기 위해 캐스케이딩을 채택함

**- 캐스케이딩 원칙**
1. 스타일 우선순위
2. 스타일 상속

## 스타일 우선순위

#### 결정요소

### 1. 중요도

중요도: 스타일 선언 위치에 따라 우선순위 매김
![image](https://github.com/user-attachments/assets/d9f7eb76-1b70-4325-8c63-7d6beb66491a)

**중요도 끌어올리기**

![image](https://github.com/user-attachments/assets/7ec647c1-2507-4579-a6e7-21bb87b7a721)

```
h2 {
    background-color: red **!important**;
}

h2 {
    background-color: blue;
}
```
  
### 2. 명시도

명시도: 셀렉터가 가리키는 것이 명확할수록 우선순위를 높게 주는 것

![image](https://github.com/user-attachments/assets/a2294283-b4f9-43c6-967b-facfd0c64f4e)

**예시**

![image](https://github.com/user-attachments/assets/bf3f062b-bd90-41d6-973d-74215564212c)


```
 <h2>태그 셀렉터</h2>
  <h2 class='cls'>클래스 셀렉터</h2>
  <h2 id='i' class='cls'>아이디 셀렉터</h2>
  <h2 class='cls' style='background-color: green'>인라인 셀렉터</h2>
```
```
h2 {
    background-color: red;
}

.cls {
    background-color: blue;
}

#i {
    background-color: violet;
}
```

### 3. 코드 순서

코드 순서: 마지막 등장한 속성을 최우선 적용하는 것
```
h2 {
    color: red;
}

h2 {
    color: green;  /* 이때 마지막 적용한 green이 적용됨 */
} 
```

## 스타일 상속
스타일 상속: 태그들이 어떻게 포함되었는지에 따라 스타일 적용 여부 결정 원칙
Ex) 부모 요소에만 스타일 적용한 경우 자식 요소에도 스타일이 적용됨
```
<div style='background-color: lightgreen;'>
      부모
      <div>자식</div>
</div>
```

## 📝결론
우선순위와 상속을 통해 어떤 스타일이 적용될지 결정되는 것을 캐스케이딩이라 하며,
CSS를 다루다가 원하는 속성이 적용되지 않는다면 캐스케이딩 규칙이 잘 지켜지고 있는지 
확인해볼 필요가 있음.

<hr> 

# ❓Q2

**시맨틱 태그(Semantic tag)**: 배치 기준으로 의미를 가진 태그 

![image](https://github.com/user-attachments/assets/18867f4c-ce90-421a-ad5b-ef60bd48adec)


- 똑같은 div 영역이지만, 문서 안에서 다른 의미를 가짐
💡 의미를 가진 태그로 만들고 싶어짐
  

**<용도>**
```
<header>: 영역 위쪽에서 로고나 제목, 메뉴 같은 걸 담고 있는 도입부
<main>: 사이트의 본격적인 내용으로 페이지에서 딱 한 번만 사용 가능
<footer>: 영역 아래쪽에서 여러 가지 연락처나 관련 정보를 담고 있음
<article>: 하나의 완성된, 독립적인 내용을 나타내는 영역
<section>: 어떤 것의 일부분을 나타내는 영역
<figure>: 이미지와, 이미지 설명을 담고 있는 영역
```


- **시맨틱 태그의 장점**
1. 검색 최적화(SEO)
2. 웹 접근성(Web Accessibility)
3. 개발자의 생산성 향상
   

## 1. 검색 최적화 

![image](https://github.com/user-attachments/assets/555d80b4-b069-40bc-9947-a9d9cf7bc687)

- 웹 사이트 검색 시 원하는 내용을 알맞게 보여주는 것
- 사용자가 원하는 내용과 일치하는 경우 화면 **맨 위**에 보여줌!
- **SEO**하는법: <meta>태그 꼼꼼히 작성/시맨틱 태그 작성
  

## 2. 웹 접근성
- 2020년 기준 전체 인구 **15%** = 장애인
![image](https://github.com/user-attachments/assets/7d219b1d-3ffb-42bb-a240-73de34f697c8)


- 이 중 시각장애인은 인터넷 사용에 어려움을 겪음
-> screen reader라는 화면을 소리내어 읽어주는 프로그램 사용
- 이때, 시맨틱 태그를 사용 시 **장벽 없는 인터넷**을 만들 수 있음.
  

## 3. 개발자의 생산성 향상

![image](https://github.com/user-attachments/assets/f7066d43-cc1f-4f18-98c8-7971346de265)



- 개발자는 눈에 보이는 화면이 아닌 코드를 보며 사이트를 이해함.
- **가독성**이 올라가 코드를 보기 편리함.


## 📝결론
- 시맨틱 태그를 무조건 사용해야하는 것은 아님.
- 의미에만 집착하다보면 정작 코드를 작성하기 어려울 수 있음
