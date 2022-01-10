# 트랜지션(transition)
트랜지션은 CSS 프로퍼티의 값이 변화할 때, 프로퍼티 값의 변화가 일정 시간(duration)에 걸쳐 일어나도록 하는 것이다.

```
﻿<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      width: 100px;
      height: 100px;
      background: red;
      /* 트랜지션 효과: 모든 프로퍼티의 변화를 2초에 걸쳐 전환한다. */
      transition: all 2s;
    }
    div:hover {
      border-radius: 50%;
      background: blue;
    }
  </style>
</head>
<body>
  <div></div>
</body>
</html>
```

→ div 셀렉터의 룰셋에 트랜지션을 설정하면 마우스가 올라갈 때(hover on)와 마우스가 내려올 때(hover off) 모두 트랜지션이 발동한다. 하지만 div:hover 셀렉터의 룰셋에 트랜지션을 설정하면 마우스가 올라갈 때(hover on)는 트랜지션이 발동하지만 마우스가 내려올 때(hover off)는 트랜지션이 발동하지 않는다.   

<br/>

※ 트랜지션(transition)은 상태 변화에 동반하여 변경되는 CSS 프로퍼티 값에 의한 표시의 변화를 부드럽게 하기 위해 애니메이션 속도를 조절한다. 즉, 프로퍼티 값의 변경이 표시의 변화에 즉시 영향을 미치게 하는 대신 그 프로퍼티 값의 변화가 일정 시간(duration)에 걸쳐 일어나도록 하는 것이다.

| 프로퍼티 | 설명 | 기본값 | 
| --- | --- | --- | 
| transition-property | 트랜지션의 대상이 되는 CSS 프로퍼티를 지정한다 | all | 
| transition-duration | 트랜지션이 일어나는 지속시간(duration)을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다 | 0s | 
| transition-timing-function | 트랜지션 효과를 위한 수치 함수를 지정한다. | ease | 
| transition-delay | 프로퍼티가 변화한 시점과 트랜지션이 실제로 시작하는 사이에 대기하는 시간을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다 | 0s | 
| transition | 모든 트랜지션 프로퍼티를 한번에 지정한다 | (shorthand syntax) | 

<br/>

## 1. transition-property
transition-property 프로퍼티는 트랜지션의 대상이 되는 CSS 프로퍼티명을 지정한다. 지정하지 않는 경우 모든 프로퍼티가 트랜지션의 대상이 된다. 복수의 프로퍼티를 지정하는 경우 쉼표(,)로 구분한다.   

<br/>
​
주의해야 할 사항은 모든 CSS 프로퍼티가 트랜지션의 대상이 될 수 없다는 것이다. 예를 들어 width, font-size, background-color 등은 하나의 범주(width, font-size는 크기, background-color는 색상)안에서 값이 변화하지만 display 프로퍼티는 그렇지 않다.   

<br/>
​
트랜지션의 대상이 될 수 있는 CSS 프로퍼티는 다음과 같다.

```
// Box model
width height max-width max-height min-width min-height
padding margin
border-color border-width border-spacing
// Background
background-color background-position
// 좌표
top left right bottom
// 텍스트
color font-size font-weight letter-spacing line-height
text-indent text-shadow vertical-align word-spacing
// 기타
opacity outline-color outline-offset outline-width
visibility z-index
```

layout에 영향을 주는 프로퍼티는 다음과 같다. (권장하지 않는다)

```
width height padding margin border
display position float overflow
top left right bottom
font-size font-family font-weight
text-align vertical-align line-height
clear white-space
```

<br/>

## 2. transition-duration

transition-duration 프로퍼티는 트랜지션에 일어나는 지속시간(duration)을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다. 프로퍼티값을 지정하지 않을 경우 기본값 0s이 적용되어 어떠한 트랜지션 효과도 볼 수 없다.

<br/>

## 3. transition-timing-function
트랜지션 효과의 변화 흐름, 시간에 따른 변화 속도와 같은 일종의 변화의 리듬을 지정한다.   

<br/>

대부분의 타이밍 함수는 큐빅 베이지어(cubic bezier)를 정의하는 네 점에 의해 정의되므로 상응하는 함수의 그래프로 제공해서 명시할 수 있다. transition-timing-function 프로퍼티값으로 미리 정해둔 5개의 키워드가 제공된다.

| 프로퍼티값 | 효과 | 
| --- | --- | 
| ease | 기본값. 느리게 시작하여 점점 빨라졌다가 느리지면서 종료한다. | 
| linear | 시작부터 종료까지 등속 운동을 한다. | 
| ease-in | 느리게 시작한 후 일정한 속도에 다다르면 그 상태로 등속 운동한다. | 
| ease-out | 일정한 속도의 등속으로 시작해서 점점 느려지면서 종료한다. | 
| ease-in-out | ease와 비슷하게 느리게 시작하여 느리지면서 종료한다. | 

<br/>

## 4. transition-delay
프로퍼티가 변화한 시점과 트랜지션이 실제로 시작하는 사이에 대기하는 시간을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다. 즉, transition-delay로 대기 사간을 지정하여 프로퍼티의 값이 변화하여도 즉시 트랜지션이 실행되지 않고, 일정 시간 대기한 후 트랜지션이 실행되도록 한다.

<br/>

## 5. transition
모든 트랜지션 프로퍼티를 한번에 지정할 수 있는 shorthand이다. 값을 지정하지 않은 프로퍼티에는 기본값이 지정된다. 지정 방법은 다음과 같다.

```
transition: property duration function delay
```

+ shorthand syntax   
transition-duration은 반드시 지정해야 한다.   
지정하지 않는 경우 기본값 0이 셋팅되어 어떠한 트랜지션도 실행되지 않는다. 기본값은 아래와 같다.

```
all 0 ease 0
```








