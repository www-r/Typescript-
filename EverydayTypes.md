---
marp: true
---

# Everyday Types

## 원시 타입: ```string```, ```number```, 그리고 ```boolean```
Javascript에서 typeof 연산자를 사용하였을 때 얻을 수 있는 것과 동일한 이름을 가진다.

- string: 문자열
- number: 숫자 (int, float 존재X)
- boolean: true , false

> String, Number, Boolean 와 같은 (대문자로 시작하는) 타입은 유효한 타입이지만, 코드상에서 이러한 특수 내장 타입을 사용하는 경우는 극히 드뭅니다. 항상 string, number, boolean 타입을 사용하세요.

## 배열
number[] : 숫자열의 배열
Array<nuumber> => 제너릭 (동일한 의미)
> [number]는 전혀 다른 의미를 가진다. => 튜플 타입 
string[] : 문자열의 배열

## ```any```
특정 값으로 인하여 타입 검사 오류가 발생하는 것을 원하지 않을 때 사용할 수 있다. 
코드 상의 특정 라인에 문제가 없다고 Typescript를 안심시킨다는 목적 단지 하나 때문에 긴 타입을 새로 정의하고 싶지 않을 때 유용하게 사용할 수 있다. 

## 변수에 대한 타입 표기
```const```, ```let``` 등을 사용하여 변수를 사용할 때, 변수의 타입을 명시적으로 지정하기위하여 타입 표기를 추가할 수 있으며 이는 선택 사항이다.
가능하다면 자동으로 코드 내의 있는 타입들을 추론하고자 시도한다. 
예를 들어 변수의 타입은 해당 변수의 초깃값의 타입을 바탕으로 추론된다. 
```javascript
let myName: string = "Alice";
```
> Typescript는 "타입을 왼쪽에 쓰는" 식의 표기법을 사용하지 않습니다. 타입 표기는 항상 타입의 대상 뒤쪽에 위치합니다.

## 함수 
### - 매개변수 타입 표기 

함수를 선언할 때, 함수가 허용할 매개변수 타입을 선언하기 위하여 각 매개변수 뒤에 타입을 표기할 수 있다. 매개변수 타입은 매개변수 이름 뒤에 표기한다. 
> 타입을 표기하지 않았더라도, 여전히 Typescript는 올바른 개수의 인자가 전달되었는지 여부를 검사한다. 
```typescript
function greet(name:string){
  console.log("hello," + name.toUpperCase() + "!!");
}
```

### - 반환 타입 표기
반환 타입은 매개변수 목록 뒤에 표기한다. 
함수에 들어있는 return 문을 바탕으로 반환 타입을 
추론하기 때문에 일반적으로 표기하지 않아도 된다. 
```typescript
funtion getFavoriteNumber():number{
  return 26;
}
```

### - 익명 함수 
문맥적 타입 부여
함수가 코드상에서 위치한 곳을 보고 해당 함수가 어떻게 호출될지 알아낼 수 있다면, Typescript는 해당 함수의 매개 변수에 자동으로 타입을 부여합니다. 

## 객체 타입 
객체는 프로퍼티를 가지는 Javacscript 값을 말하는데, 대부분의 경우가 이에 해당한다. 
각 프로퍼티를 구분할 때, ```,``` 또는 ```;```를 사용할 수 있고, 가장 마지막에 위치한 구분자의 표기는 선택 사항이다.

