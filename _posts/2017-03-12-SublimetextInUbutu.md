---
layout: post
title: Ubuntu 16.04에서 서브라임 텍스트 설정
---

Sublime text에서 MarkDown을 활용하기 위해서 관련 플러그인 설치가 필요하다.



### 한글 입력처리
처음 우분투를 설치하면 한글입력이 안되는 문제가 있으므로 아래와 같이 한글이 입력되게 처리해주어야 한다. 일단 github에서 관련 소스를 내려받는다.
```
$ git clone https://github.com/lyfeyaj/sublime-text-imfix.git
// 내려받은 디렉토리로 이동
$ cd sublime-text-imfix
// 실행
$ ./sublime-imfix
```

이렇게 설치를 하면 한글이 입력되지만, 입력이 한 박자 늦게 되는 문제가 발생한다. 윈도우에서는 IMESupport 패키지를 설치하면 괜찮아진다고 하는데, 리눅스는 어떻게 하는지..

### Markdown Editing 설치
1. Ctrl+Shift+P -> Install Package -> 'Markdown Editing' 설치

### Markdown Preview 설치
마크다운 파일(.md) 을 브라우저로 바로 보여주는 플러그인이다. 
1. Ctrl+Shift+P -> Install Package -> 'Markdown Preview' 설치
2. Ctrl+Shift+P -> Preview in Browser -> Github, markdown 중 선택
3. Preferences - Key Bindings 에 아래와 같이 단축키 추가

```
{ "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"} },
```

### 참고자료
- [우분투; Sublime text 3, Fcitx 를 사용한 한국어 입력](http://egloos.zum.com/nemonein/v/5269201)
- [Markdown Editing Github Page](https://github.com/SublimeText-Markdown/MarkdownEditing)
- [Markdown Preview Github Page](https://github.com/revolunet/sublimetext-markdown-preview)