# 애니메이션(Animation) 
애니메이션효과는 HTML 요소에 적용되는 CSS 스타일을 다른 CSS 스타일로 부드럽게 변화시킨다.    
애니메이션은 애니메이션을 나타내는 CSS 스타일과 애니메이션의 sequence를 나타내는 복수의 키프레임(@keyframes) 들로 이루어진다.   

<br/>

transition으로도 어느 정도의 애니메이션 효과를 표현할 수 있으나 animation보다는 제한적이다.    
일반적으로 트랜지션 효과는 요소 프로퍼티값이 다른 값으로 변화할 때 주로 사용하며 요소의 로드와 함께 자동으로 발동되지 않는다.   
 :hover 와 같은 가상 클래스 선택자(Pseudo-Class Selector) 또는 자바스크립트의 이벤트와 같은 부수적 액션에 의해 발동된다.

<br/>

즉 transition 프로퍼티는 단순히 요소의 프로퍼티 변화에 주안점이 있다면 animation 프로퍼티는 하나의 줄거리를 구성하여 줄거리 내에서 세부 움직임을 시간 흐름 단위로 제어할 수 있고 전체 줄거리의 재생과 정지, 반복까지 제어할 수 있다.   

<br/>

+ 비교적 작은 효과나 CSS만으로도 충분한 효과를 볼 수 있는 것은 CSS를 사용한다. 예를 들어 요소의 width 변경 애니메이션은 자바스크립트를 사용하는 것보다 훨씬 간편하며 효과적이다.

+ 세밀한 제어를 위해서는 자바스크립트 사용이 바람직하다. 예를 들어 바운스, 중지, 일시 중지, 되감기 또는 감속과 같은 고급 효과는 자바스크립트가 훨씬 유용하다.

<br/>

가장 중요한 것은 브라우저에서 애니메이션 효과가 부드럽게 실행되는 것이다. 그리고 애니메이션 효과 작성에 소요되는 시간과 수고이다.    

여러 사항들을 고려하여 자바스크립트를 사용하여야 할지 CSS를 사용하여야 할지 결정하여야 한다.

| 프로퍼티 | 설명 | 기본값 | 
| --- | --- | --- | 
| animation-name | @keyframes 애니메이션 이름을 지정한다 |  | 
| animation-duration | 한 싸이클의 애니메이션에 소요되는 시간을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다. | 0s | 
| animation-timing-function | 애니메이션 효과를 위한 타이밍 함수를 지정한다. | ease | 
| animation-delay | 요소가 로드된 시점과 애니메이션이 실제로 시작하는 사이에 대기하는 시간을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다 | 0s | 
| animation-iteration-count | 애니메이션 재생 횟수를 지정한다. | 1 | 
| animation-direction | 애니메이션이 종료된 이후 반복될 때 진행하는 방향을 지정한다. | normal | 
| animation-fill-mode | 애니메이션 미실행 시(종료 또는 대기) 요소의 스타일을 지정한다. |  | 
| animation-play-state | 애니메이션 재생 상태(재생 또는 중지)를 지정한다. | running | 
| animation | 모든 애니메이션 프로퍼티를 한번에 지정한다 (shorthand syntax) |  | 

<br/>

## 1. @keyframes
@keyframes   
CSS 애니메이션과 트랜지션 방식의 주된 차이는 @keyframes rule에 있다.    
이 rule을 사용하면 애니메이션의 흐름(sequence) 중의 여러 시점(breakpoint)에서 CSS 프로퍼티값을 지정할 수 있다.   

<br/>

@keyframes rule은 시간의 흐름에 따라 애니메이션을 정의한다. 여러 개의 키프레임을 정의하거나 애니메이션 중에 특정 CSS 프로퍼티에 값을 지정하는 지점을 정의할 수 있다.

```
@keyframes 이름 {}
```

```
@keyframes move {
  /* 애니메이션 시작 시점 */
  from { left: 0; }
  /* 애니메이션 종료 시점 */
  to   { left: 300px; }
}
```

