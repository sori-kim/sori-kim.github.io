---
layout: post
title: '[JavaScript] 객체지향 프로그래밍과 ES6 Class 기초'
tags: 'JavaScript'
---

## OOP(Object Oriented Programming)

## Introduction to Object

객체(object)는 일상을 살면서 우리가 명백하게 볼 수 있고 관찰할 수 있는 대상이다.
자동차, 자전거, 컴퓨터, 토끼, 오리, 강아지, 나무 등등 소프트웨어 세계에서는 구현할 대상을 객체라고 부른다.
그리고 이 객체들은 각각의 특징을 갖고 있다. 이걸 바로 속성(property)라고 부르는데,
같은 객체들은 같은 속성을 공유하지만 그렇다고 해서 속성에 대한 값까지 모두 같은건 아니다.
예를 들어 자동차라는 객체는 바퀴라는 속성을 공유하지만 모든 자동차의 바퀴수가 같지는 않다.

객체지향프로그램은 일상세계의 모습을 그대로 가져와 적용하는데, 프로그램을 객체들로 구성하고
객체들 간에 서로 상호작용이 가능하도록 코드를 작성하는 방법이다. <br>

아래의 dog이라는 객체는 name과 numLeg라는 두가지 속성을 가지고 있고,
이 속성에 접근하는 방법은
`dog.name`
`dog.numLeg` 이다.

```javascript
dog = {
  name : ‘jjang-gu’,
  numLeg: 2
}
```

## 객체의 메서드(method)

객체는 메서드라고 하는 특별한 타입의 속성을 가질 수 있는데 이는 객체의 속성으로 `함수`가 들어갔을때 특별히 부르는 용어이다. 위에서 객체의 속성값을 사용하는것과 마찬가지로 마침표로 불러서 사용한다.

```javascript
let dog = {
  name: 'Spot',
  numLegs: 4,
  sayLegs: function() {
    return 'This dog has 4 legs.'
  },
}

dog.sayLegs()
```

## this 키워드

우리가 만든 객체를 많은 곳에서 재사용하기 쉽게 하기 위해서는 this를 사용한다.
this는 자기가 소속된 객체를 가리킨다.

```javascript
let dog = {
  name: 'Spot',
  numLegs: 4,
  sayLegs: function() {
    return 'This dog has ' + this.numLegs + ' legs.'
  },
}

dog.sayLegs()
//'This dog has 4 legs.'
```

## Class : 객체의 설계도

클래스는 객체지향 프로그래밍의 핵심이다.
클래스는 ES6에서 새로 등장하는 개념인데, 기존에 자바스크립트는 프로토타입 기반의 객체지향 프로그래밍을 했다면 ES6이 도입되면서 새로운 방식이 가능해졌다.

주의할점은 다른 프로그래밍 언어와 달리 class 문법은 단지 문법일 뿐이라는것이다. 클래스 구문은 구문 일 뿐이며 Java, Python, Ruby 등과 같은 언어와 달리 객체 지향 패러다임의 완전한 클래스 기반 구현은 아니다.

클래스는 말하자면 객체의 설계도와 같다. 원하는 구조의 객체 틀을 짜놓고, 비슷한 모양의 객체를 공장처럼 찍어낼 수 있다.
큰 큐모의 객체이거나 비슷한 모양의 객체를 계속 만들어야 한다면,
class라는 설계도를 통해 만들 수 있다.

## class와 생성자 함수 (constructor)

객체(object)의 설계도인 클래스(class)는 기존의 객체를 생성하는 방식과 문법이 비슷한데,
둘의 가장 큰 차이는 constructor 라는 생성자 함수이다.

```javascript
class Car {
constructor(name, price) {
  this.price = price;
  this.department = "선릉지점";
  this.name = name;
  this.salesAmount = 0;
}

applyDiscount(discount) {
  return this.price \* discount;
}

addSales() {
  this.salesAmount++;
 }
}
```

class는 새로운 instance를 생성할 때마다 constructor()메서드를 호출한다.

```javascript
class Car {
  constructor(name, price) {
    this.name = name
    this.price = price
  }
}
```

- Car는 class이름이다. 항상 대문자로 시작하고, CamelCase로 작성해야 한다.
- Car class의 instance를 생성할때마다 constructor메서드가 호출되고,
  constructor()메서드는 name, price 2개의 argument(인자)를 받는다.
- constructor()메서드에 this 키워드를 사용했다. class의 실행범위(context)에서 this는 해당 instance를 의미한다.
- constructor()에서 인자로 넘어오는 name과 price를 사용해 Car instance의 name, price 프로퍼티에 값을 할당했다. 이렇게 클래스 내에서 name, price와 같이 변경 가능한 상태값이자 class내의 컨텍스트에서 어느 곳에서나 사용할 수 있는 변수를 '멤버 변수'라고 부른다.
- 멤버 변수는 'this' 키워드로 접근한다.
<br>

## Instance 인스턴스

인스턴스(Instance)는 class를 통해 생성된 객체이다.
아래와 같이 class로 객체를 생성하는 과정을 '인스턴스화'라고 부른다.

```javascript
class Car {
  constructor(name, price) {
    this.name = name
    this.price = price
  }
}

const morning = new Car('Morning', 2000000)
//인스턴스 생성
```

인스턴스는 class의 property이름과 method를 갖는 객체이다.
인스턴스 마다 모두 다른 property 값을 갖고 있다.

- 인스턴스는 Class 이름에 new를 붙여서 생성한다. new키워드는 constructor() 메서드를 호출하고 새로운 instance를 return해준다.
- 클래스 이름 우측에 () 괄호를 열고 닫고, 내부에는 constructor에서 필요한 정보를 인자로 넘겨준다.

위의 코드는 Car클래스의 instance를 morning이라는 변수에 저장했다. <br>
'Morning'이라는 String과 2000000이라는 Number를 Car 생성자에 넘겨주었고, name, price 프로퍼티에 각자의 값이 할당되었다.
<br>

## class에서의 메서드(Methods)

객체가 프로퍼티 값으로 갖고 있는 함수를 메서드라고 부른다.

Class의 method는 Object(객체)의 문법과 똑같다.
다만 객체는 프로퍼티마다 comma(,)로 구분해줘야 했지만, 클래스는 그렇지 않다.

Car 객체에 changeDepartment 메서드를 추가했다.

```javascript
class Car {
constructor(name, price) {
this.name = name;
this.price = price;
this.department = "선릉지점";
}

applyDiscount(discount) {
return this.price \* discount;
}

changeDepartment(departmentName) {
this.department = departmentName;
 }
}
```

<br>
<br>
<br>
<br>

> 이글은 wecode bootcamp의 자료와 [freecodecamp](https://www.freecodecamp.org/learn/)의 자료를 학습하고 정리한 내용입니다.
