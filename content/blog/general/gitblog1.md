---
title: Git 블로그 개설하기!(1)
date: 2020-04-14 17:04:25
category: general
draft: false
---

## To-Do List


1. [정적 사이트 생성기 선택하기(`Gatsby`)](https://sasumpi123.github.io/general/gitblog1/)
2. [선택한 정적 사이트 생성기에서 원하는 theme 다운받기](https://sasumpi123.github.io/general/gitblog1/)
3. [`Git Repository` 생성하기](https://sasumpi123.github.io/general/gitblog2/)
4. [Local 환경에서 Test 해보기](https://sasumpi123.github.io/general/gitblog2/)
5. `Github Action`으로  블로그 배포 자동화하기
6. Posting 시작하기


***      
   
   
      
**정적 사이트 생성기란**?   
먼저 **정적 사이트**란 쉽게말하면 서버에 완성된 `HTML`을 저장해 둔 후 요청에 대해 이 데이터들을 가져와 출력하는것이다.   

그렇다면 **정적 사이트 생성기**는 정적 사이트를 생성해주는 것이라고 생각하면 이해가 쉬울것 같다.   


정적 사이트 생성기도 종류가 여러가지가 있겠지만 필자가 제일 많이 들어본 것들은 **Jekyll**과 **Gatsby**이다    

[Jekyll](https://jekyllrb-ko.github.io/)은 `Ruby` 기반으로 만들어져 있으며   
[Gatsby](https://www.gatsbyjs.org/)는 `React` 기반으로 만들어져 있다.

필자는 본 블로그를 개설할때 `Gatsby` 를 사용하여 블로그를 개설하였다.


`Gatsby`사이트에도 다양한 Theme가 존재하겠지만 필자는   
[JaeYeopHan](https://github.com/JaeYeopHan)님이 커스텀한 [gatsby-starter-bee](https://github.com/JaeYeopHan/gatsby-starter-bee) Theme를 적용하였다.


위 링크를 따라 **JaeYeopHan**님의 **Github**으로 들어가보면 사용법을 자세하게 설명해 주셨지만 제 블로그를 보시는 분들을 위해 천천히 설명하려한다!

먼저 해당 Theme를 다운받으려면 **Git**을 설치해야한다 **Git**은 사용하는 운영체제마다 설치하는 방법이 다르므로 튜토리얼을 보고 설치하는걸 권장한다   

>[Git 설치 튜토리얼](https://www.atlassian.com/git/tutorials/install-git#windows)

설치이후 터미널에서 
```
git version
```
명령어를 사용하여 잘 설치되었는지 확인할 수 있다.

또한 npm모듈을 사용하기 위해 Node.js를 설치한다
>[Node.js 설치](https://nodejs.org/en/)   

마찬가지로 node도 아래 명령어를 사용하여 설치후 버전을 확인할 수 있다.
```
node --version
npm --version
```

위 기본적인 환경설정을 마쳤다면 이제 우리가 사용할 Theme를 다운받아보자   
- 먼저 터미널을 파일들을 다운받고 싶은 경로로 이동한 후,   
```
npx gatsby new my-blog-starter https://github.com/JaeYeopHan/gatsby-starter-bee
```
위 내용을 그대로 터미널에 붙여넣기해준다.
- 만약 자신이 npx를 사용하지 않는다면

```
npm install gatsby-cli
gatsby new my-blog-starter https://github.com/JaeYeopHan/gatsby-starter-bee
```

위 명령어로 다운받아 올 수 있다.   
설치가 모두 끝났다면
```
cd my-blog-starter/
npm start
```
두 명령어를 실행한다면 localhost:8000 에서 다운받아온 Theme의 블로그를 확인할 수 있다!   




## 출처
[JaeYeopHan/gatsby-starter-bee](https://github.com/JaeYeopHan/gatsby-starter-bee)