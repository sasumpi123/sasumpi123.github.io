---
title: MERN 스택(Model 생성)
date: 2020-04-23 15:04:96
category: mern
draft: false
---

`MongoDB`와 연결을 끝냈으면 아래와 같은 폴더구조를 만들자.
```
MERN
└── server
    ├── db
    │   └── index.js
    ├── node_modules
    │   └── ...
    ├── models
    │   └── addr-model.js
    ├── index.js
    ├── package-lock.json
    └── package.json
```

`server`폴더 아래에 `models`폴더를 생성하고   
그안에 `addr-model.js`파일을 생성하면된다.   
MongoDB를 통해 우리가 실질적으로 사용할 스키마를 여기서 정의할것이다.   
```js{3}
// MongoDB 스키마 정의

const mongoose = require('mongoose')
const Schema = mongoose.Schema

const Addr = new Schema(
    {
        name: { type: String, required: true, unique: true },
        email: { type: String },
        phone: { type: String }
    });

module.exports = mongoose.model('addr', Addr)
    // DB에 있는 addr이라는 데이터 콜렉션을 현재 코드의 Addr이라는 json객체와 연결
```

우리는 현재 주소록 컨셉의 `CRUD`를 만들려고 하고있기때문에,   
이름, 이메일, 핸드폰 번호 데이터가 필요하다.   
이름은 데이터 타입이 `String` 이고 유니크하며 필수이다.     
이메일의 타입은 `String`이고 핸드폰 번호도 `String`이다.

이전 `db`폴더안의 `index.js`에서 아래코드를 작성했었다.
```
mongoose.connect('mongodb://127.0.0.1:27017/addr', { useNewUrlParser: true })
```
우리는 `MongoDB`에서 `addr Collection`과 연결이 되있는상태이다.    
따라서 우리는 해당 `Collection`과 우리가 만든 `Schema`를 연결하기위해   
아래의 코드가 필요하다
```
module.exports = mongoose.model('addr', Addr)
```
이제 우리가 하려는 주된 목적인 CRUD코드를 작성할 차례이다.   
먼저 MERN스택에서 CRUD를 하기위해선 MongoDB CRUD Query문을 알아야한다.   

먼저 아래와 같은 폴더구조를 만들자
```
MERN
└── server
    ├── db
    │   └── index.js
    ├── node_modules
    │   └── ...
    ├── models
    │   └── addr-model.js
    ├── controllers
    │   └── addr-ctrl.js
    ├── index.js
    ├── package-lock.json
    └── package.json
```
`server`폴더 아래에 `controllers`폴더를 생성하고   
그안에 `addr-ctrl.js`파일을 생성하면된다.

해당 `addr-ctrl.js` 에 우리가 정의한 `Schema` 모듈을 가져온다.
```
const Addr = require('../models/addr-model')
```
먼저 c`Read`ud에 대한 함수를 작성해보자   

```js{3}
addrList = async (req, res) => {
    await Addr.find({}, (err, addrs) => {   // 빈 객체면 모든걸 찾음
        if (err) {
            return res.status(400).json({ success: false, error: err })
        }
        if (!addrs.length) {
            return res
                .status(404)
                .json({ success: false, error: '주소록을 찾을 수 없습니다.' })
        }
        return res.status(200).json({ success: true, data: addrs })
    }).catch(err => console.log(err))
}
```
위 코드에서 화살표함수와 비동기함수에서 매우 중요한 `async` `await`   
라는 단어를 볼수있다. 이 개념들에 대한 설명들은 따로 포스팅할 계획이다.   

`addrList`라는 변수를 선언하고 함수를 대입한다.   
위 함수는 `req`, `res`를 파라미터로 받으며 `Addr.find()`를 통해   
`Collection`에 있는 데이터들을 검색한다.   
만약 `err`가 발생하면 `400`에러를 세팅하고   
검색한 데이터의 길이가 0이라면 (비어있다면)   
`404`에러를 세팅하고 **주소록을 찾을 수 없습니다** 라는 메세지를 담아준다.     
만약 검색에 성공했다면, `data`에 검색 결과들을 담아준다.   
`.catch`를 통해 에러발생시 에러메세지를 콘솔에 출력해준다.










