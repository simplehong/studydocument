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
	
+ 싱글 스레드	
	
+ 자바스크립트
	
+ 넌블로킹 I/O
	
		빠르다 - 이벤트 루프 + 넌블로킹 I/O
		쉽다 - javascript
		적은메모리 - 이벤트기반으로 멀티스레드 기반 시스템(apache) 보다 적은 메모리 사용
			
+ NodeJS 단점

		스케일업으로 성능 향상이 되지 않음.
		역사가 짧다.
		
 

## 02. NodeJS 프로그래밍 기초

#### REPL (레플, Read-Eval-Print-Loop)

커맨드라인에서 파라미터를 이용한 Node 실행

### 해결 과제

+ (function() {}) (); 이런 즉시 실행용 함수의 용도   
[참고자료 : 링크](http://thoughtsonscripts.blogspot.kr/2012/01/javascript-anonymous-functions.html)

		function level scoping 특성이 있어 anonymous function 안에서 선언된 모든 변수와 함수들은 밖에 존재하지 않는다.
		사용의 경우 alias나 global object에 종속하기 위해서 사용한다.
		
		Simply, anonymous functions are used for the reasons of: 
		a) code brevity. It often makes sense to use anonymous functions calls in callbacks and event handlers; 
		b) scope management. Anonymous functions can be used to create temporary/private scope; 
		c) Anonymous function are often handy in closures and recursions.

+ == vs ===

		"==" --> 타입이 다른 비교일때, 타입을 변환하여 비교한다.
		값을 변환하여 비교하는 규칙이 복잡하고 외외구 쉽지 않다고 함.
		"===" --> 동등성 비교에 사용해야 함.
		
		ex) 아래 예제의 경우 "==="을 사용할 때는 모두 false
		 '' == '0'                     	// false
		 0 == ''                       	// true
		 0 == '0'                     	// true
		 false == 'false'         		// false
		 false == '0'               	// true
		 false == undefined  			// false
		 false == null          	   	// false
		 null == undefined    			// true
		 ' \t\r\n ' == 0             	// true