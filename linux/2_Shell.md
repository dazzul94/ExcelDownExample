# 리눅스 운영 및 관리
## 2. Shell
###  ※ 셸의 개념 및 종류
#### - 셸의 개념과 특징
- 셸: 커널과 사용자간의 다리 역할
- 사용자로부터 받은 명령을 해석하고 프로그램을 실행한다.
- 시스템에 로그인하면 각 사용자에게 셸이 부여된다.(로그인 막는 효과 O)
- 셸 특징
    + *본셸: 가장 먼저 개발된 셸*
    + bash: 표준셸
    + C셸(csh): C언어기반
    + tcsh: csh를 강화함
    + ksh: 콘셸(korn shell)
---
17. 다음 중 셸의 역할에 대한 설명으로 알맞은 것은?  
    ① 프로세스 스케줄링을 관리한다.  
    ② 실행중인 프로그램 관리 역할을 수행한다.  
    ❸ 사용자로부터 명령을 입력받아서 해석한다.  
    ④ CPU, 메모리, 디스크 등의 하드웨어를 제어한다.  

16. 다음 중 리눅스의 표준 셸로 알맞은 것은?  
① csh		② ksh
❸ bash		④ tcsh

13. 다음 중 가장 먼저 개발된 셸로 알맞은 것은?  
    ❶ 본셸		② 배시셸
    ③ C셸		④ 콘셸
---
### ※ 셸의 확인과 변경
#### - 셸의 확인
##### ＠ 사용중인 셸 확인 'echo $SHELL'
~~~
echo $SHELL
~~~
---
16. 다음 중 ihduser 사용자가 로그인 직후에 부여 받은 셸을 확인하는 방법으로 틀린 것은?  
    ① echo $SHELL	  
    ② grep ihduser /etc/passwd  
    ③ env | grep SHELL	  
❹ chsh -l    
-> 4번은 변경 가능한 셸의 확인
---
##### ＠ 변경 가능한 셸의 확인
~~~
chsh -l
cat /etc/shells
~~~
---
15. 다음 ( 괄호 ) 안에 들어갈 파일명으로 알맞은 것은?  
~~~
$ cat (괄호)
/bin/sh
/bin/bash
/sbin/nologin
/bin/dash
/bin/tch
/bin/csh
~~~
    ① /etc/profile		  
② /etc/bashrc  
    ③ /etc/chsh		  
❹ /etc/shells
---
##### ＠ 셸의 변경
~~~
chsh
~~~
---
17. 다음 작업에 해당하는 명령으로 알맞은 것은?  
~~~
[ihduser@www ~] $
Changing shell for ihduser.
Password:
New shell [/bin/bash]: /bin/csh
Shell changed.
[ihduser@www ~] $
~~~
    ① chfn		❷ chsh
    ③ chmod		④ usermod
---
###  ※ 셸 환경설정
#### - 셸 변수와 환경변수
##### ＠ 셸 변수
- 특정한 셸에서만 적용되는 변수
- 변수명=값으로 선언하고 echo $변수로 확인할 수 있다.

##### ＠ 환경변수
- 프롬프트 변경, PATH 변경 등과 같이 셸의 환경을 정의
- 미리 예약된 변수명이 있다.
- bash에서는 PATH, SHELL 등과 같이 대문자로 된 변수
- 현재 설정된 전체 환경변수는 env 명령으로 확인가능

#### - 주요 환경변수
##### ＠ 주요 환경변수
- HOME: 사용자의 홈 디렉토리
- PATH: 실행 파일을 찾는 디렉터리 경로
- LANG: 셸 사용시 기본으로 지원되는 언어
- TERM: 로그인한 터미널의 종류
- PWD: 사용자의 현재 작업 디렉토리
- SHELL: 사용자의 로그인 셸
- USER: 사용자의 이름
- DISPLAY: X에서 프로그램 실행시 출력되는 창
- PS1: 프롬프트(Prompt) 변수
- PS2: 2차 프롬프트 변수
- HISTFILE: 히스토리 파일의 절대경로
- HISTSIZE: 히스토리 파일에 저장되는 명령어의 개수(줄 기준)
- HISTFILESIZE: 히스토리 파일 크기
- HOSTNAME: 시스템의 호스명
- MAIL: 도착한 메일이 저장되는 경로
- TMOUT: 일정시간 동안 작업하지 않을경우 로그아웃되는 시간(초)
- UID: 사용자의 UID
---
~~~
[posein@www ~] $
/usr/lib/qu -3.3/bin:/usr/local/bin:/bin:/usr/bin:/usr/sbin:/home/posein/bin
[posein@www ~] $
~~~
14. 다음 명령의 결과에 해당하는 환경변수로 알맞은 것은?  
    ① PWD		② HOME
    ❸ PATH		④ PS1
