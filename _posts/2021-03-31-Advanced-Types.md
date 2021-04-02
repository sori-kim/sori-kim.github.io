---
layout: post
title:  "[TypeScript] 제너릭(Generic)"
tags: TypeScript
---

> 이 포스팅은 책 [실전리액트프로그래밍](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788966262670)을 공부하면서 기억이 필요한 부분을 발췌하여 정리한 것입니다. 모든 출처는 해당 책에 있습니다.
 
제너릭은 타입 정보가 동적으로 결정되는 타입이다. 제너릭을 통해 같은 규칙을 여러 타입에 적용할 수 있기 때문에 타입 코드를 작성할 때 발생할 수 있는 중복 코드를 제거할 수 있다. 
 배열의 초깃값을 입력받아서 배열을 생성하는 함수를 작성한다고 생각해보자. 숫자와 문자열을 위한 함수는 다음과 같이 작성할 수 있다.


 ```typescript
 function makeNumberArray(defaultValue: number, size: number): number[]{
   const arr: number[] = [];
   for (let i = 0; i < size, i++){
     arr.push(defaultValue);
   }
   return arr;
 }

 function makeStringArray(defaultValue: string, size: number): string[]{
   const arr: string[] = [];
   for (let i = 0; i < size; i++){
     arr.push(defaultValue)
   }
   return arr;
 }

 const arr1 = makeNumberArray(1, 10);
 const arr2 = makeStringArray('rosie', 10);
 ```

중복된 코드가 상당히 많아보이는 문제를 제너릭으로 해결할 수 있다. 
제너릭은 <> 기호를 이용해서 정의하며, 이름은 자유롭게 지정할 수 있다.

```typescript

function makeArray<T>(defaultValue: T, size: number): T[] {
  const arr: T[] = [];
  for (let i = 0; i < size; i++){
    arr.push(defaultValue)
  }
  return arr;
}

const arr1 = makeArray<number>(1, 10);
const arr2 = makeArray<string>('rosie', 10);
const arr3 = makeArray(1, 10);
const arr4 = makeArray('rosie', 10);
```

타입 T는 함수를 사용하는 시점에 입력되기 때문에 어떤 타입인지 결정되지 않았다. 함수를 호출할 때 타입 T가 결정된다. 타입 T의 정보는 마찬가지로 <> 기호를 사용해서 전달한다.
makeArray 함수의 첫 번째 매개변수를 알면 타입 T도 알 수 있기 때문에, 호출 시 타입  T의 정보를 명시적으로 전달하지 않아도 된다.

### extends 키워드로 제너릭 타입 제한하기

제너릭은 기본적으로 어떤 타입이든지 입력할 수 있다. 하지만 리액트와 같은 라이브러리의 API는 입력 가능한 값의 범위를 제한한다. 이를 위해 타입스크립트의 제너릭은 타입의 종류를 제한할 수 있는 기능을 제공한다. 
다음과 같이 extends 키워드를 이용하면 제너릭 타입으로 입력할 수 있는 타입의 종류를 제한할 수 있다.

```typescript
function identity<T extends number | string>(p1: T): T {
  return p1;
}

identity(1);
identity('a');
identity([]) //타입에러
```

제너릭 T의 타입을 number | string에 할당가능한 타입으로 제한했다. 배열은 여기에 해당하지 않기 때문에 타입에러가 발생한다.
조금 더 복잡하지만 실용적인 예제를 보자.

```typescript
interface Person {
  name: string;
  age: number;
}

interface Korean extends Person {
  liveInSeoul: boolean;
}

function swapProperty<T extends Person, K extends keyof Person>(
  p1: T, 
  p2: T, 
  name: K
  ): void {
    const temp = p1[name];
    p1[name] = p2[name];
    p2[name] = temp;
  }

  const p1: Korean = {
    name: '김소리',
    age: 60,
    liveInSeoul: true
  };

  const p2: Korean = {
    name: '홍길동',
    age: 31,
    liveInSeoul: false
  };

  swapProperty(p1, p2, 'age'); 
```

Korean 인터페이스는 Person을 확장해서 만들었기 때문에 Korean 타입은 Person 타입에 할당 가능하다.
제너릭 T는 Person에 할당 가능한 타입이어야 하고, 제너릭 K는 Person의 속성 이름이어야 한다. 참고로 keyof 키워드는 인터페이스의 모든 속성 이름을 유니온 타입으로 만들어준다.

extends 조건을 만족하지 않아서 에러가 발생하는 코드도 보자.

```typescript
interface Product {
  name: string;
  price: number;
}

const p1: Product = {
  name: '시계',
  price: 1000
}

const p2: Product = {
  name: '맥북',
  price: 10000
}

swapProperty(p1, p2, 'name')
```

Product는 Person에 할당가능하지 않기 때문에 타입 에러가 발생한다.