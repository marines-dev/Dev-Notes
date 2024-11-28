# [Git] 깃배쉬(Git Bash) : 기본 명령어 사용하기

<br><br>

## **깃 옵션 설정하기**

1. Git Bash를 실행한다.
2. Git Bach의 상단바에 있는 Git Bash 아이콘을 클릭한다.
3. [Options]을 클릭하면 Options 창에서 다양한 옵션을 설정할 수 있다.

![image](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image.png)

![image%201](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%201.png)

<br><br>
<br><br>

## **깃 옵션 확인하기**

- git : 깃 명령에서 사용할 수 있는 다양한 옵션을 확인할 수 있다.

![image%202](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%202.png)

입력

<br><br>

![image%203](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%203.png)

출력

<br><br>
<br><br>

## 리눅스 명령어로 깃 사용하기

Git Bash의 터미널 창에서 리눅스 명령어로 깃을 사용할 수 있다.

<br><br>

**현재 디렉터리 확인하기**

- pwd : 현재 디렉터리의 경로를 확인할 수 있다.

![image%204](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%204.png)

입력

<br><br>

![image%205](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%205.png)

출력

<br><br>

- ls : 현재 디렉터리에 있는 파일, 디렉터리 이름을 확인할 수 있다.
이름 뒤에 슬래시(/)가 붙어있으면 디렉터리이다.

![image%206](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%206.png)

![image%207](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%207.png)

입력

<br><br>

![image%208](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%208.png)

출력

<br><br>

> **Is 명령 옵션**
> 
> 
> ls 명령을 사용할 때 옵션을 추가하면 파일과 디렉터리를 다양한 형식으로 표시할 수 있으며, 옵션을 2개 이상 사용할 수도 있다.
> 
> - ls -r : 파일의 정렬 순서를 거꾸로 표시한다.
>     
>     ![image%209](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%209.png)
>     
> - ls -t : 파일 작성 시간순으로 표시한다.
>     
>     ![image%2010](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2010.png)
>     
> - ls -l : 파일, 디렉터리의 상세 정보까지 표시한다.
>     
>     ![image%2011](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2011.png)
>     
> - ls -a : 숨긴 파일, 디렉터리도 함께 표시한다.
>     
>     ![image%2012](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2012.png)
>     

<br><br>
<br><br>

**디렉터리 이동하기**

- cd : cd 명령의 다음에 오는 명령 옵션을 기준으로 디렉터리 사이를 이동할 수 있다.

<br><br>

> **cd 명령 옵션**
> 
> - cd ~ : 현재 접속 중인 사용자 디렉터리(홈 디렉터리)로 이동한다.
>     
>     ![image%2013](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2013.png)
>     
> - cd *디렉터리이름* : 현재 디렉터리 기준 하위 디렉터리로 이동한다.
>     
>     ![image%2014](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2014.png)
>     
> - cd .. : 현재 디렉터리의 상위 디렉터리로 이동한다.
>     
>     ![image%2015](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2015.png)
>     
> - cd . : 현재 사용자가 작업 중인 디렉터리이다.
>     
>     ![image%2016](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2016.png)
>     

<br><br>
<br><br>

**디렉터리 생성하기**

- mkdir *디렉터리이름* : 현재 디렉터리를 기준으로 하위 디렉터리를 생성한다.
    
    ![image%2017](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2017.png)
    
    입력


    ![image%2018](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2018.png)
    
    결과
    

<br><br>
<br><br>

**디렉터리 삭제하기**

- rm *디렉터리이름* : 현재 디렉터리를 기준으로 하위 디렉터리를 삭제한다.
- rm -r *디렉터리이름* : -r 옵션을 추가하면, 현대 디렉터리를 기준으로 하위 디렉터리와 파일을 함께 삭제한다.
    
    ![image%2019](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2019.png)
    
    ![image%2020](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20기본%20명령어%20사용하기/image%2020.png)
    

<br><br>
<br><br>

**터미널 창 지우기**

- clear

<br><br>
<br><br>

**터미널 종료하기**

- exit