---
18. 다음 중 셸 사용 시 기본으로 지원되는 언어를 한글에서 영문으로 변경할 때 사용하는 명령으로 알맞은 것은?  
    ① TERM=C		❷ LANG=C
    ③ PS1=C		④ PS2=C
---
#### - 배시셸의 주요 기능과 관련 파일
##### ＠ 배시셸의 주요 기능(1): *명령어 History 기능*
- bash에서는 입력 후 실행했던 모든 명령이 히스토리 리스트 버퍼에 스택으로 저장.
- history를 입력하면 히스토리 리스트에 있는 명령어들이 출력.
- 각 사용자의 홈 디렉터리 안에 .bash_history라는 파일에 업데이트 된다.(로그아웃할때 저장)

##### ＠ 관련 명령어 history(!)
---
12. 다음 중 최근에 실행한 명령어 10개를 확인하는 명령으로 알맞은 것은?  
    ① !10		② ! 10
    ③ ! -10		❹ history 10  
-> 1번은 10번째 히스토리    
-> 2번은 X  
-> 3번은 최근 10번째 히스토리  
-> 최근에 실행한 명령어 10개  
---

##### ＠ 배시셸의 주요 기smd(2): *alias기능*
- alias로 지정해 놓으면 나만의 명령어로 쓸 수 있다.
- alias라고만 실행하면 설정된 목록을 확인 할 수 있다.
- unalias라고 하면 설정을 해제할 수 있다.
~~~
alias [별명='명령어']
unalias 별명
~~~
---
13. 다음 명령의 결과로 알맞은 것은?
~~~
$ user=lin
$ echo user
()
~~~
    ① lin	② echo
    ❸ user	④ 화면에 아무것도 출력되지 않는다.  
-> user에 lin을 저장했다. echo user라고 하면 user가 출력된다.
-> echo $user라고 해야 user에 저장된 lin이 출력된다.
---
##### ＠ 셸 관련 파일 및 디렉터리
사용자가 명령행에서 설정한 환경변수와 alias는 일시적인 것. 다음 로그인 시에는 적용이 안되므로 파일에 저장해야한다.
- /etc/profile: 시스템 전체에 적용되는 환경변수와 시작관련 프로그램 설정
- /etc/bashrc: 시스템 전체에 적용되는 alias와 함수 설정
- ~/.bash_profile: 개인 사용자의 환경설정과 시작프로그램 설정 관련 파일
- ~/.bashrc: 개인 사용자가 정의한 alias와 함수 설정
- ~/.bash_logout: 개인사용자가 로그아웃할 때 수행하는 설정
- /etc/profile.d: 몇몇 응용프로그램들이 시작할때 필요한 스크립트의 위치. 보통/etc/profile에서 실행된다.
---
11. 다음 중 사용자가 설정한 alias가 다음 로그인 시에도 사용가능하도록 등록하는 파일로 가장 알맞은 것은?  
    ① ~/.bash_history	② ~/.cshrc
    ③ ~/.bash_logout	❹ ~/.bashrc
---
15. 다음 결과에 해당하는 명령으로 알맞은 것은?  
    ❶ alias		② alias -l
    ③ ualias		④ unalias
-> alias 만 치면 명령어 목록이 나온다.
~~~
[ihduser@www ~] $
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias vi='vim'
~~~
---
18. 다음 중 앨리어스(alias)가 설정된 ls를 해제하는 명령으로 알맞은 것은?  
    ① ualias ls		❷ unalias ls
    ③ !ls		④ ?ls
---
11. 다음 중 사용자가 로그아웃할 때 실행할 명령을 등록하는 파일로 알맞은 것은?  
    ① ~/.bash_profile	❷ ~/.bash_logout  
    ③ ~/.bashrc_logout	④ ~/.bash_exit
---
