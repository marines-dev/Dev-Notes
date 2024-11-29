# [Git] 깃배쉬(Git Bash) : 지역 저장소 사용하기

<br><br>

### **지역 저장소(Local Repository)**

깃의 지역 저장소는 본인의 컴퓨터에 저장된 로컬 버전의 깃 파일을 관리하는 저장소이다.

Git Bash를 이용하여 지역 저장소를 추가해 보자.

<br><br>

**지역 저장소 생성하기**

지역 저장소로 깃 파일의 버전 관리를 하기 위해서 컴퓨터의 폴더 안에 버전을 저장하는 저장소가 필요하다.

먼저 깃 저장소를 생성할 디렉터리를 생성하자.

- git init : 현재 디렉터리를 깃 저장소로 사용하기 위해 초기화한다.
- git init *디렉터리이름* : 현재 디렉터리에 저장소로 사용할 디렉터리를 생성하고 초기화한다.

    ![image](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image.png)

    Repository 이름의 저장소(디렉터리)를 생성한다.

    <br><br>
    
    ![image%201](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%201.png)

    cd 명령어를 이용해 해당 저장소로 이동하면 터미널 창에서 마지막 라인에 (main)이 표시되는 데, 현재 디렉터리에 깃 저장소가 생성되었다는 의미이다.

    <br><br>
    
    ![image%202](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%202.png)

    실제 Repository 저장소로 이동하면 .git 디렉터리가 생성된 것을 확인할 수 있다.
    
<br><br>

> **깃 상태 확인하기**
> 
> - git status : 깃 저장소의 상태를 보여주는 메시지를 표시한다.
>
> ![image%203](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%203.png)
> 

<br><br>

> **git status 상태 메시지**
> 
> - On branch main : 현재 main 브랜치에 있다. main 브랜치는 저장소에 들어 있는 디렉터리와 비슷한 것이다.
> - No commits yet : 아직 커밋할 파일이 없다.
> - nothing to commit : 현재 커밋할 파일이 없다.

<br><br>
<br><br>

### 깃 버전 관리하기

깃의 버전 관리 시스템은 깃 저장소 내에서 문서를 수정할 때마다, 수정 내용과 간단한 메모를 기록해 버전으로 저장하는 기능 제공한다. 이러한 버전 관리 시스템을 이용하면 원본 파일 이름은 그대로 유지하면서 버전마다 작업한 내용을 확인하고, 이전 버전으로 되돌릴 수도 있다.

<br><br>
<br><br>

### 깃 **버전 만들기**

깃에서 버전을 만드는 순서는 작업 트리 → 스테이지 → 저장소이다.

<br><br>

**작업 트리(working tree)**

파일 수정, 저장 등의 작업을 하는 디렉터리이다.

<br><br>

> **git status 상태 메시지**
> 
> - Untracked files : : 해당 파일은 아직 버전에 추가되지 않았다. 작업 트리에 있는 파일은 tracked와 untracked 상태로 구분할 수 있다. untracked 파일은 한 번도 커밋하지 않았으므로 깃이 수정 내역을 추적하지 않는다. 반대로 tracked 파일은 한 번이라도 커밋한 파일로 수정 내역을 추적한다.

<br><br>

**스테이지(stage)**

버전으로 만들 파일이 대기하는 영역으로, 작업 트리에서 파일을 수정하고 저장하였으면, 버전으로 만들 파일만 스테이지에 올린다.

- git add *파일이름.(확장자)* : 수정한 파일을 스테이지에 추가하기
- git add . : 저장소에 있는 수정한 파일을 한번에 스테이지에 추가할 수 있다.

    ![image%204](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%204.png)

    ![image%205](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%205.png)
    
    Repository 디렉터리에 Text.txt 파일을 추가한다.

    <br><br>
    
    ![image%206](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%206.png)
    
    Text.txt 파일을 스테이지에 추가한다.
    
<br><br>

> **git status 상태 메시지**
> 
> - Changes to be committed: : 새 파일을 커밋할 예정으로, staged 상태이다.
>
>     ![image%207](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%207.png) 
>     

<br><br>

**저장소(repository)**

스테이지와 저장소는 .git 디렉터리 안에 숨은 파일 형태로 존재하는 영역이다. 

스테이지에서 대기하고 있는 파일을 버전으로 만들어 저장하는 영역이다.

파일 수정을 끝내고 스테이지에 다 넣었다면 버전을 만들기 위해 깃에 커밋(commit)하면 새로운 버전이 생성되고, 스테이지에 대기하던 파일이 모두 저장소에 저장된다. 

