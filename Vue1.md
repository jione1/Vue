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