→ from, to 키워드를 사용하여 애니메이션의 시작과 끝 시점을 정의하였다. 그리고 애니메이션의 시작 시점을 의미하는 from 키프레임 내에는 left 프로퍼티에 값 0을, 애니메이션의 끝 시점을 의미하는 to 키프레임 내에는 left 프로퍼티에 값 300px을 지정하였다. 그 결과, 정지 상태에서 오른쪽으로 300px 이동하는 애니메이션이 실행된다.

```
@keyframes move {
  0%   { left: 0; }
  50%  { left: 100px; }
  100% { left: 300px; }
}
```

→ from, to 키워드 대신 %를 사용할 수 있다. 또한 시작과 끝 키프레임 사이에 % 단위로 키프레임을 삽입할 수 있다.

<br/>

## 2. animation-name
@keyframes 뒤에 애니메이션을 대표하는 임의의 이름를 부여할 수 있다.

```
@keyframes 이름 {}
```

이 이름을 animation-name 프로퍼티값으로 지정하여 사용하고자 하는 @keyframes rule을 선택한다.    
하나 이상의 애니메이션 이름을 지정할 수 있다.

<br/>

## 3. animation-duration
한 싸이클의 애니메이션에 소요되는 시간을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다.

```
animation-duration: .5s;
animation-duration: 500ms;
```

animation-duration은 반드시 지정해야 한다. 지정하지 않는 경우 기본값 0s가 셋팅되어 어떠한 애니메이션도 실행되지 않는다.

<br/>

## 4. animation-timing-function
애니메이션 효과를 위한 수치 함수를 지정한다.    

<br/>

## 5. animation-delay
요소가 로드된 시점과 애니메이션이 실제로 시작하는 사이에 대기하는 시간을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다.

```
animation-delay: 2s;
```

<br/>

## 6. animation-iteration-count
애니메이션 주기의 재생 횟수를 지정한다. 기본값은 1이며 infinite로 무한반복 할 수 있다.

```
animation-iteration-count: 3;
```

<br/>

## 7. animation-direction
애니메이션이 종료된 이후 반복될 때 진행하는 방향을 지정한다.

| 프로퍼티값 | 설명 | 
| --- | --- |
| normal | 기본값으로 from(0%)에서 to(100%) 방향으로 진행한다. | 
| reverse | to에서 from 방향으로 진행한다. | 
| alternate | 홀수번째는 normal로, 짝수번째는 reverse로 진행한다. | 
| alternate-reverse | 홀수번째는 reverse로, 짝수번째는 normal로 진행한다. | 

<br/>

## 8. animation-fill-mode
애니메이션 미실행 시(대기 또는 종료) 요소의 스타일을 지정한다.

| 프로퍼티값 | 상태 | 설명 | 
| --- | --- | --- |
| none | 대기 | 시작 프레임(from)에 설정한 스타일을 적용하지 않고 대기한다. | 
|  | 종료 | 애니메이션 실행 전 상태로 애니메이션 요소의 프로퍼티값을 되돌리고 종료한다. | 
| forwards | 대기 | 시작 프레임(from)에 설정한 스타일을 적용하지 않고 대기한다. | 
|  | 종료 | 종료 프레임(to)에 설정한 스타일을 적용하고 종료한다. | 
| backwards | 대기 | 시작 프레임(from)에 설정한 스타일을 적용하고 대기한다. | 
|  | 종료 | 애니메이션 실행 전 상태로 애니메이션 요소의 프로퍼티값을 되돌리고 종료한다. | 
| both | 대기 | 시작 프레임(from)에 설정한 스타일을 적용하고 대기한다. | 
|  | 종료 | 종료 프레임(to)에 설정한 스타일을 적용하고 종료한다. | 

<br/>

## 9. animation-play-state
애니메이션 재생 상태(재생 또는 중지)를 지정한다. 기본값은 running이다.

<br/>

## 10. animation
모든 애니메이션 프로퍼티를 한번에 지정한다. 값을 지정하지 않은 프로퍼티에는 기본값이 지정된다.   
지정 방법은 다음과 같다.

```
animation: name duration timing-function delay iteration-count direction fill-mode play-state
```

animation-duration은 반드시 지정해야 한다. 지정하지 않는 경우 기본값 0s가 셋팅되어 어떠한 애니메이션도 실행되지 않는다.    

기본값은 아래와 같다.

```
none 0 ease 0 1 normal none running
```







