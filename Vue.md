# Vue

### Vue는 무엇인가?

MVVM 패턴의 ViewModel 레이어에 해당하는 View 단 라이브러리

=> View와 Model사이에 ViewModel이 위치한다.

> View에서 변화가 있을 때 ViewModel에서 변화를 감지해서 Model에 신호를 보내고  Model에서 변화된 Data에 대해서 View Model을 거쳐서 View에 보냈을 때 화면에 Reactive하게 변화가 일어나게 제어해주는 것이 Vue이다.

### MVVM패턴이란?

> 화면 앞단의 화면 동작 관련 로직과 뒷단의 DB데이터 처리 및 서버 로직을 분리하고, 뒷단에서 넘어온 데이터를 Model에 담아 View로 넘겨주는 중간지점

---

# Vue Instance

- Vue 생성자
- 기존 객체, 화면에서 사용할 옵션(데이터, 속성, 메서드 등)을 포함하여 화면의 단위를 생성

~~~ vue
var vm = new Vue({
	template: ...,
	el: ..., //화면이 그려지는 시작점
	methods: {
		
	},
	created: {

	}
})
~~~

- 확장 재사용 가능 (custom element로 작성하는 것이 더 좋다.)

~~~
var ExVm = Vue.extend({
  template: '<p>Hello {{message}}</p>',
  data: {
    message: 'Vue'
  }
})
~~~

### 라이프싸이클

![Life](C:\Users\user\Desktop\Vue\Life.png)

1. 객체가 생성될 때 초기화 작업 
   1. 데이터 관찰
   2. 템플릿 컴파일
   3. DOM에 객체 연결
   4. 데이터 변경시 DOM 업데이트
2. Method
   1. created
   2. mounted
   3. updated
   4. destroyed

---

# Vue Components

**"화면에 비춰지는 뷰의 단위를 쪼개어 재활용이 가능한 형태로 관리하는 것"**

##### Global Component

```
//컴포넌트 등록하기
Vue.component('Component name', {
  template: '여기에 component 내용을 써주세요'
});
```

##### Local Component

```
new Vue({
  components: {
    'Component name' : 내용
  }
})
```

---

# Vue 컴포넌트 통신

##### 부모와 자식 컴포넌트 관계

![Life](C:\Users\user\Desktop\Vue\Component.png)

- 부모 -> 자식 : props down
- 자식 -> 부모 : events up

##### Props

- 상위에서 하위로 값을 전달할때 사용하는 속성
- 객체, 배열 등 전달 가능
- 모든 컴포넌트는 각 컴포넌트의 자체의 스코프를 갖는다. => props / events로 통신
- **주의** js에서 props변수 명명을 카멜 기법으로 하면 html에서 접근은 케밥 기법(-)으로 해야한다.

##### 같은 레벨의 컴포넌트 간 통신

- 동일한 상위 컴포넌트를 가진 2개의 하위 컴포넌트 간의 직접적인 통신은 불가능하다.
- Child -> Parent -> Child

##### Event Bus - 컴포넌트 간 통신

- 컴포넌트 간의 관계가 없더라도 데이터를 주고 받을 수 있다.

- *단점* : 컴포넌트간의 관계가 명확하지 않다.

- ~~~ vue
  export const eventBus = new Vue();
  new Vue({

  })
  ~~~

---

# Vue 라우터

- SPA : Single Page Application =>해당 화면에 관한 정보를 미리 갖고 있다가 client 내부적으로 라우터를 이용해서 화면을 바로 전환해줄 수 있다.
- 설치 : npm install vue-router
- RootURL/#/{Router name} => #을 제거하고 싶을 때는 mode: 'history'추가



##### Nested Routers

- 여러개의 컴포넌트를 동시에 렌더링 가능
  - 렌더링 : HTML, CSS, JS 파일을 브라우저 사용자가 볼 수 있게끔 그려내는 행위
- 컴포넌트의 구조 : Parent-Child 구조
- 특정 URL에서 1개의 컴포넌트에 여러 개의 하위 컴포넌트를 갖는 것



##### Named Views

- 여러개의 View(컴포넌트)를 동시에 렌더링 한다.
- 특정 URL에서 여러 개의 컴포넌트를 쪼개즌 뷰 단위로 랜더링



##### Vue Resource

npm install vue-resource

---

# Vue Templates

- Vue로 그리는 화면의 요소들, 함수, 데이터 속성을 모두 Templates안에 포함된다.
- render function을 직접 구현하여 사용할 수 있다.

##### Attributes

- HTML  Attributes를 Vue의 변수와 연결할 때는 *v-bind*를 이용

- ~~~ 
  <div v-bind:id="이름"></div>
  ~~~

##### JS Expressions

- {{}}안에 javascript표현식 사용 가능

##### Directives

- v- 접두사를 붙인 attributes

- javascript표현식으로 값을 나타내는게 일반적

- ~~~
  <p v-if="seen">True</p>
  <a v-bind:href="url"></a>
  <a v-on:click="doSomething></a>
  ~~~

##### Filter

- 화면에 표시되는 텍스트의 형식을 편하게 바꿀 수 있도록 고안된 기능

- *|* 을 이용하여 여러 개의 필터를 적용

- ~~~ 
  <!-- new Vuew({});에서 로직 정의-->
  {{message | capitalize}}
  ~~~

---

# Vue 데이터 바인딩

##### 방법

- Interpolation (값 대입)
- Binding Expression (값 연결)
- Directives (디렉티브 사용)

##### Interpolation

- Vue의 가장 기본적인 데이터 바인딩 체계
- Mustache {{ }} 를 따른다.

##### Binding Expression

- {{}}를 이용한 데이터 바인딩을 할때 자바스크립트 표현식을 사용할 수 있다.
- Vue에 내장된 Filter를 {{ }} 안에 사용할 수 있다.
- 여러개 필터 체인 가능

##### Directives

- Vue에 제공하는 특별한 Attributes
- v- 의 접두사를 갖는다.
- 자바스크립트 표현식, filter모두 적용된다.

##### Class Binding

- CSS 스타일링을 위해서 class를 아래 2가지 방법으로 추가 가능
  - class = "{{ className }}"    cf) Vue 2.4 버전부터는 제거된 문법
  - v-bind:class

