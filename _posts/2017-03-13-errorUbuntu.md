---
layout: post
category : ubuntu
title: Ubuntu 16.04 각종 오류들 정리
---

### colord-sane Crash
무슨 이유인지 모르겠는데 아래와 같은 에러가 우분투 설치후 주기적으로 나타났습니다.

![error_1](https://cloud.githubusercontent.com/assets/13127455/23853876/fb6d39ea-0831-11e7-8c82-bab91ce33fe7.png)

찾아보니 이 현상이 발생하는 사람이 많은 것 같네요..; 댓글을 보니 오래전부터.. 최근 16.04까지 지속되고 있는 문제로 보입니다.
https://bugs.launchpad.net/ubuntu/+source/sane-backends/+bug/1351286

colord-sane은 스캐너 관련 패키지라고 합니다. 전 사용하지 않아서 아래와 같이 지우는 것으로 해결하였습니다.


```bash
$ sudo apt-get remove sane-utils
$ sudo apt-get remove colord
$ sudo apt-get autoremove
```


### 참고자료
http://askubuntu.com/questions/875864/colord-sane-crash-after-boot-at-startup-on-xubuntu-16-04-64-bit
