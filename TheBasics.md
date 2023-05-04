---
marp: true
---

# The Basics

javascript: 동적 타입만을 제공 => 코드를 실행해야만 어떤 일이 벌어지는지 비로소 확인할 수 있다
typescript: 정적 타입 시스템 => 코드가 실행되기 전에 코드에 대하여 예측한다

## 정적 타입 검사
정적 타입 시스템은 우리가 작성한 프로그램에서 사용된 값들의 형태와 동작을 설명한다. 이 정보를 활용하여 프로그램이 제대로 작동하지 않을 때 우리에게 알려준다. 

## 예외가 아닌 실행 실패
유연성을 희생해야 하겠지만, 겉으로 드러나지 않는 버그를 꽤 많이 잡아냅니다.
: 오타, 호출되지 않은 함수, 기본적인 논리 오류 등
```javascript
const user = {
  name: 'Daniel',
  age: 26,
};
```
```
//javascript:
user.location; //undefined

//typescript:
user.location; 
//Property 'location' does not exist on type'{name:string, age:number;}'.
```

## 프로그래밍 도구로서의 타입
타입 검사기는 우리가 변수 또는 다른 프로퍼티 상의 올바른 프로퍼티에 접근하고 있는지 여부를 검사할 수 있도록 관련 정보들을 가지고 있습니다. 이 정보를 활용하면 타입 검사기는 우리가 사용할 수 있는 프로퍼티를 제안할 수 있게 됩니다. 

## tsc, Typescript 컴파일러
Typescript는 당신을 방해하지 않습니다. 
물론, 시간이 흐름에 따라 좀 더 실수에 방어적으로 대응하고, Typescript가 보다 엄격하게 동작하기를 원할 수도 있습니다. 이 경우 --noEmitOnError 컴파일러 옵션을 사용하면 됩니다. 
```
tsc --noEmitOnError hello.ts
//hello.js가 하나도 수정되지 않는다
```

## 명시적 타입
명시적인 타입 표기를 항상 작성할 필요는 없다. 많은 경우, Typescript는 생략된 타입 정보를 추론할 수 있다.(기본 기능)
타입 시스템이 알아서 올바른 타입을 어떻게든 잘 알아낼 수 있다면 타입 표기를 굳이 적지 않는 것이 가장 좋습니다. 

## 지워진 타입 
타입 표기는 Javascript의 일부가 아니므로, Typescript를 수정 없이 그대로 실행할 수 있는 브라우저나 런타임은 현재 존재하지 않는다. 
이것이 컴파일러가 필요한 이유입니다. 

## 다운레벨링
상위 버전의 ECMAScript를 예전의 또는 하위 버전의 것으로 바꾸는 과정
--target 플래그를 설정하면 보다 최근 버전을 타켓으로 변환을 수행할 수도 있습니다
(타켓 버전의 기본값은 ES3이지만, 현존하는 대다수의 브라우저들은 ES2015를 지원하고 있다.)

## 엄격도
가능하다면, 새로 작성하는 코드에서는 항상 엄격도를 활성화해야 한다. 
CLI 에서 ```--strict ``` 플래그를 설정하거나 tsconfig.json에 ``` "strict":true```를 추가하면 모든 플래그를 동시에 활성화하게 된다. 
두 가지 가장 주요한 옵션: noImplicitAny, strictNullChecks

```noImplicitAny```
활성화 하면 타입이 ```any```로 암묵적으로 추론되는 변수에 대하여 오류를 발생시킨다. 

```strictNullChecks```
```null```과 ```undefined```를 보다 명시적으로 처리한다.

