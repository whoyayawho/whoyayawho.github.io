---
title: "[Web] 리액트 state 관리 (Redux, Redux Toolkit)"

sidebar:
    nav: "web"
---

<br/>

# 1. Redux toolkit 라이브러리 설치

## (1) 설치 

> 설치 참고 : [https://redux-toolkit.js.org/](https://redux-toolkit.js.org/)
{: .notice--info}

리액트의 state 사용을 편하게 하기 위해 Redux 개선 버전인 Redux toolkit을 설치한다.

리액트 프로젝트 폴더 안에서 명령어를 실행한다.

```bash
$ npm install @reduxjs/toolkit react-redux
```

## (2) 셋팅

### a. `src/store.js` 파일 생성

`src/store.js` 파일을 만들어 아래와 같이 작성한다.

이 파일을 통해 state 들을 보관한다.

```javascript
import { configureStore } from '@reduxjs/toolkit'

export default configureStore({
  reducer: { }
}) 
```

### b. `src/index.js` 파일 수정

`src/index.js` 파일을 아래와 같이 수정한다.

```javascript
import { Provider } from "react-redux";
import store from './store.js'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <BrowserRouter>
        <App/>
      </BrowserRouter>
    </Provider>
  </React.StrictMode>
); 
```

- `import { Provider } from "react-redux";` 추가
- `import store from './store.js'` 추가
- `<Provider store={store}>`, `</Provider>`으로 `<App />` 부분을 감싸기

<br/>


# 2. state 보관 

`createSlice( )`으로 state를 만들고, `configureStore( )`으로 등록한다.

```javascript
import { configureStore, createSlice } from '@reduxjs/toolkit'

let user = createSlice({
  name : 'user',
  initialState : 'kim'
})

let cart = createSlice({
  name : 'cart',
  initialState : [
    {id : 0, name : 'White and Black', count : 2},
    {id : 2, name : 'Grey Yordan', count : 1}
  ]
})

export default configureStore({
  reducer: {
    user : user.reducer,
    cart : cart.reducer
  }
}) 
```

<br/>


# 3. state 불러오기

`useSelector()`를 이용하여 state를 불러온다.

```javascript
import { useSelector } from "react-redux"

function Cart(){
  let a = useSelector((state) => state.user ) 

  let state = useSelector((state) => state)

  state.cart.map((a, i)=>
    <tr key={i}>
      <td>1</td>
      <td>{state.cart[i].name}</td>
      <td>{state.cart[i].count}</td>
      <td>안녕</td>
    </tr>
  )

  return (생략)
}
```

<br/>


# 4. state 변경

## (1) state 수정 함수 생성

`store.js`에서 `reducers:{}` 안에 state 수정 함수를 만든다.

`store.js` 맨 아래에 `export let { changeName } = user.actions`을 추가한다.

`slice이름.actions`으로 적으면 state 변경 함수가 모두 변수에 저장되어 export 된다.

```javascript
let user = createSlice({
  name : 'user',
  initialState : 'kim',
  reducers : {
    changeName(state){
      return 'john ' + state
    }
  }
}) 

export let { changeName } = user.actions
```

## (2) state 수정 함수 사용

`dispatch( state변경함수() )`처럼 감싸서 실행하면 state 변경 함수가 실행된다. 

```javascript
import { useDispatch, useSelector } from "react-redux"
import { changeName } from "./../store.js"

(생략) 

<button onClick={()=>{
  dispatch(changeName())
}}>버튼임</button> 
```

## (3) 변경함수 파라미터 

함수 파라미터자리에 넣은 값을 `action.payload` 처럼 불러와 사용한다.

`action.type`은 state 변경함수 이름

`action.payload`은 파라미터

```javascript
let user = createSlice({
  name : 'user',
  initialState : {name : 'kim', age : 20},
  reducers : {
    increase(state, action){
      state.age += action.payload
    }
  }
}) 
```

## (4) state가 array/object인 경우

state가 array/object인 경우 아래와 같이 state를 직접 수정이 가능하다.

그래서 문자나 숫자 하나만 필요한 경우에도 array/object를 사용하기도 한다.

```javascript
let user = createSlice({
  name : 'user',
  initialState : {name : 'kim', age : 20},
  reducers : {
    changeName(state){
      state.name = 'park'
    }
  }
}) 
```

<br/>