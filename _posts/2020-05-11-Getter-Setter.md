---
layout: post
title: '[JavaScript] getter와 setter 메서드 똑똑하게 사용하기'
tags: 'JavaScript'
---

## 프로퍼티 getter와 Setter

자바스크립트에서 프로퍼티는 크게 **데이터 프로퍼티(data property)**와 **접근자 프로퍼티(accessor property)**라는 두가지 종류로 나뉜다. <br> 데이터 프로퍼티는 그동안 일반적으로 사용한 프로퍼티를 말하기 때문에 생략하고,
이번 포스팅에서 새롭게 정리해볼 주제는 접근자 프로퍼티(accessor property)이다. <br>

접근자 프로퍼티의 본질은 함수인데, 값을 획득(get)하고 설정(set)하는 역할을 담당한다. 객체에서 함수로 담겨있는 프로퍼티기 때문에 메서드라고 부른다. 객체 리터럴 안에서 getter와 setter는 `get`과 `set`으로 나타낼 수 있다.

<!-- - getter는 객체의 특정 프로퍼티값을 가져오도록 하기 위한 메서드이다.
- setter는 객체의 특정 프로퍼티값을 설정하기 위한 메서드이다. -->

```javascript
let obj = {
  get propName() {
    // getter, obj.propName을 실행할 때 실행되는 코드
  },

  set propName(value) {
    // setter, obj.propNAme = value를 실행할 때 실행되는 코드
  },
}
```

getter 메서드는 `obj.propName`을 사용해 프로퍼티를 읽으려고 할 때 실행되고, setter 메서드는 `obj.propName = value`로 프로퍼티에 값을 할당하려 할 때 실행된다.

아래의 코드로 user라는 객체를 만들어서 이해를 해보자.

```javascript
let user = {
  name: 'John',
  surname: 'Mayer',
}
```

이 객체에 fullName이라는 프로퍼티를 추가해 fullName이 John Mayer가 되도록 해보려면 어떻게 할까? <br>
getter와 setter를 이용해서 만들어보자.

```javascript
let user = {
  name: "John",
  surname: "Mayer",
};
get fullName() {
    return `${this.name} ${this.surname}`;
  }
};

console.log(user.fullName) // John Mayer
user.fullName = 'Test' // Error
```

getter 같은 접근자 프로퍼티를 사용하면, 일반 프로퍼티에서 값에 접근하는 것처럼 프로퍼티 값을 얻을 수 있다. <br>
하지만 이때 `user.fullName = 'Test'`를 사용해서 새로운 값을 할당하려고 하면 에러가 발생하는데, <br>
그 이유는 값을 조회하는 getter 메서드만 있는데 값을 수정하려고 시도했기 때문이다. 이때는 setter 메서드를 추가해서 값의 변경이 가능하게 만들어줘야한다.

```javascript
let user = {
  name: "John",
  surname: "Mayer",

get fullName() {
    return `${this.name} ${this.surname}`;
  }

set fullName(value){
    [this.name, this.surname ] = value.split(" ");
    //공백을 기준으로 성과 이름 분리하여 새로운 값 할당
 }
};

user.fullName = 'Anne Marie';
console.log(user.name); //Anne
console.log)(user.surname); //Marie
```

이렇게 getter와 setter 메서드를 이용하면 객체에 fullName 이라는 가상의 프로퍼티가 생긴다. <br>
가상의 프로퍼티는 읽고 쓸 수는 있지만 실제로 존재하지 않는다.

**중요: getter와 setter 메서드는 호출할때 user.fullName = 'Anne Marie' 처럼 괄호를 사용하지 않는다. <br>문법적으로 프로퍼티의 값을 재할당하는 것처럼 보인다는걸 기억하자.**

예시를 더 보면서 익숙하게 해보자. setter 메서드를 이용하면 입력된 값의 데이터 타입을 체크하고 원하는 데이터타입이 입력되었을때만 값이 갱신되게 하는 코드를 만들 수 있다.

```javascript
const person = {
  _age: 37,
  set age(newAge) {
    if (typeof newAge === 'number') {
      this._age = newAge
    } else {
      console.log('You must assign a number to age.')
    }
  },
}

person.age = 40 //40
person.age = '40' //'You must assign a number to age.'
```

<br>

## getter와 setter 똑똑하게 활용하기

getter와 setter를 실제 프로퍼티 값을 감싸는 래퍼(wrapper)처럼 사용한다면, 실제 프로퍼티 값을 직접적으로 수정하지 않고도 원하는대로 값을 통제할 수 있다.<br>
아래 예시를 보자.

```javascript
let user = {
  get name() {
    return this._name
  },
  set name(value) {
    if (value.length < 4) {
      alert(
        '입력하신 값이 너무 짧습니다. 네글자 이상으로 구성된 이름을 입력하세요.'
      )
      return
    }
    this._name = value
  },
}

user.name = 'Teo' //"입력하신 값이 너무 짧습니다. 네글자 이상으로 구성된 이름을 입력하세요."
```

user의 이름은 \_name에 저장되고, 프로퍼티에 접근하는건 getter와 setter로 이루어진다. <br>
기술적으로는 `user.\_name`을 사용해 이름에 바로 접근할 수 있다. 하지만 밑줄로 시작하는 프로퍼티는 객체 내부에서만 활용하고
외부에서는 건드리지 않는게 관습이다. 이럴때 바로 접근자 프로퍼티를 이용해 간접적으로 값을 다루는 것이 방법이다.

<br>

## 호환성을 위해 사용하기

접근자 프로퍼티는 언제 어느때나 getter와 setter를 이용해서 데이터 프로퍼티의 행동과 값을 원하는대로 조정할 수 있다는 점에서 유용하다.

```javascript
function User(name, age) {
  this.name = name
  this.age = age
}

let john = new User('John', 25)
alert(john.age) // 25;
```

그런데 갑자기 코드를 수정할 일이 생겨서 age 대신 birthday라는 프로퍼티를 이용해서 만 나이를 구해야한다고 생각해보자. <br>
생성자 함수를 수정하면 기존 코드 중 age 프로퍼티를 사용하고 있는 코드를 모두 수정해줘야하는데, 시간이 오래걸리고 힘들다.

```javascript
function User(name, birthday) {
  this.name = name
  this.birthday = birthday
}

let john = new User('John', new Date(1992, 6, 1))
```

그래서 기존 코드를 그대로 두면서 똑똑하게 수정을 하는, getter를 이용하는 방법이 있다.

```javascript
function User(name, birthday) {
  this.name = name
  this.birthday = birthday

  Object.defineProperty(this, 'age', {
    get() {
      let todayYear = new Date().getFullYear() //현재의 연도
      return todayYear - this.birthday.getFullYear()
      //현재 연도 - 태어난 연도
    },
  })
}

let john = new User('john', new Date(1992, 6, 1))
alert(john.birthday) // birthday 사용 가능
alert(john, age) // age 도 그대로 사용 가능
```

이렇게 get을 이용해서 값을 더 유연하게 받을 수 있는 객체로 변경했다.

defineProperty()라는 다소 생소한 메서드를 사용해서 프로퍼티를 조작했는데, <br>
이 부분에 대한 추가적인 공부는 참고링크에 달아놓은 자료를 보고 공부해야겠다.

<br>
<br>
<br>
<br>

_이 포스팅은 [모던자바스크립트 튜토리얼](https://ko.javascript.info/property-accessors#ref-614)을 학습하고 정리한 내용입니다._
