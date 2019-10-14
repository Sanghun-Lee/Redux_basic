# Redux

> 해당 코드는 생활코딩의 Redux강의를 보고 만들었습니다.<br>
> https://www.youtube.com/playlist?list=PLuHgQVnccGMB-iGMgONoRPArZfjRuRNVc

## store 생성

- store를 생성하기 위해선 reducer함수가 필요하다.

```javascript
var store = Redux.createStore(reducer);
```

## reducer 함수 생성

```javascript
/*
 * dispatch함수를통해 받은 action객체와 기존의(이전의)state를 매개변수로 받는다.
 * action객체에는 type이란 이름의 key가 반드시 존재해야 한다.
 * 그리고 그 type이 어떤 것이냐에 따라 리듀서 함수 내에서 state를 변화시킨다.
 * 하지만 직접 변경시켜서는 안된다.??
 *    >> dispatch함수를 호출할 때 state에 들어갈 값을 객체로 전달해 주어야 한다.
 *
 * 그리고 새로운 state를 return 한다.
 */
function reducer(state, action) {
  if (state === undefined) {
    // initialState
    return {color: 'yellow'};
  }

  if (action.type === 'CHANGE_COLOR') {
    // state의 객체들이 빈 객체 {}에 복사되어 리턴된 새로운 객체를 newState에 할당한다.
    var newState = Object.assign({}, state, {color: action.color});
  }
  return newState; // 새로운 state를 리턴해준다.
  // 그래서 각각의 객체들이 독립적으로 존재하게 된다.
}
```

## dispatch함수로 state변경

```javascript
store.dispatch({type: 'CHANGE_COLOR', color: 'red'});
// dispatch는 action객체를 넘겨준다.
// 여기서 action객체 >> {type : 'CHANGE_COLOR', color : 'red'}
// action객체 안에 변경되어야 할 state값을 전달해 주어야 한다.
// * 단, state의 값에 따라 변경되는 경우 (카운터) 그냥 리듀서 함수 내에서 수정되어도 무방하다.
```

## subscribe함수 사용

- subscribe함수는 state객체가 바뀔 때 마다 다시 랜더링 해야하는 함수를 지정해준다.

```javascript
store.subscribe(red); // red는 다시 랜더링할 함수 이름, 여러개 존재할 수 있다.
```

## store에서 state가져오기

```javascript
var state = store.getState();
```

## <br>

---

## <br>

**노마드코더의 강의나 다른 리덕스 강의같은 경우는 action들을 분리한다.**

## 1. action type이름을 변수로 만든다.

```javascript
'CHANGE_COLOR'
>>> export const CHANGE_COLOR = 'CHANGE_COLOR';
```

## 2. dispatch안에 들어갈 action객체는 객체를 생성해주는 함수로 만든다.

```javascript
store.dispatch({type: 'CHANGE_COLOR', color: 'red'});
>>>
export const change_color = (color) => ({
    type: CHANGE_COLOR,
    color : color
    // [color : color]는 [color]로 대체할 수 있다.
});
// const CHANGE_COLOR = 'CHANGE_COLOR';
```

## 3. initialState에 대한 처리

```javascript
function reducer(state, action) {
    if (state === undefined) {
    // initial State 적용
    return {color: 'yellow'};
    }
...
}
>>>
const initialState = {
    color : 'yellow'
}
function reducer(state = initialState, action) {
    ...
}
```

## 4. dispatch또한 생성자 함수로 호출한다.

```javascript
store.dispatch({type: 'CHANGE_COLOR', color: 'red'});
>>> store.dispatch(change_color('red'));
```

---

# redux의 구성요소

## store

```
  store는 리덕스 전체를 구성하는 요소이다.
```

## state

```
  state는 현재 우리가 관리할 state를 뜻한다.
```

## reducer

```
  어떤 액션이 들어왔을 때 일어나는 동작들을 모아둔 것이다.
```
