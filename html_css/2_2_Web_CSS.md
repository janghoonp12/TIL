# 0801 Web_CSS
# CSS
- Cascading Style Sheets
- 계단식
- 스타일을 지정하기 위한 언어
  - 선택하고, 스타일을 지정한다.
  - HTML을 선택하고 특정 태그를 선택하고 스타일을 지정

> CSS 구문 - 용어 정리
```css
h1{
  color: blue;
}
```
- `h1`: 선택자(Selector)
- `color: blue;` 선언
- `color`: 속성(Property)
- `blue`: 값(Value)

> CSS

- CSS 구문은 선택자를 통해 스타일을 지정할 HTML 요소를 선택
- 중괄호 안에서는 속성과 값, 하나의 쌍으로 이루어진 선언을 진행
- 각 쌍은 선택한 요소의 속성, 속성에 부여할 값을 의미
  - 속성(Property): 어떤 스타일 기능을 변경할지 결정
  - 값(Value): 어떻게 스타일 기능을 변경할지 결정

> CSS 정의 방법
- 인라인(Inline): 태그에 바로 스타일 적용
  - 인라인을 쓰게 되면 실수가 잦아짐(중복도 있을 것이고, 찾기가 어려워서)
  ```html
  <h1 style="color: blue; font-size: 100px;">Hello</h1>
  ```

- 내부 참조(embedding): `<style>`
  - 내부 참조를 쓰게 되면 코드가 너무 길어짐
  ```html
  <head>
    <title>Title</title>
    <style>
      h1 {
        color: blue;
        font-size: 100px
      }
    </style>
  </head>  
  ```

- 외부 참조: 분리된 CSS 파일
  - 가장 많이 쓰는 방식
  ```html
  <head>
    <title>title</title>
    <link rel="stylesheet" href="mystyle.css">
  </head>
  ```

> CSS 시작하기전에
- ! + tab 하면 html 기본 구조 생김
- 선택자의 우선순위에 따라 적용
- 실제로 사용하는 태그는 3~40개 정도
- lorem: 텍스트 생성


## CSS Selectors
---
> 선택자(Selector) 유형
- 기본선택자
  - 전체 선택자, 요소 선택자
  - 클래스 선택자, 아이디 선택자, 속성 선택자

- 결합자(Combinators)
  - 자손 결합자, 자식 결합자
  - 일반 형제 결합자, 인접 형제 결합자

- 의사 클래스/요소(Pseudo Class)
  - 링크, 동적 의사 클래스
  - 구조적 의사 클래스, 기타 의사 클래스, 의사 엘리먼트, 속성 선택자

> CSS 선택자 예시
```html
<style>
  /* 전체 선택자 */
  * {
    color: red;
  }

  /* 요소 선택자 */
  h2 {
    color: orange;
  }

  h3,
  h4 {
    font-size: 10px;
  }

  /* 클래스 선택자 */
  .green {
    color: green;
  }

  /* id 선택자 */
  #purple {
    color: purple;
  }

  /* 자식 결합자 */
  .box > p {
    font-size: 30px;
  }

  /* 자손 결합자 */
  .box p {
    color: blue;
  }
</style>
```

> CSS 선택자 정리
- 전체 선택자
  - (*) 사용

- 요소 선택자
  - HTML 태그(h1, header 등)를 직접 선택
  - 서울 사람

- 클래스(class) 선택자
  - 마침표(.) 문자로 시작하며, 해당 클래스가 적용된 항목을 선택
  - 최씨, 김씨
  
- id 선택자
  - `#` 문자로 시작하며, 해당 아이디가 적용된 항목을 선택
  - 일반적으로 하나의 문서에 1번만 사용
  - 여러 번 사용해도 동작하지만, 단일 id를 사용하는 것을 권장
  - 지웅, 길동

> CSS 적용 우선순위 (cascading order)

- CSS 우선순위를 아래와 같이 그룹을 지어볼 수 있다.
  - (1) 중요도 (Importance) - 사용시 주의
    - `!important`
  - (2) 우선 순위 (Specificity)
    - 인라인 > id > class, 속성, pseudo-class > 요소, pseudo-element
  - (3) CSS 파일 로딩 순서
    - 클래스 적힌 순서 아님

> CSS 상속

- CSS는 상속을 통해 부모 요소의 속성을 자식에게 상속한다.
  - 속성(프로퍼티) 중에는 상속이 되는 것과 되지 않는 것들이 있다.
  - 상속 되는 것 예시
    - 예) Text 관련 요소(font, color, text-align), opacity, visibility 등
  - 상속 되지 않는 것 예시
    - 예) Box model 관련 요소(width, height, margin, padding, border, box-sizing, display), position 관련 요소(position, top/right/bottom/left, z-index) 등


## CSS 기본 스타일
---
> 크기 단위

- px(픽셀)
  - 모니터 해상도의 한 화소인 '픽셀' 기준
  - 픽셀의 크기는 변하지 않기 때문에 고정적인 단위