### - 옵셔널 프로퍼티
객체 타입은 일부 또는 모든 프로퍼티 타입을 선택적인 타입(옵셔널)으로 지정할 수 있다. 프로퍼티 이름 뒤에 ```?```를 붙이면 된다. 
```javascript 
function printName(obj:{first:string, last?:string}){...}

//둘 다 OK
printName({first:"Bob"});
printName({first:"Alice", last:"Alisson"});
```
Javascript에서는 존재하지 않는 프로퍼티에 접근하였을 때, 런타임 오류가 발생하지 않고 ```undefined``` 값을 얻게 됩니다. 이 때문에, 옵셔널 프로퍼티를 읽었을 때, 해당 값을 사용하기에 앞서 ```undefined```인지 여부를 확인해야 한다. 
```typescript
function printName(obj: { first: string; last?: string }) {
  console.log(obj.last.toUpperCase());
//'obj.last' is possibly 'undefined'.
// 오류 - `obj.last`의 값이 제공되지 않는다면 프로그램이 멈추게 됩니다!
  if (obj.last !== undefined) {
    // OK
    console.log(obj.last.toUpperCase());
  }
 
  // 최신 JavaScript 문법을 사용하였을 때 또 다른 안전한 코드
  console.log(obj.last?.toUpperCase());
}
```

기존의 타입을 기반으로 다양한 연산자를 사용하여 새로운 타입을 만들 수 있다. 
=>
## 유니언 타입
### 유티언 타입 정의하기
유니언 타입은 서로 다른 두 개 이상의 타입들을 사용하여 만드는 것으로,유니언 타입의 값은 타입 조합에 사용된 타입 중 무엇이든 하나를 타입으로 가질 수 있다. 조합에 사용된 각 타입을 유니언 타입의 멤버라고 부릅니다. 
```typescript
function printId(id: number | string) {
  console.log("Your ID is: " + id);
}
```
### 유니언 타입 사용하기 
해당 유니언 타입의 *모든* 멤버에 대하여 유효한 작업일 때에만 허용된다. 
예를 들어, ```number | string``` 라는 유니언 타입의 경우, ```string``` 타입에만 유요한 메서드는 사용할 수 없다.  
- 이를 해결하려면 코드상에서 유니언을 좁혀야 한다. 
좁히기란 Typescript가 코드 구조를 바탕으로 어떤 값을 보다 구체적은 타입으로 추론할 수 있을 때 발생한다. 
  - 
  1. 예를 들어, Typescript 는 오직 string 값만이 typeof 연산의 결괏값으로 string을 가질 수 있다는 것을 알고 있다. 
  2. 또 다른 예시는 ```Array.isArray``` 와 같은 함수를 사용하는 것이다. 
- 때로는 유니언의 모든 멤버가 무언가 공통점을 가질 수도 있습니다. 
  - 예를 들어, 배열과 문자열은 둘 다 ```slice```메서드를 내장합니다. 

## 타입 별칭
똑같은 타입을 한 번 이상 재사용하거나 또 다른 이름으로 부르고 싶은 경우도 존재한다. 이러한 경우를 위하여 존재한다. 타입을 위한 이름을 제공한다.

## 인터페이스 
인터페이스 선언은 객체 타입을 만드는 또 다른 방법이다. 
타입 별칭과 마찬가지로, 예측된 프로퍼티를 가졌는지 여부만을 따진다. 이처럼, 타입이 가지는 구조와 능력에만 관심을 가진다는 점은 Typescript가 구조적 타입 시스템이라고 불리는 이유이다.

## 타입 별칭과 인터페이스의 차이점
둘은 매우 유사하며, 대부분의 경우 둘 중 하나를 자유롭게 선택하여 사용할 수 있다. ```ìnterface```가 가지는 대부분의 기능은 ```type```에서도 동일하게 사용 가능하다. 
*이 둘의 핵심적인 차이는, 타입은 새 프로퍼티를 추가하도록 개방될 수 없는 반면, 인터페이스의 경우 항상 확장될 수 있다는 점이다.* 

## 타입 단언
타입 표기와 마찬가지로, 타입 단언은 컴파일러에 의하여 제거되며 코드의 런타임 동작에는 영향을 주지 않는다.
꺽쇠괄호를 사용하는 것 또한 가능하다.(동일한 의미) 
```typescript
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;

const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
```

복잡하기는 하지만 유효할 수 있는 강제 변환인 경우, 두 번의 단언을 사용할 수 있다. ```any``` 또는 ```unknown``` 으로 우선 변환한 뒤, 그다음 원하는 타입으로 변환하면 된다. 
```const a = (expr as any) as T;```

## 리터럴 타입
