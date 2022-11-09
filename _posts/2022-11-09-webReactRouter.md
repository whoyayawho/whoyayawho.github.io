---
title: "[Web] 리액트 라우터 (react-router-dom)"

sidebar:
    nav: "web"
---

<br/>

# 1. react-router-dom 라이브러리 설치

## (1) 설치 

> 설치 참고 : [https://reactrouter.com/](https://reactrouter.com/)
{: .notice--info}

리액트 프로젝트 폴더 안에서 아래 명령어를 실행하여 리액트 라우팅을 위한 외부라이브러리를 설치한다. 

```bash
$ npm install react-router-dom@6
```

## (2) 셋팅

`src/index.js` 파일을 아래와 같이 수정한다.

```javascript
import { BrowserRouter } from "react-router-dom";

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
      <BrowserRouter>
        <App/>
      </BrowserRouter>
  </React.StrictMode>
); 
```

<br/>


# 2. 기본 사용법

url 뒤에 `/about` 또는 `/detail` 입력에 따라 다른 페이지를 보여준다.

```javascript
import { Routes, Route, Link } from 'react-router-dom'

function App(){
  return (
    (생략)
    <Routes>
      <Route path="/detail" element={ <div>상세페이지</div> } />
      <Route path="/about" element={ <div>about페이지</div> } />
    </Routes>
  )
}
```

<br/>


# 3. 페이지 이동

`useNavigate()` 함수를 이용하여 페이지를 이동한다.

`useNavigate(-1)`은 뒤로 1번 가기

`useNavigate(2)`은 앞으로 2번 가기

```javascript
function App(){
  let navigate = useNavigate()
  
  return (
    (생략)
    <button onClick={()=>{ navigate('/detail') }}>이동버튼</button>
  )
}
```

<br/>


# 4. 기본 페이지 설정

`<Route path="*">`를 맨 아래에 넣어둔다.

```javascript
<Route path="*" element={ <div>없는페이지</div> } />
```

<br/>


# 5. nested routes

`/about/member`로 접속시 `<About> & <div>멤버들</div>` 을 보여준다.

`/about/location`으로 접속시 `<About> & <div>회사위치</div>` 을 보여준다.

```javascript
<Route path="/about" element={ <About/> } >  
  <Route path="member" element={ <div>멤버들</div> } />
  <Route path="location" element={ <div>회사위치</div> } />
</Route>
```

nested routes안의 element들은 `<Outlet>` 위치에 보여준다.

따라서 `<About/>` 컴포넌트에서 아래와 같이 수정하면 `/about/member`로 접속시 `<Outlet>`자리에 `<div>` 박스들이 보인다.

```javascript
function About(){
  return (
    <div>
      <h4>about페이지</h4>
      <Outlet></Outlet>
    </div>
  )
}
```

<br/>


# 6. URL 파라미터

아래와 같이 `/:url파라미터`를 사용하면 `/detail/0`, `/detail/1`, `/detail/2`와 같이 주소 입력을 하면 `<Detail/>` 컴포넌트를 보여준다.

```javascript
<Route path="/detail/:id" element={ <Detail shoes={shoes}/> }/>
```

그 후에 `useParams()` 함수를 아래와 같이 사용하면 `/detail/숫자`에서 입력한 `숫자` 값이 `id`에 입력된다.

```javascript
import { useParams } from 'react-router-dom'

function Detail(){
  let {id} = useParams();
  console.log(id)
  
  return (
    <div className="container>
      <div className="row">
        <div className="col-md-6 mt-4">
          <h4 className="pt-5">{props.shoes[id].title}</h4>
          <p>{props.shoes[id].content}</p>
          <p>{props.shoes[id].price}원</p>
          <button className="btn btn-danger">주문하기</button>
          </div>
      </div>
    </div>
  )
}
```

<br/>