- `%`
  - 백분율 단위
  - 가변적인 레이아웃에서 자주 사용

- em (자식 0.5배)
  - (바로 위, 부모 요소에 대한) 상속의 영향을 받음
  - 배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈를 가짐

- rem
  - (바로 위, 부모 요소에 대한) 상속 영향을 받지 않음
  - 최상위 요소(html)의 사이즈를 기준으로 배수 단위를 가짐
    - 브라우저 기본 16px -> 2rem: 32px

> 크기단위 (viewport)

- 웹 페이지를 방문한 유저에게 바로 보이게 되는 웹 컨텐츠의 영역 (디바이스 화면)
- 디바이스의 viewprot를 기준으로 상대적인 사이즈가 결정됨
- vw, vh, vmin, vmax
- px는 브라우저의 크기를 변경해도 그대로
- vw는 브라우저의 크기에 따라 크기가 변함

> 색상단위
- 색상 키워드(`background-color: red;`)
  - 대소문자를 구분하지 않음
  - red, blue, black 과 같은 특정 색으 직접 글자로 나타냄
- RGB색상(`background-color: rgb(0, 255, 0);`)
  - 16진수 표기법('#'+16진수) 혹은 함수형 표기법을 사용해서 특정 색을 표현하는 방식
- HSL 색상(`background-color: hsl(0, 100%, 50%;`)
  - 색상, 채도, 명도를 통해 특정 색을 표현하는 방식
- a는 alpha(투명도)

> CSS 문서 표현

- 텍스트
  - 서체(font-family), 서체 스타일(font-style, font-weight 등)
  - 자간(letter-spacing), 단어 간격(word-spacing), 행간(line-height) 등

- 컬러(color), 배경(background-image, background-color)
- 기타 HTML 태그별 스타일링
  - 목록(li), 표(table)


## CSS Selectors 심화
---
> 결합자 (Combinators)
- 자손 결합자(공백)
  - selectorA 하위의 모든 selectorB 요소
- 자식 결합자 (>)
  - selectorA 바로 아래의 selectorB 요소
- 일반 형제 결합자(~)
  - selectorA의 형제 요소 중 뒤에 위치하는 selectorB 요소를 모두 선택
- 인접 형제 결합자(+)
  - selectorA의 형제 요소 중 바로 뒤에 위치하는 selectorB 요소를 선택

## CSS Box model
---
> CSS 원칙 1
- CSS의 모든 요소는 네모(박스모델)이고,
- 위에서부터 아래로, 왼쪽에서 오른쪽으로 쌓인다 (좌측 상단에 배치)

> Box model
- 모든 HTML 요소는 box 형태로 되어있음
- 하나의 박스는 네 부분(영역)으로 이루어짐
  - margin, border, padding, content

> Box model 구성
- margin: 테두리 바깥의 외부 여백, 배경색 지정 x
  - border: 테두리 영역
    - padding: 테두리 안쪽의 내부 여백, 요소에 적용된 배경색, 이미지는 padding까지 적용
      - content: 글이나 이미지 등 요소의 실제 내용

> Box sizing
- 기본적으로 모든 요소의 box-sizing은 coontent-box
  - Padding을 제외한 순수 contents 영역만을 box로 지정
- 다만, 우리가 일반적으로 영역을 볼 때는 border까지의 너비를 100px 보는 것을 원함
  - 그 경우 box-sizing을 border-box로 설정


## CSS Display
---
> CSS 원칙 2
- display에 따라 크기와 배치가 달라진다.

> 대표적으로 활용되는 display
- display: block
  - 줄 바꿈이 일어나는 요소
  - 화면 크기 전체의 가로 폭을 차지한다.
  - 블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있음.

- display: inline
  - 줄 바꿈이 일어나지 않는 행의 일부 요소
  - content 너비만큼 가로 폭을 차지한다.
  - width, height, margin-top, margin-bottom을 지정할 수 없다.
  - 상하 여백은 line-height로 지정

> 블록 레벨 요소와 인라인 레벨 요소
- 이것저것 있음
> 블록
- 한줄 다 차지함
> 인라인
- inline 기본 너비는 컨텐츠 영역만큼
- 글자처럼 취급?

> 속성에 따른 수평 정렬
- margin에 따라 좌우 가운데 정렬
- text-align 글자 정렬
  - 부모요소에 넣어줘야함

## CSS Position
> CSS position
- 문서 상에서 요소의 위치를 지정
- relative
  - 원래 있어야 할 위치에서 이동
  - 원래 위치는 차지하고 있음...
- absolute
  - 브라우저 화면 기준으로 이동
  - 붕뜸? 겹쳐짐?
  - normal flow에서 벗어나 부모/조상 요소를 기준으로 위치
    - 못만나면 브라우저 기준
- fixed
  - 얘도 붕떠서 고정위치에 고정
  - viewport 기준으로 위치
- sticky
  - 스크롤에 따라 static에서 fixed로 바뀜

