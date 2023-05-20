---
layout: post
title: DB 최초 구축 시, 자동으로 데이터 삽입
author: yeeun
category: ['Study']
tags: db-init-data-auto-insert
keywords: 
usemathjax: false
permalink:
visibility: public
---

## **DB 최초 구축 시, 자동으로 데이터 삽입**

<br/>

#### **1. Query가 맞는지 DB 상에서 미리 테스트**
<code>data.sql</code>을 사용해서 <code>insert</code>를 작성하기 때문에 해당 Query가 맞는지 테스트를 해보면 좋습니다.

<br/>

#### **2. Spring Boot resource에 sql 파일 생성**
<code>{프로젝트명}\src\main\resources</code>에 <code>data.sql</code> 파일을 생성합니다.<br/>
<code>data.sql</code>에 최초에 실행시키고 싶은 Query문을 작성합니다.

![img.png](../../../../../assets/img/posts/github_blog_2.png){: width="800"}

<br/>

#### **3. application.yml 수정**
```
spring:
  jpa:
    defer-datasource-initialization: true

  # sql.init.mode=always : 스크립트 동작 설정
  # ALWAYS : 모든 데이터베이스에 sql 스크립트를 동작시킵니다.
  sql:
    init:
      mode: always
```

<br>

**<code>defer-datasource-initialization: true</code>**<br/>
<ul>
    <li>2.5이상의 버전부터 <code>data.sql</code> 스크립트는 Hibernate가 초기화되기 전에 실행된다고 합니다.<br/>
그래서 <code>data.sql</code>을 사용하여 Hibernate에 의해 생성된 스키마를 채우려면 <code>spring.jpa.defer-datasource-initialization</code>을 <code>true</code>로 설정하라고 지시되어 있습니다.</li>
</ul>

<br/>

++ 최초 DB 구축하는 테스트를 위해 <code>application.yml</code>에 <code>ddl-auto=create</code>를 해주면 됩니다.<br/>
<code>ddl-auto=create</code> 설정을 해주면 Database 테이블들을 모두 drop하고 다시 create 해줍니다.<br/>

이렇게 최초 DB 구축 시 원하는 데이터가 잘 삽입되는 것을 확인할 수 있습니다!

<br/>

#### **한글 데이터를 삽입했을 때 한글 깨짐 문제 해결!**

한글 데이터를 삽입할 때 한글이 깨지는 문제가 있었습니다.<br/>
그럴 때는 <code>application.yml</code>에 다음 설정을 해주면 됩니다!
```
spring
  sql
    init
      encoding: UTF-8
```

<hr>

#### 참고
<ul>
    <li><a href="https://velog.io/@jupiter-j/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%EC%8B%A4%ED%96%89-%EC%8B%9C-Database-sql-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%82%BD%EC%9E%85">스프링부트 실행 시, Database sql 데이터 삽입</a></li>
    <li><a href="https://sas-study.tistory.com/354">https://sas-study.tistory.com/354</a></li>
    <li><a href="https://milenote.tistory.com/70">https://milenote.tistory.com/70</a></li>
    <li><a href="https://pasudo123.tistory.com/394">https://pasudo123.tistory.com/394</a></li>
    <li><a href="https://ryeon9445.com/develop/1-springboot/">https://ryeon9445.com/develop/1-springboot/</a></li>
    <li><a href="https://godekdls.github.io/Spring%20Boot/howto.data-initialization/">https://godekdls.github.io/Spring%20Boot/howto.data-initialization/</a></li>
    <li><a href="https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.5-Release-Notes#hibernate-and-datasql">https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.5-Release-Notes#hibernate-and-datasql</a></li>
</ul>
