---
layout: post
title: 각종 프록시(proxy) 환경설정 정리
---

### git

Proxy 세팅을 해야하는 환경에서 세팅이 안된 상태에서 git clone 등을 사용하면 아래와 같은 메세지가 뜹니다.

```bash
fatal: unable to access 'https://github.com/ddanguri/ddanguri.github.io.git/': Unknown SSL protocol error in connection to github.com:443
```

아래와 같이 프록시 세팅을 해줍니다.

```bash
$ git config --global http.proxy "[PROXY 주소]:[포트번호]"
$ git config --global https.proxy "[PROXY 주소]:[포트번호]"
```

참고 : 이렇게 설정된 정보는 아래와 home 아래 .gitconfig 에서 조회할 수 있습니다.

```bash
$ cat ~/.gitconfig
```
