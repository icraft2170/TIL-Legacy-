---
title: HTTP
---

# 인터넷

- 인터넷 != WWW(World Wide Web)
    - 인터넷 기반 서비스

    |이름|프로토콜|포트번호|기능|
    |------|-----------|------------|------------|
    |WWW|HTTP|80|웹서비스|
    |Email|SMTP/POP3/IMAP|25/110/114|이메일|
    |FTP|FTP|21|파일전송서비스|
    |DNS|TCP/UDP|53|네임서비스|
    |NEWS|NNTP|119|인터넷뉴스|

- 인터넷(Internet)
    - TCP/IP기반의 네트워크가 전세계로 확대되어 하나로 연결된 네트워크의 네트워크(네트워크의 결합체)



## 웹

## HTTP(HyperText Transfer Protocol)
- 팀 버너스리와 그의 팀 CERN에서 HTML과 HTTP를 발명
- HTTP는 서버 클라이언트가 인터넷상에서 데이터를 주고 받기 위한 프로토콜

### HTTP 작동방식
- HTTP는 서버/클라이언트 모델을 따른다
- 장점
    - 불특정 다수에게 하는 서비스로 적합
    - 클라이언트와 서버가 계속 연결된 상태가 아니기 때문에 클라이언트와 서버간의 최대 연결 수보다 훨씬 많은 요청과 응답처리를 할 수 있다.
- 단점
    - 연결을 끊기 때문에, 클라이언트의 이전 상황을 알 수 없고 이러한 특징을 무상태(Stateless)라고 함.
    - 정보 유지가 힘들어 Cookie와 같은 기술 등장    


### URL(Uniform Resource Locator)
- 인터넷상의 자원의 이치
- 특정 웹 서버의 특정파일에 접근하기 위한 경로 혹은 주소

```
http://www.naver.com/docs/index.html
http : 프로토콜
www.naver.com : IP 주소 또는 도메인
docs : 경로
index.html : 접속하는 파일
```