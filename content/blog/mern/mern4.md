---
title: MERN 스택(Express.js, MongDB 연결)
date: 2020-04-22 15:04:97
category: mern
draft: false
---

## Node.js와 MongoDB 연결하기
이전 포스트에서 우리가 간단하게 만들었던 서버 코드이다   
하나씩 살펴보고 지나가자

```js{3}
const express = require('express')      // 우리가 npm install 한 express를 가져옴

const app = express()                   // app에 받아온 모듈 저장
const port = process.env.PORT || 3001;  // port 번호 3001 번으로 설정

app.get('/', (req, res, next) => {      // 해당 url로 접속했을때 실행할 행동 정의해줌
    res.send('hello world!');
});

app.listen(port, function () {          // 해당 port번호로 리스닝이 성공했을때 실행될 콜백함수이다.
    console.log('server on! ' + port);
});
```

먼저 `express`라는 변수에 우리가 npm install 한 `express` 모듈을 받아오고   
`app`에 `express`객체를 담아준다.   
`port` 에 3001또는 process.enc.PORT 번호를 주입하고   
해당 포트번호로 리스닝이 성공할시 console에   
**"server on! 3001"** 메세지를 출력한다   
또한 해당 `url`로 접속했을때 웹 페이지에 
**"hello world!"**를 출력해준다.

간단하게 서버를 만들었고 이제 서버에 `MongoDB`를 연결해 보자.
먼저 `server` 폴더 안에 `db` 폴더를 만들고      
`db` 폴더안에 `index.js` 파일을 생성한다.   

```
MERN
└── server
    ├── db
    │   └── index.js
    ├── node_modules
    │   └── ...
    ├── index.js
    ├── package-lock.json
    └── package.json
```
이제 위와같은 구조가 완성되었을 것이다.  
db 폴더의 index.js 파일에 아래 코드를 입력하자.

```js{3}
const mongoose = require('mongoose')        // npm install 한 mongoose 을 가져옴

mongoose.set('useFindAndModify', false);    // mongoose가 제공하는 함수를 사용하기 위한 set
mongoose.set('useCreateIndex', true);       // mongoose 필요없는 경고 메세지 제거
mongoose.set('useUnifiedTopology', true);   // mongoose 필요없는 경고 메세지 제거

mongoose
    .connect('mongodb://127.0.0.1:27017/addr', { useNewUrlParser: true })
    .catch(e => {
        console.error('Connection error', e.message)
    })
                                            // mongoose 를 사용하여 MongoDB에 
                                            // 연결하고 addr이라는 Collection과 연결
                                            // 에러 발생시 콘솔에 에러 출력
const db = mongoose.connection
                                            // db객체에 MongoDB연결 정보 담가

module.exports = db                         // 모듈 생성
```

위 코드에서 눈여겨 봐야할 부분은 `mongoose.connect` 와 `module.exports` 이다.    
`mongoose.connect`에 연결할 `MongoDB` 포트번호와 생성할 DB이름을 입력하면      
`MongoDB`가 켜져있을때 `mongoose`가 알아서 연결해준다.   
또한 `.catch`를 통해 연결 실패했을때 **"Connection error"** 라는 문장을 콘솔에 출력한다.

이후 선언한 `db`에 `mongoose.connection` 객체를 담고   
해당 객체를 `db`라는 이름으로 모듈화 시킨다.

이제 다시 `server`폴더에 있는 `index.js`로 돌아오자.   
index.js에 아래 코드들을 추가한다.   
```js{3}
const db = require('./db')              // 생성한 모듈 가져오기(MongoDB 연결)
// MongoDB 연결
db.once('open', function () {           
    console.log('DB Connected');
});

// DB 연결중 에러가 있으면 "DB ERROR :" 와 에러를 출력
db.on('error', function (err) {
    console.log('DB ERROR : ', err);
});
```
db 객체에 우리가 이전에 만들었던 모듈을 담아주고,   
`db.once`를 이용해 `MongoDB`와 연결해준다. 연결 성공했을때   
**"DB Connected"**메세지를 콘솔에 출력한다.    
연결에 실패했을때 **"DB ERROR + 에러메세지"**를 출력해준다.
`index.js`파일 수정후 자신이 `nodemon`을 사용해 서버를 켜둔 상태라면   
자동으로 서버가 리로드되면서 콘솔창에    
**"DB Connected"** or **"DB ERROR"** 메세지를 확인 할 수 있을것이다.

아래코드는 현재 server 폴더안의 index.js 파일 전체코드이다.   
```js{3}
const express = require('express')      // 우리가 npm install 한 express를 가져옴

const app = express()                   // app에 받아온 모듈 저장
const port = process.env.PORT || 3001;  // port 번호 3001 번으로 설정
const db = require('./db')              // 생성한 모듈 가져오기(MongoDB 연결)

app.get('/', (req, res, next) => {      // 해당 url로 접속했을때 실행할 행동 정의해줌
    res.send('hello world!');
});

// MongoDB 연결
db.once('open', function () {           
    console.log('DB Connected');
});

// DB 연결중 에러가 있으면 "DB ERROR :" 와 에러를 출력
db.on('error', function (err) {
    console.log('DB ERROR : ', err);
});

app.listen(port, function () {          // 해당 port번호로 리스닝이 성공했을때 실행될 콜백함수이다.
    console.log('server on! ' + port);
});

```

여기까지 문제없이 성공했다면 우리는 서버를 생성하고 서버와 `MongoDB`와 연결을 마친것이다!