- git commit : 스테이지에 추가한 파일 커밋 하기
- git commit -m “*메시지내용*” : 커밋과 함께 버전의 변경 사항을 기록할 커밋 메시지이다.
- git commit -am “*메시지내용*” : 스테이지에 올리고 커밋하기. 수정한 파일을 스테이지에 하나씩 올린 후 한번에 커밋할 수도 있지만, 스테이지에 올리는 동시에 커밋까지 할 수 있다. 단, 한 번이라도 커밋한 파일일 경우 사용할 수 있다.
- git commit —amend : 직전에 커밋한 커밋 메시지를 수정한다. 그리고 커밋 메시지가 수정되면 이전 커밋 버전에 변경 내용이 추가된다.

![image%208](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%208.png)

<br><br>

> **git status 상태 메시지**
> 
> - nothing to commit, working tree clean : 버전으로 만들 파일이 없고, 작업 트리의 수정 사항도 깨끗하다.
>   
>     ![image%209](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%209.png)
>     

<br><br>

> **저장소 버전 확인하기**
> 
> 
> 커밋 로그는 커밋한 최근 버전 정보부터 순서대로 확인할 수 있다. commit 다음 문자열은 커밋 해시(commit hash)로, 커밋을 구별할 수 있는 값이다. 그리고 (HEAD → main)는  가장 최신 버전이라는 표시이다. Author는 버전을 만든 사람,  Date는 버전 날짜, 커밋 메시지가 나온다. 
> 
> - git log : 커밋한 버전 정보를 표시한다.
> - git log —stat : 커밋한 버전 정보, 파일의 변경 기록을 표시한다.
> - git log —oneline : 한 줄에 한 버전씩 정보를 표시한다.
> - git log —all : 모든 버전 정보를 표시한다.
>
> ![image%2010](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%2010.png)
> 

<br><br>

> **저장소의 수정 사항 확인하기**
> 
> 
> 커밋하기 전에 수정 사항을 확인할 수 있다. 커밋 메시지를 참고해도 변경 사항을 파악하기 어려울 때 사용한다.
> 
> - git diff : 파일의 수정 사항을 표시한다.
>
> ![image%2011](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%2011.png)
>
> ![image%2012](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%2012.png)
> 

<br><br>

> **git status 상태 메시지**
> 
> - Changes not staged for commit : tracked 파일 기준으로 작업 트리에서 파일이 수정되었으나, 아직 스테이지에 추가되지 않았다.
> - modified: : tracked 파일 기준으로 파일이 수정되었다.
>
> ![image%2013](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%2013.png)
> 

<br><br>
<br><br>

### 깃 **작업 되돌리기**

<br><br>

**수정된 파일 되돌리기**

- git restore *파일이름.(확장자)* : 작업 트리에서 수정한 파일을 취소하고, 최신 버전으로 되돌린다.
- git restore —staged *파일이름.(확장자)* : 스테이지에 추가한 파일을 취소하고, 작업 트리 상태로 되돌린다.

![image%2014](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%2014.png)

![image%205](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%205.png)

<br><br>

**버전 되돌리기**

깃 파일은 커밋할 때마다 버전이 쌓이게 된다. 커밋한 파일의 마지막 버전을 취소하고 이전 버전으로 불러올 수 있다.

- git reset HEAD^ : 마지막 커밋을 취소하고, 작업 트리 상태로 되돌아가기. 이때, 명령어에서 HEAD가 가리키는 브랜치의 최신 버전을 취소하는 것이다.
- git reset — soft HEAD^ : 마지막 커밋을 취소하고, 스테이지 상태로 되돌아가기.
- git reset — mixed HEAD^ : 마지막 커밋을 취소하고, 스테이지 전 상태가 되돌아가기. git reset HEAD^ 명령어와 기능이 같다.
- git reset *커밋해시* : 커밋해시를 통해 특정 커밋으로 되돌리기.
- git revert *커밋해시* : 특정 커밋으로 되돌릴 때, 이전 버전 기록을 유지할 수 있다.

![image%2015](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%2015.png)

테스트를 위해 두 번째 커밋을 하고, git log 명령어로 커밋 정보 표시

<br><br>

![image%2016](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%2016.png)

마지막 커밋 취소

<br><br>

![image%2017](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/지역%20저장소%20사용하기/image%2017.png)

git log 명령어로 다시 출력할 경우 첫 번째 커밋 정보만 남아있는 것을 확인할 수 있다.

<br><br>

> **버전 관리에서 제외하기**
저장소가 있는 디렉터리 안에서 .gitignore 파일로 버전 관리를 하지 않을 파일, 디렉터리를 제외할 수 있다.
>
