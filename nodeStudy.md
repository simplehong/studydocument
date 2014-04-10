# Node Study

## 01. NodeJS 소개

> 노드는 자바스크립트로 네트워크 애플리케이션을 작성할 수 있는 플랫폼이다.

#### google의 V8 기반으로 동작한다.

V8 JavaScript Engine
		
V8 is Google's open source JavaScript engine.

V8 is written in C++ and is used in Google Chrome, the open source browser from Google.

V8 implements ECMAScript as specified in ECMA-262, 5th edition, and runs on Windows (XP or newer), Mac OS X (10.5 or newer), and Linux systems that use IA-32, x64, or ARM processors.

V8 can run standalone, or can be embedded into any C++ application.

You can find more information here:

The V8 documentation [page](https://developers.google.com/v8/intro) which includes instructions on [downloading and building V8](https://developers.google.com/v8/build).   
Performance documentation covering the [performance goals](https://developers.google.com/v8/design) of V8, and instructions on how to run the Octane benchmark suite (evolution of the V8 benchmark suite).   
User mailing list: http://groups.google.com/group/v8-users   
The V8 contributor [wiki](http://code.google.com/p/v8/wiki/Contributing) page.

#### CommnJS [참고자료](http://helloworld.naver.com/helloworld/12864)

CommonJS(http://www.commonjs.org/)는 JavaScript를 브라우저에서뿐만 아니라, 서버사이드 애플리케이션이나 데스크톱 애플리케이션에서도 사용하려고 조직한 자발적 워킹 그룹이다. CommonJS의 'Common'은 JavaScript를 브라우저에서만 사용하는 언어가 아닌 일반적인 범용 언어로 사용할 수 있도록 하겠다는 의지를 나타내고 있는 것이라고 이해할 수 있다.


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

+ == vs ===
