---
layout: post
title: Design pattern
author: yeeun
category: ['Study']
tags: Design_pattern
keywords: 
usemathjax: false
permalink: 
---

## 디자인 패턴 (Design pattern)

<br/>

#### 디자인 패턴 종류 (23가지)
<ol>
<li>
<strong>Singleton Pattern</strong><br/>
하나의 인스턴스만 존재하도록 보장하기 위해 사용됩니다.<br/>
예를 들면, 데이터베이스 연결과 같이 <u>애플리케이션 전체에서 공유해야 하는 자원을 관리</u>할 때 사용됩니다.
</li>
<li>
<strong>Factory Method Pattern</strong><br/>
객체를 생성하는 인터페이스를 정의하고, 하위 클래스에서 어떤 클래스의 인스턴스를 만들지 결정합니다.<br/>
예를 들면, 전화를 만드는 공장에서 공장에서 객체를 만드는 방법을 추상화하여 다양한 전화 모델을 만들 수 있습니다.
</li>
<li>
<strong>Abstract Factory Pattern</strong><br/>
객체를 생성하는 인터페이스를 정의하고, 서로 관련된 객체를 생성하는 데 사용됩니다.
</li>
<li>
<strong>Builder Pattern</strong><br/>
객체를 생성할 때 복잡한 초기화 과정을 가진 클래스를 처리합니다.
</li>
<li>
<strong>Adapter Pattern</strong><br/>
서로 다른 인터페이스를 가진 두 클래스 사이의 연결을 만듭니다.
</li>
<li>
<strong>Decorator Pattern</strong><br/>
객체에 추가 기능을 동적으로 추가합니다.
</li>
<li>
<strong>Observer Pattern</strong><br/>
객체의 상태 변경을 감지하고 다른 객체에 알립니다.
</li>
<li>
<strong>Strategy Pattern</strong><br/>
알고리즘을 정의하고, 다른 알고리즘으로 대체할 수 있습니다.<br/>
예를 들면, 게임에서 캐릭터의 공격 알고리즘을 변경하는 데 사용됩니다.
</li>
<li>
<strong>Template Method Pattern</strong><br/>
알고리즘의 구조를 정의하고, 하위 클래스에서 구체적인 내용을 구현합니다.
</li>
<li>
<strong>Command Pattern</strong><br/>
요청을 객체의 형태로 캡슐화하고 나중에 실행합니다.
</li>
<li>Prototype Pattern : 객체를 복제할 때 사용되는 디자인 패턴입니다.</li>
<li>Bridge Pattern : 추상화와 구현을 분리합니다.</li>
<li>Composite Pattern : 객체를 트리 구조로 구성합니다.</li>
<li>Facade Pattern : 서브시스템을 노출시키지 않고 복잡한 시스템의 인터페이스를 간단하게 만듭니다.</li>
<li>Flyweight Pattern : 객체의 메모리 사용량을 최소화합니다.</li>
<li>Proxy Pattern : 객체에 대한 대리인이나 자리 표시자 역할을 수행합니다.</li>
<li>Chain of Responsibility Pattern : 객체들이 연결되어 요청을 처리하도록 합니다.</li>
<li>Interpreter Pattern : 언어나 문제를 해석하는 방법을 제공합니다.</li>
<li>Iterator Pattern : 컬렉션의 요소에 순차적으로 접근할 수 있도록 합니다.</li>
<li>Mediator Pattern : 객체 간의 상호작용을 캡슐화합니다.</li>
<li>Memento Pattern : 객체의 상태를 저장하고 복원합니다.</li>
<li>State Pattern : 객체의 상태에 따라 행동을 변경합니다.</li>
<li>Visitor Pattern : 객체에서 수행하는 작업을 캡슐화하고, 다른 객체에서 처리할 수 있습니다.</li>
</ol>

위의 23가지 종류 중 1번째부터 10번째까지가 많이 사용하는 디자인 패턴입니다.

<br/>

#### Singleton Pattern 예제

```java
public class Singleton {
    private static Singleton instance = null;
 
    private Singleton() {
        // Private constructor to prevent instantiation outside the class
    }
 
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

<br/>

#### Strategy Pattern 예제

고객이 나이에 따라 다른 할인 정책을 적용받는 커피 가게 시스템

<span>1. Strategy 인터페이스와 각 전략 클래스 정의</span>

```java
// Strategy 인터페이스
public interface DiscountStrategy {
    double getDiscount(double totalPrice);
}

// 청소년 할인 전략
public class TeenagerDiscountStrategy implements DiscountStrategy {
    @Override
    public double getDiscount(double totalPrice) {
        return totalPrice * 0.2;
    }
}

// 어린이 할인 전략
public class ChildrenDiscountStrategy implements DiscountStrategy {
    @Override
    public double getDiscount(double totalPrice) {
        return totalPrice * 0.1;
    }
}

// 어른 할인 전략
public class AdultDiscountStrategy implements DiscountStrategy {
    @Override
    public double getDiscount(double totalPrice) {
        return 0;
    }
}
```

<span>2. Context 클래스 정의</span>

```java
public class CoffeeStore {
    private DiscountStrategy discountStrategy;
 
    // 나이를 입력받아 해당하는 할인 전략 적용
    public CoffeeStore(int age) {
        if (age < 13) {
            discountStrategy = new ChildrenDiscountStrategy();
        } else if (age < 20) {
            discountStrategy = new TeenagerDiscountStrategy();
        } else {
            discountStrategy = new AdultDiscountStrategy();
        }
    }
 
    public double checkout(double totalPrice) {
        double discountAmount = discountStrategy.getDiscount(totalPrice);
        double result = totalPrice - discountAmount;
        System.out.println("Total: " + totalPrice);
        System.out.println("Discount: " + discountAmount);
        System.out.println("Result: " + result);
        return result;
    }
}
```

<span>3. 전략 패턴을 사용하는 예제 코드</span>

```java
public class Main {
    public static void main(String[] args) {
        CoffeeStore store1 = new CoffeeStore(10);
        store1.checkout(50000); // 어린이 할인
        CoffeeStore store2 = new CoffeeStore(18);
        store2.checkout(50000); // 청소년 할인
        CoffeeStore store3 = new CoffeeStore(25);
        store3.checkout(50000); // 어른 할인
    }
}
```

<hr>

#### 참고
<ul>ChatGPT</ul>
