---
title: 명령형(Imperative) 언어와 선언형(Declarative) 언어
excerpt: 명령형 언어와 선언형 언어 비교
tags: [programming paradigm, imperative programming, declarative programming]
comment: true
---

## 명령형 패러다임

**절차적** 또는 **객체 지향적**이 **명령형 패러다임**의 아래 범주에 속해 있는데, 이는 C, C++, C#, PHP, Jave와 Assembly와 같은 언어로부터 알 수 있다.

명령형 패러다임은 컴퓨터가 **어떻게 동작하는지**를 말해주는 알고리즘을 생성하는 것을 통해 **프로그램의 상태를 변화시키는 구문들(statements)**을에 초점을 둔다. 이는 하드웨어의 동작과 밀접한 관련이 있다. 일반적으로, 조건문, 반복문 그리고 클래스 상속의 사용이 이를 보여준다.

JavaScript로 작성한 명령형 코드의 예는 다음과 같다:

```javascript
class Number {
    
    constructor (number = 0) {
        this.number = number;
    }
    
    add (x) {
        this.number = this.number + x;
    }
    
}

const myNumber = new Number (5);
myNumber.add (3);
console.log (myNumber.number); // 8
```

---

## 선언형 패러다임

**논리**, **함수형**, **도메인-특화** 언어가 **선언형 패러다임**의 아래 범주에 속해 있는데, 이는 **항상 튜링-완전(Turing-Complete)**을 만족하지는 않는다(항상 일반적인 프로그래밍 언어는 아니다). HTML, XML, CSS, SQL, Prolog, Haskell, F#, Lisp과 같은 언어들이 있다.

선언형 그 프로그램이 **실제로 어떻게 흘러가는지에 대한 묘사 없이 오직 프로그램의 논리**에 초점을 맞춘다. HTML의 예를 들면, 브라우저에 이미지를 표시하기 위해 사용하는 `<img src="./image.jpg" />`는 이 코드 구문이 어떻게 동작하는지에 대해 신경쓰지 않고 이를 사용한다.

**람다 대수(lambda calculus)**에 근간을 둔 **함수형 프로그래밍(functional programming)**은 **튜링-완전**하고 **구문을 피하며(avoid states)** **부작용(side effect)**이 있으며(?), **데이터의 변화(mutation of data)**가 있어야 한다. 이를 통해, **구문(statement)**과 **비교 함수(evaluation function)** 없이 표현이 가능하다. 또한, 반복문이나 항상 같은 값을 반환하는 함수의 사용이 있어서는 안된다.

JavaScript로 작성한 선언형 코드의 예는 다음과 같다:

```javascript
const sum = a => b => a + b;
console.log (sum (5) (3));
```

JavaScript에서는 **조건문(conditional statement)**이나 **조건 표현(conditional expression)**의 사용을 통해 코드를 세분화할 수 있다. 