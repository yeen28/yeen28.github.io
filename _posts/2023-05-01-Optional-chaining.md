---
layout: post
title: Optional chaining
author: yeeun
category: ['Study']
tags: Optional_chaining
keywords: 
usemathjax: false
permalink: 
---

## optional chaining (?.)

<br/>

#### 옵셔널 체이닝이 필요한 이유
존재하지 않는 요소에 접근할 때 에러가 발생할 수 있습니다.<br/>
옵셔널 체이닝이 등장하기 이전에는 비교문을 사용하여 존재하는 요소인지 확인하였습니다. 하지만 이 방법은 코드가 길어진다는 단점이 존재합니다.<br/>

<code>?.</code>은 <code>?.</code> 앞의 평가 대상이 undefined나 null이면 평가를 멈추고 <strong><u><code>undefied</code></u></strong>를 반환합니다.

<br/>

```javascript
const adventurer = {
  name: 'Alice',
  cat: {
    name: 'Dinah'
  }
};
```
```javascript
const dogName = adventurer.dog?.name;
console.log(dogName);
// Expected output: undefined
```
<code>adventurer</code>에는 dog가 존재하지 않습니다.<br/>
그래서 <code>adventurer.dog</code>는 <strong><code>undefined</code></strong>이기 때문에 <code>dogName</code>은 <code>undefined</code>입니다.<br/>

위의 코드를 optional chaining(?.)없이 사용하면 다음 코드와 같습니다.
```javascript
const dogName =
    (adventurer.dog === null || adventurer.dog === undefined) ?
        undefined :
        adventurer.dog.name;
```

<br/>

#### 주의사항
<code>?.</code>앞의 변수는 꼭 선언되어 있어야 합니다.<br/>
<code>let</code>이나 <code>const</code>, <code>var</code>를 사용해 선언이 완료된 변수를 대상으로만 동작합니다.

<code>?.</code>은 읽기나 삭제하기에는 사용할 수 있지만 쓰기에는 사용할 수 없습니다.
```javascript
user?.name = "Violet"; // SyntaxError: Invalid left-hand side in assignment
```

<hr>

#### 참고
<ul><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining">https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining</a></ul>
<ul><a href="https://ko.javascript.info/optional-chaining">https://ko.javascript.info/optional-chaining</a></ul>
