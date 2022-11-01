# Coding Style Convetion
협업정책 중 코딩컨벤션에 대한 프로젝트

## 목차
- 목적
- 용어정의
- 작성패턴
- 예외상황
- 기타주제
- 적용언어
- 항목 유형
  - 코멘트
  - 리터럴
  - 식별자
  - 변수
  - 코드 정렬
  - 연산
  - 조건문
  - 배열
  - 함수
  - 모듈
  - 설정파일

## 목적
서비스 신뢰, 개발 속도, 의사소통, history tracking 등에서 향상.
협업자간 통일된 스타일 작성으로써 개발 수준 상향평준화 기대.
## 용어정의
 - `코딩 컨벤션`: 팀원간 공유 및 인지하고 있으며 커밋에 적용돼있어야할 코딩 스타일 기준.
 - `리팩토링`: 중요도에 밀렸거나 변경된 컨벤션을 적용하지 못한 것.
 - `항목`: 컨벤션 적용 대상.
 - `기타주제`: 명확한 주제로 분류되기 전(다른 협업정책 프
 - `논리상수`: 
   - Object.frozen 인 값
    ``` javascript
    Object.getOwnPropertyDescriptor(Number, 'EPSILON'); //{value: 2.220446049250313e-16, writable: false, enumerable: false}
    ```
   - 전역 스코프 변수 중 상수로 여겨야할 값(ex. 쉘파일, 환경변수 등 raw 데이터) !== const
- `액션`: Conditions(if, else, else if, switch case), Loops(for, while, do while, ), Interruptions(return, break), module exports, 함수 호출

## 작성패턴
 - `항목 추가`: 항목별 내용, 이유 및 근거와 예시가 명확할 경우만 올림. 예시는 실행가능하고 다른 컨벤션을 침범하지 않아야함.
 - `항목별 이유 및 근거`:  질문을 통해서만 받으며 답변으로 달도록함.
 단, 모든채널(온오프라인)에서 이뤄진 질문과 답변 또한 컨벤션에 기입돼야함.
## 예외상황
- 컨벤션 적용은 필수지만 에러초기대응은 제외.
단, 에러대응 완료 즉시 컨벤션누락 후속조치 필수.
- 그 외 필요한 경우(컨벤션 사각지대 발견)
적합한 대응 후 해당부분에 그 의도를 코멘트 후 리뷰 내용에 따라 결정.
- 의문 미해결시 적용보류(애매한 경우 확실해질때까지 적용을 미룸)
## 기타주제
- 하면 좋은 것들 중 반드시 먼저 해야되는 것을 모두 수행하고 맨마지막에 수행한다.(= 절대 하면안되는 것을 염두에 두고 진행한다.)
```
[good case]
Frontend: 디자인 및 기능 전체완료 후 이펙트나 css에 치중
Backend: 레거시 전체 파악(보장) 후 관련 신규기능 추가

[bad case]
Frontend: 디자인 및 기능 전체완료 후 이펙트나 css에 치중
Backend: 레거시 전체 파악(보장) 전 관련 신규기능 추가
```
- (보류)자발적 구글링을 포함한 모든 질문은 공유되며
질문자는 원하는 경우에만 명시한다.
## 적용 언어
- JavaScript
- (보류)TypeScript
## 항목

### 코멘트
- 간결한 종결어미 사용하기
``` javascript
//코드 작성부분. //success, and good
//코드 작성을 하려고하는 부분입니다. //success, and bad
```
- 인라인(in-line) 코멘트는 현재 행의 인접문을 수식한다.
``` javascript
password = '1234'; //위험한 패스워드 //success, and good

function(){ //say nothing //success, and good
}
```
- 블록(multi-line) 코멘트는 두 개 이상의 행을 수식한다. 수식하려는 곳 최상단에 사용한다. 
``` javascript
/* process cycle check: success, and good */
console.log('process 1 done.')
console.log('process 2 done.')
console.log('process 3 done.')
console.log('process all done.')
```
- 기본적으로 한국어로써 기술하고, 코드부분만 영어를 이용하도록 지향한다.
``` javascript
console.log(123); //순서 //success, and good
console.log(123); //order //success, and bad

order = 123;
console.log(order); //순서 //success, and good
console.log(order); //order 가  //success, and bad
```
- 유추가능한 부분을 적지 않는다.
``` javascript
console.log(123); //123을 출력합니다 //success, but bad
console.log(123); //참조 끊긴 이슈 디버깅용(임시) //success, but bad
```
단, 오해소지가 있는 부분은 자세히 기술한다.
``` javascript
custom = {
    log: function(){ //로깅없이 무한루프라서 사용하면 안됨.
        
        while(1){}
    }
}

custom.log(123); //로깅없이 무한루프라서 사용하면 안됨.
```

### 리터럴
- 문자열 구성은 작은 따옴표 ' 기호를 이용한다.
``` javascript
testText = 'test text'; //success, and good
testText = "test text"; //success, and bad
testText = `test text`; //success, and bad
```
단, 템플릿 문자열이 필요한 경우 백틱 ` 기호 이용한 구성을 허용한다.
``` javascript
testText = `${testText}`; //success, and bad
```
- URL 은 caseSensitive 하게 참조 및 지정한다.
``` javascript
'http://localhost' //success, and good
'HTTP://LOCALHOST' //success, and bad
'http://LOCALHOST' //success, and bad
'http://Localhost' //success, and bad
```
### 식별자
- 식별자 표기체계는 영문, 숫자, 언더바 _ 기호로 제한한다.
``` javascript
book = 'ant';  //success, and good
책 = 'ant';  //success, but bad
```

- 식별자는 낙타 대문자(camelCase) 로 표기한다.
``` javascript
favoriteBookName = 'ant';  //success, and good
favorite_book_name = 'ant';  //success, but bad
```

- 식별자는 소문자로만 구성된 단어로 시작한다.
``` javascript
favoriteBookName = 'ant';  //success, and good
FavoriteBookName = 'ant';  //success, but bad
fAVORITEBOOKNAME = 'ant';  //success, but bad
FAVORITEBOOKNAME = 'ant';  //success, but bad
_favoriteBookName = 'ant';  //success, but bad
_FavoriteBookName = 'ant';  //success, but bad
_fAVORITEBOOKNAME = 'ant';  //success, but bad
_FAVORITEBOOKNAME = 'ant';  //success, but bad
```

- 논리상수 표기는 대문자로만 구성하고 SNAKECASE로 구분한다.
``` bash
favoriteBookName=ant  //success, but bad
FavoriteBookName=ant  //success, but bad
fAVORITEBOOKNAME=ant  //success, but bad
FAVORITEBOOKNAME=ant  //success, but bad
FAVORITE_BOOKNAME=ant  //success, and good
_favoriteBookName=ant  //success, but bad
_FavoriteBookName=ant  //success, but bad
_fAVORITEBOOKNAME=ant  //success, but bad
_FAVORITEBOOKNAME=ant  //success, but bad
```

- 최소한 두 글자 이상으로 구성한다.
``` javascript
/* case1: succes, but bad*/
for(i=0; i<10; i++){}

/* case2: succes, and good*/
for(ii=0; ii<10; ii++){}
```
- 자료형을 변수명에 기입금지
``` javascript
arrayNumber = [1,2,3]; //success, but bad
numbers = [1,2,3]; //success, and good
```

- 연관 의미 부여 필요(명칭으로서 result 사용금지)
``` javascript
result = 1+1; //success, but bad
two = 1+1; //success, and good
``` 
- 불리언 변수명은 whether로 prefix.
``` javascript
whetherTruthy = new Boolean(1).valueOf();
```
- 불리언 함수명은 is로 prefix.
``` javascript
function isTruthy(numberOne){
whetherTruthy = new Boolean(numberOne).valueOf();

return whetherTruthy;
}
```

- 연관된 의미를 갖도록 구성한다.
``` javascript
asdfds = 'text'; //success, but bad
number = 'text'; //success, but bad
number = 'text'; //success, but bad
number = 1; //success, and good
```
- 클래스 표기는 식별자 규칙을 따르되, 첫 글자만 대문자로 한다.
``` javascript
class favoriteBookName {};  //success, but bad
class FavoriteBookName {};  //success, and good
class fAVORITEBOOKNAME {};  //success, but bad
class FAVORITEBOOKNAME {};  //success, but bad
class _favoriteBookName {};  //success, but bad
class _FavoriteBookName {};  //success, but bad
class _fAVORITEBOOKNAME {};  //success, but bad
class _FAVORITEBOOKNAME {};  //success, but bad
```

- 변수 선언부는 수신부와 수신파생부, 초기화부와 초기화파생부, 조합부로 구분한다.
``` javascript
/* case1: success, and good*/
function(parameter1, parameter2){
/* 수신부 */
firstParameter = parameter1; 
secondParameter = parameter2;

functionVariable = true; //초기화부

/* 수신파생부 */
unionParameter = firstParameter + secondParameter; 
oppositeUnionParameter = !firstParameter + !secondParameter; 
reverseOppositeUnionParameter = !unionParameter + !oppositeUnionParameter;

oppositeFunctionVariable = !functionVariable; //초기화파생부

firstParameter+oppositeFunctionVariable//조합부
}
```
수신부, 초기화부 순으로 상단 고정이고 이외(수신파생부 및 초기화 파생부)는 context에 맞게 사용한다. 

- 변수선언을 체이닝하지않는다.
``` javascript
const first=1, second=2; //success, but bad

/* success, and good */
const first=1; 
const second=2;
```

- 서버 context 는 strict mode를 적용한다.
``` javascript
//success, but bad
'use strict'; //success, and good
```

- 생략문법(비구조화 할당 제외)을 이용하지 않는다.
(ex. arrow function 의 return, {}, () 이나 parameter 생략)
``` javascript
emptyParameter => emptyParameter //success, but bad
(emptyParameter) => {return emptyParameter;} //success, and good
```
단, 기능적 차이를 갖는 경우 예외(ex. 기본 function 대신 arrow function 사용).

- 명시적 블록 statement를 깨지않는다. if 등에 다 넣어야함.
``` javascript
if(true){ true } //success, and good

if(true) true  //success, and bad
```

### 변수

- 외부 코드 변수는 반드시 const 선언 후 이용하고
불가피한 경우 파생코드 최초 참조부에 출처 코멘트를 남긴다.
``` javascript
/* case1 */
method = require('path/obejct').method; //success, and bad
obejct = require('path/obejct'); //success, and bad

/* case1 */
const method = require('path/obejct').method; //success, and bad
const obejct = require('path/obejct'); //success, and good

/* case2 */
<javascript src = 'https://쿠팡파트너스CDN'></javascript> 
PartnersCoupang  //succes, and bad
PartnersCoupang  //https://쿠팡파트너스CDN //succes, and good
```


### 코드 정렬
- 코드 정렬은
VSCode default formatter 를 이용한다.

`Ctrl + K + F`

### 연산
- 비교연산자(compare operator) 사용시
해당 결과가 truthy일 때를 기준으로하여
좌변을 작은 값 우변을 큰 값으로 둔다.
``` javascript
0 < 1 //true, and good
1 > 0 //true, but bad
``` 
- 매우 크거나 작은 정수 혹은 제한을 두지 않는 정수가 요구되는 경우 safe integer 판별이 포함돼야 한다.
``` javascript
Number.isSafeInteger(Math.pow(2, 53)); //false, and good

Number.isInteger(Math.pow(2, 53)) //true, and bad
```
- safe integer 가 아닌 정수는 사용하지 않는다.
``` javascript
Math.pow(2, 53) === Math.pow(2, 53)+1; //true, and bad
```

- safe integer가 아닌 수끼리 연산을 금지하며 불가피한 경우 앱실론 상수를 이용한다.
``` javascript
((0.1*10) + (0.2*10))/10 === 0.3 //true, but bad
0.1 + 0.2 === 0.3 //false, and bad
Math.abs((0.1+0.2) - 0.3) < Number.EPSILON //true, and good
```
- 실수와 제한을 두지 않는 정수 validation 에는 safe integer 판별이 포함돼야한다.

### 조건문
- 조건절(if, while, do while, switch 등) 에는 수행내용을 코멘트한다.
``` javascript
/* success, but bad */
if(true){ }
/* success, and good */
if(true){ //무언가를 할 것임.

}
```

- 선행조건과 연관된다면 반드시 체이닝한다.
``` javascript
/* success, but bad */
if(true){'첫 항목만 정답입니다.';}
if(true){'다음 항목만 정답입니다.'; }
if(false){'정답이 없습니다'; }

/* success, and good */
if(true){ //첫 항목 정답 알림
'첫 항목만 정답입니다.';

} else if (true){ //다음 항목 정답 알림
'다음 항목만 정답입니다.';

} else { //항목내 정답 없음 알림
'정답이 없습니다.';
}
```

### 배열
- production 의 경우 
- 프론트의 경우 forEach 사용을 지양한다.

### 함수
- 할당없는 function 키워드로써 함수선언하지 않는다.
``` javascript
function doNothing(){} //success, but bad
doNothing = function (){} //success, and good
```

- 화살표 함수는 함수부 맨 앞에서 선언 혹은 할당한다.
``` javascript
/* case1 */
()=>{} //success, and good
doNothing = function (){}

/* case2 */
doNothing = function (){}
()=>{} //success, but bad
```

- 모든 유형별 함수 선언은 const 로써 진행한다.
``` javascript
const doNothing = ()=>{} //success, and good
const doNothing = function (){} //success, and good

let doNothing = ()=>{} //success, but bad
var doNothing = function (){} //success, but bad
```
- 할당없는 IIFE는 사용하지 않는다.
``` javascript
(()=> {return true;}); //success, and bad
alwaysTrue = (()=> {return true;}); //success, and good
```
- 모든 함수 호출은 세미콜론을 생략하지 않는다.
``` javascript
(funtion(){})(); //success, and good
(()=>())(); //success, and good

(funtion(){})() //success, and bad
(()=>())() //success, and bad
```
단, 인자로서 직접이용하는 상황은 배제한다.
``` javascript

```
- 페이지네이션은 20개를 기준으로 한다.

- 함수호출시 유형이 다르다면 줄바꿈을 둔다.
``` javascript
/* case1: success, and good */
console.log('일반 문구');
console.log('일반 문구');

console.warn('경고 문구');

/* case2: success, and bad*/
console.log('일반 문구');
console.log('일반 문구');
console.warn('경고 문구');
``` 

- 커스텀 인스턴스 생성은 반드시 class constructor 용법을 이용한 선언부 절대 function 선언부를 이용하지않도록 한다.
``` javascript
/* case1: success, and bad */
function BornWrong(){}
new BornWrong() 

/* case2: success, and good */
class BornWrong(){}
new BornWrong() 
```

- 모든 함수 호출은 변수(호출함수와 연관된)에 할당한다.
``` javascript
numberOne = isOne(1);
```
    단, 반환 값이 없거나 동일 인자의 재사용이 잘못된 케이스(ex. main()) 는 제외한다.
    (ex. function(){console.log('최초실행 알림 텍스트입니다.')}) //반환값이 없는 함수의 디자인가능여부는 논의대상

- 커스텀 로직 대신 내장 메서드를 이용한다.
``` javascript
/* case1: success, and good*/
3*3*3*3*3 //success, and bad
Math.pow(3,5); //success, and good

/* case1: success, and good */
참가번호목록 = [1,2,3,4,5];
순위목록 = 참가번호목록.map(function(number){
등수 = number + '등';

return 등수;
})

/* case2: success, but bad */
참가번호목록 = [1,2,3,4,5];
순위목록 = [];
ii=0;

for(ii; ii < 참가번호목록.length; ii++){
참가번호 = 참가번호목록[ii];
등수 = 참가번호 + '등';

순위목록.push(등수);
}
```

- 익명함수 선언부에는 목적을 코멘트한다
``` javascript
/* case1: success, and good */
function(){ //say nothing

}

/* case1: success, and bad */
() => {

}
```

- 하나의 함수는 하나의 기능만 갖는다.
``` javascript
/* case1: success, and bad */
function createUserAndDocument(entryOrder){
user.entryOrder = entryOrder;
document.entryOrder = entryOrder;

userAndDocument = {user, document};

return userAndDocument;
}

/* case2: success, and good */
function createUser(entryOrder){
user.entryOrder = entryOrder;

return user;
}
function createDocument(entryOrder){
document.entryOrder = entryOrder;

return document;
}
```
- 재귀용법을 이용하지 않으며, 불필요한경우 꼬리 재귀를 사용하고 이유를 주석으로 단다.

- 포괄적인 validation이 아닌 정확한 validation을 이용한다.
``` javascript
numberOne = 1;

if(isNumber(numberOne) || isString(numberOne)){

numberOne++;
}
```

- PR에서 console 로깅은 에러만 가능하고 빌드시점외에 운영간 발생하는 로깅은 금지한다.
``` javascript
/* case1: success, and good */
//empty

/* case2: success, and bad */
setInterval(function(){

console.log('연결 중...');
}, 1000);

/* case3: success, and not bad */
db.connect(function(){

    console.log('연결 됨');
})
```
### 모듈
- 외부모듈과 커스텀모듈 로드 우선순위를 구분한다.
``` javascript
/* case1: success, and bad */
styles = require('./styles');
react = require('react');

/* case2: success, and bad */
import * as styles from'./styles.js';
import * as react from'react';

/* case3: success, and good */
react = require('react');

styles = require('./styles');

/* case4: success, and good */
import * as react from 'react';

import * as styles from './styles.js';
```

### 액션
모든 컨벤션 충족 후 액션마다 줄바꿈을 둔다.
``` javascript
/* case1: success, and good */
if(true){ //do nothing

}

if(true){//do nothing again

}

console.log('일반 문구');
console.log('일반 문구');

console.warn('경고 문구');

/* case2: success, and bad*/
if(true){ //do nothing
} if(true){//do nothing again
}
console.log('일반 문구');
console.log('일반 문구');
console.warn('경고 문구');
``` 

### 설정파일
- .env* 데이터는 외부 참조 특성을 가져야만한다.
``` shell
HTTP_PORT=80 #success, and good
LOOP_DEFAULT_INDEX=0 #success, and bad
```
- .gitignore 제외목록(노드모듈, 환경변수, OS별 예외파일, 개발환경) 필수
``` bash

```
