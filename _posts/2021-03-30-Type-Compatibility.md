---
layout: post
title:  "[TypeScript] Type Compatibility 타입의 호환성"
tags: TypeScript
---


> 이 포스팅은 책 [실전리액트프로그래밍](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788966262670)을 공부하면서 기억이 필요한 부분을 발췌하여 정리한 것입니다. 모든 출처는 해당 책에 있습니다.
 


# 타입 호환성

타입 호환성은 어떤 타입을 다른 타입으로 취급해도 되는지 판단하는 것이다. 정적 타입 언어의 가장 중요한 역할은 타입 호환성을 통해 컴파일 타임에 호환되지 않는 타입을 찾아내는 것에 있다. 어떤 변수가 다른 변수에 할당 가능하기 위해서는 해당 변수의 타입이 다른 쪽 변수의 타입에 할당 가능해야 한다. 
  할당 가능은 다음과 같은 서브타입(subtype)으로 표현되기도 한다.

`타입 A가 타입 B에 할당 가능하다. = 타입 A는 타입 B의 서브타입이다.`

할당 가능을 판단할 때는 타입이 가질 수 있는 값의 집합을 생각하면 이해하기 쉽다. A 타입의 값의 집합이 B 타입 값의 집합에 포함되면 A 타입은 B 타입에 할당 가능하다. 

<br />

## 1. 숫자와 문자열의 타입 호환성

```typescript
function func1(a: number, b: number | string){
  const v1: number | string = a;
  // 변수 v1에 매개변수 a를 할당한다. 할당을 받는 쪽의 타입 집합이 더 크기 때문에 성공   
  const v2: number = b;  //에러 
  // 변수 v2에 매개변수 b를 할당한다. 할당을 받는 쪽보다 할당하는 쪽의 타입 집합이 더 크기 때문에 에러
}
```

```typescript
function func2(a: 1 | 2 ){
  const v1: 1 | 3 = a; // 에러
  // 할당을 받는 쪽의 타입 1 | 3는 할당하는 쪽의 타입 1 | 2으로부터 할당 가능하지 않기 때문에 에러
  const v2: 1 | 2 | 3 = a; 
  // 할당 받는 쪽의 타입 1 | 2 | 3은 할당하는 쪽의 타입 1 | 2로부터 할당 가능하기 때문에 성공  
}
```
<br />


## 2. 인터페이스의 타입 호환성 

다른 정적 타입 언어와 달리 타입스크립트에서는 값 자체의 타입보다는 값이 가진 내부 구조에 기반해서 타입 호환성을 검사한다.(`덕타이핑` 또는 `구조적 타이핑`이라 부른다.) 타입스크립트가 구조적 타이핑을 도입한 이유는 동적 타입언어인 자바스크립트를 기반으로 하기 때문이다.

인터페이스 A가 인터페이스 B로 할당 가능하려면 다음 조건을 만족해야한다.
- B(할당받는 대상)에 있는 모든 필수 속성의 이름이 A(할당하는 대상)에도 존재해야한다.
- 같은 속성 이름에 대해, A(할당하는 대상)의 속성이 B의 속성(할당받는 대상)에 할당 가능해야한다.

코드를 보면서 살펴보자.

```typescript
interface Person {
  name: string;
  age: number;
}

interface Product {
  name: string;
  age: number
}

const person: Person = { name: 'sori', age: 10 };
const product: Product = person;
```

Person과 Product는 모든 속성 이름과 타입이 같다. 타입 이름은 다르지만 내부구조가 같기 때문에 Person과 Product는 서로 할당이 가능하다.
만약 Person에 age 속성이 없다면 할당받는 대상의 타입 집합(Product)보다 할당하는 대상의 타입 집합(Person)이 더 작아지기 때문에 Person은 Product에 할당 가능하지 않다. 속성이 많을 수록 타입에 더 많은 제약을 가하는 것이고, 이는 해당 타입의 값의 집합이 작아지는 것을 의미한다. 

<br />


## 추가 속성과 유니온 타입이 타입 호환성에 미치는 영향

추가 속성과 유니온 타입은 타입 호환성에 영향을 미친다. 추가 속성이 있으면 값의 집합은 더 작아진다. (위에서 설명함) 반대로, 유니온 타입이 있으면 값의 집합은 더 커진다.
  다음은 Person에 속성을 추가하고, Product의 age 속성을 유니온 타입으로 변경한 코드다.

```typescript
interface Person {
  name: string;
  age: number;
  gender: string;
}

interface Product {
  name: string;
  age: number | string;
}

const person: Person = { name: 'sori', age: 10, gender: 'Female' };
const product: Product = person;
```  

person에는 추가 속성이 있어서 값의 집합이 작아졌고, product는 유니온 타입을 적용하여 속성 타입의 범위가 넓어졌다. 그래서 person(할당하는 대상)을 product(할당받는 대상)에 할당할 수 있다. person에는 product에 없는 gender라는 속성이 있지만 상관없다. **할당 가능성을 따질 때엔 할당을 받는 쪽 타입만이 중요하다.**

<br />

## 3. 함수의 타입 호환성

함수는 호출하는 시점에 문제가 없어야 할당 가능하다. 다음은 함수 타입 A가 함수 타입 B로 할당 가능하기 위한 조건이다.

- A(할당받는 대상)의 매개변수 개수가 B(할당하는 대상)의 매개변수 개수보다 적어야한다.
- 같은 위치의 매개변수에 대해 B의 매개변수가 A의 매개변수로 할당 가능해야 한다.
- A의 반환값은 B의 반환값으로 할당 가능해야한다.

```typescript
type F1 = (a: number, b: string) => number;
type F2 = (a: number) => number;
type F3 = (a: number) => number | string;

let f1: F1 = (a, b) => 1;
let f2: F2 = a => 1;
let f3: F3 = a => 1;

f1 = f2; 
f2 = f1; //타입에러 (F2보다 f1의 매개변수가 더 많기때문에 에러)
f2 = f3; //타입에러  (F3의 반환타입이 f2의 반환 타입으로 할당가능하지 않기 때문에 에러)
```
함수의 타입 호환성은 호출하는 쪽에서 생각하면 이해하는 데 도움이 된다.

<br />

## 마무리

타입스크립트에서 타입 호환성 부분은 제대로 이해하지 않고 넘어가면 헷갈리기 쉬운 개념이라고 느껴졌다. 할당 받는 대상을 기준으로 생각하고 타입의 집합이 어느 쪽이 더 큰지 판단하는 연습을 계속 해야겠다.   





