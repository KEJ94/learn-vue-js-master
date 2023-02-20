## 개발 환경 설정

### VSCode 플러그인 설치 및 설정
- Vetur
- Night Owl
- Material Icon Theme
- Live Server 
- ESLint
- Prettier
- Auto Close Tag
- Atom Keymap

index.html 을 우클릭 하고 Open with Live Server 로 로컬서버를 띄울 수 있다.  

### 뷰 개발자 도구 소개 및 실행 방법
Vue.js devtools (크롬 개발자 도구) 를 설치한다.  

## Vue.js 소개

### MVVM 모델에서의 Vue
Vue 는 무엇인가?
MVVM 패턴의 뷰모델(ViewModel) 레이어에 해당하는 화면(View)단 라이브러리  
View(DOM) ---> DOM Listeners(Vue) ---> Model(Plain JavaScript Objects)  
View(DOM) <--- Data Bindings(Vue) <--- Model(Plain Javascript Objects)  

### 기존 웹 개발 방식(HTML, Javascript)
```
var div = document.querySelector('#app');
var str = 'hello world';
div.innetHTML = str;
str = 'hello world!!!'; // 여기까지 작성된 코드는 str 이 초기화 되더라도 화면에 반영되지 않는다.
```

### Reactivity 구현
뷰의 핵심 리액티비티를 재현해보자.
```
// 객체의 동작을 재정의하는 API 다.
Object.defineProperty(대상 객체, 객체의 속성, {
    // 정의할 내용
});
```
```
// 실제 사용
Object.defineProperty(viewModel, 'str', {
    // 속성에 접근했을 때의 동작을 정의
    get: function(){
        consol.log('접근');
    },
    // 속성에 값을 할당했을 때의 동작을 정의
    set: function(newValue){
        console.log('할당', newValue);
        div.innerHTML = newValue;
    }
}); 

viewModel.str // 접근
viewModel.str = 10; // 할당 10 그리고 화면이 바뀌게된다.
```

### Reactivity 코드 라이브러리화 하기
```
var div = document.querySelector('#app');
var viewModel = {};

// Object.defineProperty(대상 객체, 객체의 속성, {
//   // 정의할 내용
// })

(function() {
    function init() {
    Object.defineProperty(viewModel, 'str', {
        // 속성에 접근했을 때의 동작을 정의
        get: function() {
        console.log('접근');
        },
        // 속성에 값을 할당했을 때의 동작을 정의
        set: function(newValue) {
        console.log('할당', newValue);
        render(newValue);
        }
    });
    }

    function render(value) {
    div.innerHTML = value;
    }

    init();
})();    
```


