---
title: MERN 스택
date: 2020-04-20 20:04:25
category: mern
draft: false
---

## MERN스택 이란? ##
- M : MongoDB
- E : Express.js   
- R : React.js   
- N : Node.js   

`MERN` 스택은 위 네가지 요소를 사용하여 웹사이트를 개발하는 것을 말한다.   
먼저 위 요소들을 간단하게 살펴보자.


## MongoDB ##
`MongoDB`는 `C++`로 작성된 문서지향 적 데이터베이스이다.   
`MongoDB`는 `NoSQL DB`이다.   
`NoSQL`이라고 해서 `SQL`이 없는 데이터베이스가 아니라, 
사실은 `Not Only SQL` 이다.   
이말인 즉슨, 단순히 기존 `RDBMS`가 가지고 있는 특성들 뿐만 아니라,   
새로운(?) 특성들을 추가적으로 지원한다는 것을 뜻한다.   
또한 기본적으로 자바스크립트 문법을 사용한다.


## Express.js ##
`Express.js`는 웹 프레임워크이다.   
더 쉽게 말하자면 웹을 빠르게 개발할 수 있는 편리한, 다양한 도구들의   
집합체라고 볼 수 있다.


## React,js ##
`React.js` 는 `facebook`에서 제공해주는 `Front-End` 라이브러리이다.   
라이브러리 이므로, 웹을 만드는 데 꼭 필요한 도구들이 모두 기본적으로 제공되지는 않는다.   
하지만 그만큼 가볍다.   
또 `React.js`는 `View`단을 조작하는 라이브러리 이다.

## Node.js ##
`Node.js`는 구글 크롬의 자바스크립트 엔진에 기반해 만들어진 서버 사이드 플랫폼이다.   
또한 `Node.js` 는 `JavaScript`의 `runtime`이다. 즉 `JavaScript Program`을    
실행할 수 있게 도와준다.      
`Node.js`는 이벤트기반, 논블로킹 I/O 모델을 사용해 가볍고 효율적이다.


간단히 살펴본 위 네가지 요소들을 활용하여   
웹에서 간단한 `CRUD`를 구현해보려한다.   

필자는 현재 MacOS를 사용하여 코딩을 하기때문에 Windows에서의   
자세한 환경설정 까지는 확실하게 모르지만 최대한 두가지 환경에서 할 수 있도록 적어보려한다.
