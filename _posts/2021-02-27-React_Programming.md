---
layout: post
title: "React Programming"
subtitle: ""
date: 2021-02-27 12:00:00 -0400
background: '/img/posts/01.jpg'
---

이 포스팅은 회원가입 페이지를 제작해보면서 React에 대해 배운 내용을 정리해보기 위해 작성되었습니다. React에 대해 겉핥기를 한 것에 지나지 않고 포스팅 작성에도 서툴러 부족한 부분이 많을 것으로 생각됩니다. 이에 대한 코멘트는 감사히 받겠습니다.
* [나의 git repository](https://github.com/qnbz209/pogomgom-react)

# React?

> 웹(혹은 앱)을 만들기 위해 사용되는 Javascript 라이브러리 프레임워크

Facebook이 만들고, 쓰고있으며, 많은 사람들이 웹 개발을 편히 하기위해 쓰고 있는 Framework이며, 주로 SPA(Single Page Application)의 개발에 사용된다.
* [공식 문서](https://ko.reactjs.org/)

## SPA(Single Page Application)
여러번 서버와의 통신을 통해 페이지를 하나하나 받아오기 보다는 한 페이지 내에서 Javascript로 렌더링을 바꿔가며 서버와의 통신을 최소화하는 방식이다. 이로 인해 Javascript의 사이즈가 늘어나서 초기 렌더링에 시간이 많이 소요된다.

## JSX
* React에서 UI rendering을 편리하게 하기 위해 만든 문법이다.
* JSX 문법은 React Element를 생성하는데에 있어 기본적인 html tag들을 모두 wrapping 해놓았기 때문에 <div>, <h1>, <img> 등도 마음껏 쓸 수 있다.
* [Synatic sugar](https://ko.reactjs.org/docs/jsx-in-depth.html): JSX 역시 Javascript이다.


# React 주요 구성요소

## Component

스스로 상태를 관리하며 재사용이 가능한 React의 구성요소
* [react lifecycle](https://ko.reactjs.org/docs/react-component.html#the-component-lifecycle)

## State
* 어떤 프로그램, 혹은 어떤 객체는 항상 state에 의해 결과가 달라지며, 다르게 할 수도 있다.
* State는 모델(데이터)이 될 수도 있고(MVC 패턴에서), store라고 불리기도 하고(redux 패턴에서), 프로그램의 어떤 시점을 정의하는 대상이 되기도 한다.
* State는 "현재 state"와 "state를 바꾸는 event", 그리고 "event에 의해 변경된 newState", "그로 인해 변경된 결과"를 포함한 개념이다.
* 모든 Component는 state를 가지고 있고, 이 state에 의해 보이는 결과물이 결정된다.
* LifeCycle이 돌면서 state가 변경되면 새 state에 걸맞는 결과물을 보여주기위해 Component는 다시 rendering 된다.

### Props
* state가 내부 요인이라면, props는 외부 요인 즉, 어떤 Componet에 의해 주입되어서 영향을 미치는 요인이다.
* 비슷한 Component를 여러개 만들지 않아도 되어 확장성을 갖게 해준다.
* Component가 다른 Component에 영향을 미칠 수 있게 만드는 props는 항상 아래 방향으로만 전달 가능하다는 점이다.

## Coding
상기 배운 React의 개념을 기반으로 회원가입 페이지에 필수로 존재하거나, 의례 존재하는 Component들을 선언 및 기능을 추가해주었다.
* 아이디 입력란: 입력란의 경우 모두 label을 이용하여 rendering 되도록 선언해주었다. 
* 중복확인 버튼: fetch를 이용해 해당 아이디가 존재하는 지 확인 및 유효성에 대한 state를 update 해줄 수 있도록 한다.
* 비밀번호 입력란: 숫자와 영문의 조합으로 8자 이상이 되어야 한다.
* 비밀번호 확인 입력란: 앞서 입력한 비밀번호와 같아야 한다.
* 이름 임력란: 공란인 경우를 제외하면 유효성이 false가 되는 경우는 없다.
* 전화번호 입력란: 오직 숫자로만 입력을 받도록 한다.
* 이메일 입력란: 이메일 형식에 알맞는 입력을 받아야 한다.
* 광고 수신 동의 버튼: input type="radio"를 이용해 "동의"와 "미동의"가 동시에 활성화되지 않도록 한다.
* 가입 버튼: 위의 모든 입력이 유효할 때에 fetch를 이용해 서버에 필요한 내용을 제출 및 회원가입 완료 페이지로 넘어가도록 한다.


# React-Router
SPA 개발을 위해서는 필요한 페이지마다 새로운 네트워크 통신을 하는 것보단, 최소한의 re-rendering으로 html, Javascript 내에서 조작하는 것이 옳다.
다만 각 페이지마다 다른 링크를 가지는 것이 페이지 변화를 알기에 좋기 때문에 페이지마다 적절한 링크를 부여하도록 해야 하며, 이를 지원하는 것이 react-router라는 모듈이다.
* React-Router는 브라우저에 입력된 링크 path 별로 패턴매칭을 해 그 케이스에 맞는 component들을 보여준다.
* 이 때 Router를 통한 링크간 이동은 페이지를 모두 re-rendering 하는것이 아니다. 

## Coding
상기 배운 React-Router를 이용해 초기 페이지, 가입 페이지, 가입 완료 페이지와 해당 path를 설정해주었다. 
```
<BrowserRouter>
    <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/signup" component={Signup} />
        <Route path="/success" component={Success} />
    </Switch>
</BrowserRouter>
```
* 페이지 간의 이동은 Link to="path"를 이용해 구현 가능하다.


# Redux
Redux란 Component들끼리 소통할 수 있게 하는 Global storage이다.
* 지금 제작하는 회원가입 페이지의 경우에는 해당되지 않지만 실제 개발에서는 여러 페이지가 생기고 정말 많은 Component들이 생긴다.
* Tree 기준으로 가장 하위에 있는 Component에서 다른 페이지 Component의 하위 Component에 영향을 끼치고 싶다면 redux 없이는 코드가 엄청 복잡해질 것이다.
* [공식 문서](https://ko.redux.js.org/introduction/getting-started/)

## Coding
* Redux에서 저장할 내용을 다음 가입 완료 페이지에 넘길 아이디, 이름으로 정하고 이를 initialState에 지정한다.
* 가입 버튼을 누를 시에 회원가입 페이지에 state로 저장되어 있는 아이디와 이름을 Redux에 저장할 함수를 선언한다.
* Redux를 관리하는 디렉토리에서 index.jsx를 아래와 같이 작성해 export할 수 있다.

```
import { combineReducers } from 'redux';
import reducer from './reducer';
const rootReducer = combineReducers({
    reducer
});
export default rootReducer; 
```

* index.js에서 아래와 같이 사용해 Redux를 연결해준다.

```
const store = createStore(rootReducer, composeWithDevTools());
<Provider store={store}>
    <React.StrictMode>
        <App />
    </React.StrictMode>
</Provider>
```

* mapStateToProps를 이용해 Redux에 저장된 state를 참고하도록 할 수 있으며, mapDispatchToProps를 이용해 Redux에 값을 update하도록 선언한 함수를 호출할 수 있다.


# Hook
Functional Component를 사용할 수 있게하는 React의 API
* [공식 문서](https://ko.reactjs.org/docs/hooks-intro.html)

## Why?
* Component를 감싸는 Wrapping Component(connect, withRouter)의 경우 순수한 component만 있는 component tree 사이사이에 끼어들어 진정한 component 관계를 보기 어렵게 만든다. -> Custom Hook
* 관심사의 분리라는 개념에서 접근해 공통된 로직을 함수로 분리해서 import해서 쓰거나 어떤 feature에 대한 로직을 한 곳에 모아둘 수 있게 한다. -> [useEffect()](https://ko.reactjs.org/docs/hooks-effect.html)
* Class기반 component개발을 하기 위해서는 Class가 가지고 있는 this가 뭘 가리키고 있는지, class와 instance, state와 props에 대해 알아야 했고, 함수를 등록하기 위해 항상 bind 하기도 해야하는 반면, 더 직관적인, 설명적인 Function만 사용한다면, 더 쉽게 개발 할 수 있을 것이다.
* [ref.](https://reactjs.org/docs/hooks-intro.html#motivation)

## Coding
Hook으로의 리팩토링이 이미 작성된 코드에 대해 반드시 이루어져야 하는 작업은 아니지만, functional component로의 React 작성법에 대해 배우는 과정을 진행하였다.
* return 에 rendering될 내용을 작성한다.
* this.state, this.setState() >> useState()

### for react-router
* useHistory()를 이용해 현재 path를 기억하고, push를 통해 이에 path를 더함으로써 페이지 이동을 할 수 있다.

### for Redux
* mapStateToProps >> useSelector()
* mapDispatchToProps >> useDispatch()

### Memoization
데이터의 변경이 있어 렌더링이 필요한 경우에만 렌더링을 진행해 비용을 절감시키는 기술
* useMemo(), useCallback()


# TypeScript

> TypeScript is a **superset** of JavaScript

Type scrict한 Javascript로 이해했으며, type에 대한 정의가 이루어지다보니 협엽 중에 함수와 인자의 사용법에 대한 공유가 더 용이하게 될 것이라 느꼈다.

## Types
* boolean
* number
* bigInt
* string
* array
* tuple
* enum
* any
* void
* null, undefined

## Interface
코드에서 사용되는 object의 type 정의가 필요한 경우에 사용된다. (나는 구조체와 같은 개념이라 이해했다.)

```
interface Person {
  firstName: string;
  lastName: string;
}
function greeter(person: Person) {
  return "Hello, " + person.firstName + " " + person.lastName;
}
let user = { firstName: "Jane", lastName: "User" };
console.log(greeter(user));
```

## Coding
상기 배운 내용을 바탕으로 해 아래의 순서로 리팩토링을 진행하였다.
* TypeScript 패키지를 다운로드 받는다.

```
npm install --save typescript @types/패키지명
```

* .jsx를 .tsx, .js를 .tsx로 수정한다.
* Component에 있는 function, state, props의 type들을 정리해준다.

# 마치며
CSS를 이용해 스타일을 적용하는 등의 구현을 모두 해보지는 못하였고 수박 겉핥기에 지나지 않을 정도로 진행을 했지만 이전에 전혀 알지 못했던 웹 브라우저의 구현 방식에 대해 배울 수 있는 좋은 시간이었습니다. 주말마다 시간을 내어 가르침을 준 류인아 선생님께 감사를 드립니다.