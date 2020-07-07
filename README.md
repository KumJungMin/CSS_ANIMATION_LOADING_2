# 로딩 화면(2), 두 개의 박스가 시간방향으로 도는 로딩화면

## 1. preview

<img src="https://j.gifs.com/ANzJL1.gif" />


## 2. 코드 분석

### 1) html
- `<div>`안에 두 개의 `<span>` 요소를 자식으로 둔다.
- `<span>`은 로딩할 때 움직이는 네모박스이다.
- `<span>` 대신 `<div>`를 써도 된다. 대신 `class` 이름을 지정해야한다.

<br/>

#### (1) 하나의 div에 span 요소를 자식으로 둔다.
```html
<body>
    <div class="loading">
      <span></span>
      <span></span>
    </div>
 </body>
```

<br/><br/>

### 2) css

#### (1) body안의 요소들을 상하좌우 중앙 배치한다.

```css

body {
    margin: 0; 
    display: flex;            /*내부 요소들이 차례로 배치 */
    justify-content: center;  /*내부 요소의 좌우 정렬 상태를 가운데로 설정*/
    align-items: center;      /*요소는 세로 중앙 배치*/
    height: 100vh;            /*웹 크기 변화에 따라 변경되는 반응형 수치*/
  }

```

<br/>

#### (2) 부모는 `relative`, 자식은 `absolute`로
- 부모 요소에서 `position :relative`를 하고 자식 요소를 `position :absolute`를 하면 고정적 위치 설정 가능하다.*/
- 부모 요소에서 `relative`이라고 안하면, `span`은 `body`를 기준으로 생각한다.

```css

 .loading {                    /*span요소의 부모*/
  width: 50px;
  height: 50px;
  position: relative;          /*화면변화가 있어도 자식은 같은 위치(1)*/ 
}

.loading span {
  position: absolute;          /*화면변화가 있어도 자식은 같은 위치(2)*/
  
  width: 20px;
  height: 20px;
  background-color: gray;
  top: 0;
  left: 0;
  animation: loading 1.5s linear infinite;
}

.loading span:nth-child(1) {
  animation-delay: 0s;          /*span에 애니메이션이 있으면 0s 딜레이 후 시작*/
  background-color: pink;
}
.loading span:nth-child(2) {
  animation-delay: 0.8s;        /*span에 애니메이션이 있으면 0.8s 딜레이 후 시작*/
  background-color: orange;
}

```

<br/>
<br/>

#### (3) `keyframe`을 사용하여 이벤트를 만든다.

- CSS 애니메이션에서 구간을 정하고 각 구간별로 다른 스타일을 적용시킬 수 있다.

- `animation-name`은 사용자가 직접 지정한 이름으로, @keyframes 가 적용될 애니메이션의 이름이다.

- `스테이지`는 0~100% 의 구간
 
- `CSS 스타일`은 각 스테이지(구간)에 적용시킬 스타일


```css

 @keyframes loading {
  0%,
  100% {
    top: 0;
    left: 0;
    background-color: coral;
  }
  25% {
    top: 0;
    left: calc(100% - 20px);
    /* 자기 자신의 부모 안에서 100%위치에 있도록 calc로 설정 */
    /* calc(100% - 자기자신의 너비를 뺌) */
    background-color: greenyellow;
  }
  50% {
    top: calc(100% - 20px);
    left: calc(100% - 20px);
    background-color: pink;
  }
  75% {
    top: calc(100% - 20px);
    left: 0;
    background-color: rgb(150, 64, 117);
  }
}

```

















