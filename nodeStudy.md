# Node Study

## 01. NodeJS 소개

> 노드는 서버사이드 자바스크립트 플랫폼이다.

#### google의 V8 기반으로 동작한다.

V8 JavaScript Engine은 Google의 Open source JavaScript 엔진이다. V8은 C++로 작성 되었으며, Google의 오픈소스 브라우저인 Chrome에서 사용되고 있다.

V8은 ECMA-262 스펙(5th Edition)에 명시 된 ECMASCript를 표준으로 구현 되어있으며, Windows(XP or newer), Mac OS X (10.5 or newer), 그리고 Linux systems(IA-32, x64, or ARM processors) 환경에서 동작가능하다.

V8은 standalone, 혹은 C++기반의 어떤 application환경(embedded)에서도 동작가능하다.

V8 참고 자료:
	The V8 Documentation: https://developers.google.com/v8/intro 
	Downloading and building V8: https://developers.google.com/v8/build 
	V8 Performance goals: https://developers.google.com/v8/design 
	User mailing list: http://groups.google.com/group/v8-users 
	The V8 contributor: http://code.google.com/p/v8/wiki/Contributing 

#### CommonJS 표준을 준수한다.
CommonJS( http://www.commonjs.org )는 JavaScript를 브라우저에서뿐만 아니라, 서버사이드 애플리케이션이나 데스크톱 애플리케이션에서도 사용하려고 조직한 자발적 워킹 그룹이다. CommonJS의 'Common'은 JavaScript를 브라우저에서만 사용하는 언어가 아닌 일반적인 범용 언어로 사용할 수 있도록 하겠다는 의지를 나타내고 있는 것이라고 이해할 수 있다.
[CommonJS 참고자료](http://helloworld.naver.com/helloworld/12864)


#### NodeJS 특징

+ 이벤트 루프 기반의 비동기 I/O
		노드의 I/O는 이벤트 루프를 기반으로 비동기로 실행.
        I/O의 결과를 직접 리턴 받지 않고 콜백함수의 파라미터로 전달 받음.

+ 싱글 스레드
		노드의 이벤트 루프는 싱글 스레드, 싱글 스택 사용.
        개발자가 작성한 코드는 싱글 스레드 상에서 동기로 실행 됨.
        그 외 모든 I/O는 비동기로 실행 됨.

+ 자바스크립트
		이벤트 기반 동작 방식에 적합한 프로그래밍 언어.
        현존 최강 자바스크립트 엔진인 크롬의 V8을 그대로 노드에 탑재.

+ 넌블로킹 I/O
		빠르다 - 이벤트 루프 + 넌블로킹 I/O (비동기 + 콜백)
		쉽다 - javascript
		적은메모리 - 이벤트기반으로 멀티스레드 기반 시스템(apache) 보다 적은 메모리 사용

+ NodeJS 단점
		스케일업으로 성능 향상이 되지 않음.
		역사가 짧다.


## 02. NodeJS 프로그래밍 기초

#### REPL (레플, Read-Eval-Print-Loop)

+ 커맨드라인에서 파라미터를 이용한 Node 실행 도구

#### 노드의 Architecture

+ Node's internal architecture
	![node_arch_image](http://orange-coding.net/wp-content/uploads/2013/06/node_standard1.png)
		node library는 자바스크립트로 작성 되었으며, 나머지 영역은 C++로 작성 되었다.

+ Single threaded
		노드는 단 하나의 스레드를 사용한다.
		이는 context switching에 소비되는 자원낭비를 줄일 수 있고, 개발자가 concurrency control에 신경을 써야하는 부담을 없애준다.

+ Non blocking I/O
	![node_event_loop](http://orange-coding.net/wp-content/uploads/2013/06/node_threading_model.png)
    	노드는 논블러킹 I/O기반이다. 이는 기존의 DB calls같은 응답시간이 긴 작업에 해당 스레드가 대기하는 것을 피할 수 있다.
		그런데 노드는 싱글 스레드라고 했잖어?? 스레드 하나가 어떻게 이것을 처리해?? 위의 그림을 보시라.ㅋ
		실제로는 이벤트 루프는 싱글 스레드로 동작하고, 노드 내부적으로 long running jobs을 처리할 worker threads가 존재한다.
		최종적으로 개발자는 이벤트 루프에 해당하는 싱글스레드만 신경쓰면 된다.

+ Event loop
		이벤트 루프는 C로 작성된 Marc Lehmann의 libev 라이브러리를 사용한다.

+ [출처링크](http://orange-coding.net/2013/06/29/xfiles-part-i-learning-how-to-walk)

#### 노드의 Coding style

+ 몇가지 대표적 관례

항목 | 설명 | 예시
:-|:-|:-
들여쓰기 | 공백 2칸 |
세미콜론 | 자바스크립트 관례를 따라 항상 사용 |
작은따옴표 | 문자열 등은 큰따옴표 대신 작은 따옴표 사용 |
중괄호 | 여는 중괄호는 문장과 같은 라인에 작성 | if (true) { ...
변수와 프로퍼티 | 소문자로 시작하는 카멜케이스 사용 |
클래스 | 대문자로 시작하는 카멜케이스 사용 |
콜백함수 | 콜백함수 첫 파라미터는 에러 파라미터로 사용 | callback(err, param)

+ [Felix's Node.js Style Guide](http://nodeguide.com/style.html), [한글링크](http://pismute.github.io/nodeguide.com/style.html)

#### 해결 과제

+ Anonymous function: 익명함수 (function() {}) ();
		function level scoping 특성이 있어 anonymous function 안에서 선언된 모든 변수와 함수들은 밖에 존재하지 않는다.
		사용의 경우 alias나 global object에 종속하기 위해서 사용한다.

		Simply, anonymous functions are used for the reasons of:
		a) code brevity. It often makes sense to use anonymous functions calls in callbacks and event handlers;
		b) scope management. Anonymous functions can be used to create temporary/private scope;
		c) Anonymous function are often handy in closures and recursions.
[참고자료1](http://thoughtsonscripts.blogspot.kr/2012/01/javascript-anonymous-functions.html)
[참고자료2](http://hotdogya.tistory.com/103)

+ \== vs ===

		"==" --> 타입이 다른 비교일때, 타입을 변환하여 비교한다.
		값을 변환하여 비교하는 규칙이 복잡하고 외외구 쉽지 않다고 함.
		"===" --> 동등성 비교에 사용해야 함.

		ex) 아래 예제의 경우 "==="을 사용할 때는 모두 false
		 '' == '0'             // false
		 0 == ''               // true
		 0 == '0'              // true
		 false == 'false'      // false
		 false == '0'          // true
		 false == undefined    // false
		 false == null         // false
		 null == undefined     // true
		 '\t\r\n' == 0         // true

## 03. 노드의 기본 모듈

[Node.js API Reference](http://www.nodejs.org/api/)

#### 전역 객체

+ global
전역적으로 어디서든 접근할 수있는 객체. global 이라는 이름으로 존재하며, 생략가능. 아래 두 코드는 동일
		console.log('메시지');
		global.console.log('메시지');


#### kkk
+ 브라우저의 경우 --> window
+ nodeJS --> global, process
+ debug 옵션
	
#### 해결과제

+ closure
+ octet stream


