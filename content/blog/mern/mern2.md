---
title: MERN 스택(MongoDB 설치)
date: 2020-04-21 15:04:79
category: mern
draft: false
---


# MongoDB 설치하기 #

MongoDB를 설치하는 방법중 세가지 방법정도를 소개하려한다.   


## Homebrew로 설치하기(MacOS) ##
> **Homebrew란?**   
    MacOS 용 패키지 관리자이다. 터미널(`Terminal`)에서 명령어를 작성하여 자신이 필요로 하는    
    프로그램들을 설치, 삭제, 업데이트 할수있다.   
    [Homebrew 설치하러가기](https://brew.sh/index_ko)

- 먼지 터미널을 킨뒤 `Homebrew`를 사용하기전엔 항상 
    ```
    brew update
    ```
    위 명령어를 입력해 주어야한다. 이후
    ```
    brew install mongodb-community
    ```
    이 명령어만 입력하면 `brew`가 알아서 `MongoDB`설치를 끝낼것이다.   
    설치가 완료되면 아래 세개파일이 해당 경로에 자동 생성되며   
    디폴트 값으로 지정된다.

    ```
    configuration file : /usr/local/etc/mongod.conf   
    log directory path  : /usr/local/var/log/mongodb   
    data directory path : /usr/local/var/mongodb
    ```

    이후
    ```
    mongod --config /usr/local/etc/mongod.conf
    brew services start mongodb-community@4.0
    ```
    위 두가지 명령어를 입력해주면 

    ```
    mongo
    ```
    위 명령어로 `MongoDB`를 실행 시킬수 있다!

    만약 자신이 brew services start mongodb-community@4.0    
    이 커맨드를 입력하지 않았다면   
    mongod 라는 명령어를 통해 MongoDB서버를 켜주어야 한다.


## Docker로 설치하기 ##
> **Docker란?**   
    도커는 컨테이너 기반의 오픈소스 가상화 플랫폼이다.   
    다양한 프로그램들과 실행환경들을 컨테이너로 추상화 하고, 동일한   
    인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 만들어준다.   
    [Docker 설치하러가기](https://www.docker.com/)

- Teminal을 실행시킨뒤
    ```
    docker run --name mongo -p 27017:27017 -d mongo
    docker start mongo
    docker exec -it mongo bash
    mongo    
    ```
    위 네가지 명령어들을 순차적으로 입력하면 MongoDB가 실행되는것을 확인할 수 있다.   

    외부접속이 가능하도록 설정을 변경해주고 싶다면,   
    ```
    apt-get update 
    apt-get install vim
    vim etc/mongod.conf.orig
    ```
    위 세가지 명령어를 통해여 `vim`을 실행시키고   
    bind_ip=127.0.0.1을 찾아서 0.0.0.0 으로 변경해준뒤 저장하면 된다. 


## Window에서 설치하기 ##   
- 먼저 [MongoDB 홈페이지](https://www.mongodb.com) 에 접속한다. 이후   
    `Software` -> `Community Server` 탭으로 찾아 들어간다   
    이후 자신이 사용하고 싶은 Version, OS, Package를 선택해 설치하면 된다.   
    설치프로그램 다운로드가 끝내면 해당 프로그램을 실행시킨다.   
    특별히 신경 설정들은 없기에 계속 next 또는 ok를 눌러주면되지만   

    중간에 `Install MongoDB Compass` 가 나오면 꼭!! **체크해제** 해주고    
    다음단계로 진행하자.`MongoDB Compass`는 `MongoDB` 를 위한 Tool인데    
    이걸 같이설치하면 가끔 알수없는 에러가   
    발생한다고 하니 잊지말고 체크해제후 설치하자!   
    만약 `MongoDB Compass`를 설치하고싶다면 `MongoDB`설치 완료후    
    개별적으로 설치하는것을 권장한다.   
    특별히 경로수정한것 없이 설치를 완료했다면
    ```
    c:\data\db
    ```  
    위 경로에 db폴더를 생성하자
    폴더를 만들었다면 `Path`를 설정해주자   
    내PC 혹은 내컴퓨터 오른쪽클릭 ->    
    속성 -> 고급 시스템 설정 -> 환경 변수 -> 시스템 변수 -> Path
    1. Server   
        cmd -> mongod [--dbpath]
    2. Client   
         cmd -> mongo   

    이제 cmd창을 열어 
    ```  
    mongod 
    ```  
    명령어를 입력하여 mongoDB서버를 가동하는지 확인한다. 이후 cmd창에서 아래 명령어를 입력한다.   
    ```  
    mongod.exe —dbpath "c:\data\db" —serviceName MongoDB —serviceDisplayName MongoDB
    ```  
    위 명령어에서 -dbpath 다음에 나오는 경로는 아까 위에서 만들었던 db폴더의 경로이다.   
    이후 cmd에서 
    ```
    mongo 
    ```
    를 입력하면 `MongoDB`가 작동하는것을 확인할 수 있다!




