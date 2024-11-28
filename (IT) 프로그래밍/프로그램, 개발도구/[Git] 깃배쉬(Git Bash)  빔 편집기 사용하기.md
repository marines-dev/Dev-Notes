# [Git] 깃배쉬(Git Bash) : 빔 편집기 사용하기

<br><br>

### **빔(Vim)**

터미널에서 사용하는 기본 텍스트 편집기로, 터미널 창에 키보드만 이용해서 텍스트 문서를 만들 수 있어 시간을 단축할 수 있다.

<br><br>

**빔 편집기 실행하기**

- vim *파일이름* : 현재 디렉토리에 파일 이름으로 해당 파일을 열고(해당 파일이 없다면 파일 생성), 빔 편집기를 실행한다.


![image](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20빔%20편집기%20사용하기/image.png)

입력
  
<br><br>

![image%201](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20빔%20편집기%20사용하기/image%201.png)
    
![image%202](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20빔%20편집기%20사용하기/image%202.png)
    
Text 파일 생성 및 빔 편집기 실행
    
<br><br>
<br><br>

**ex 모드와 입력 모드**

1. 빔에는 읽기 모드인 ex 모드와 문서를 작성할 수 있는 입력모드가 있으며, 처음에는 ex 모드로 열린다. 
    
    ex 모드에서 [I] 또는 [A]를 눌러서 입력 모드로 바꾸어 텍스트를 작성할 수 있다.
    
    ![image%203](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20빔%20편집기%20사용하기/image%203.png)
    
   [I]를 눌러서 입력 모드로 변경

    <br><br>
    ![image%204](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20빔%20편집기%20사용하기/image%204.png)
    
    빔 편집기에서 텍스트 작성 중
    
<br><br>

2. 입력 모드에서 텍스트 입력 후 파일을 저장하려면, [Esc]를 눌러 다시 ex 모드로 돌아가야 한다.
    
    :wq를 입력하여 편집한 문서를 저장하고 빔 편집기를 종료할 수 있다.
    
    ![image%205](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20빔%20편집기%20사용하기/image%205.png)
    
   ex 모드에서 :wq 입력
   
    <br><br>

    ![image%206](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20빔%20편집기%20사용하기/image%206.png)
    
    ![image%207](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20빔%20편집기%20사용하기/image%207.png)
    
    Text 파일에 편집한 내용을 저장하고 빔 편집기는 종료
    
<br><br>

> **ex 모드 명령**
> 
> - :wq : 편집한 문서를 저장하고 빔 편집기를 종료한다.
> - :w 또는 :wrte : 편집하던 문서를 저장한다.
> - :q 또는 :quit : 빔 편집기를 종료한다.
> - :q! : 편집한 문서를 저장하지 않고 편집기를 종료하며, 임시 파일(.swp)이 생긴다.

<br><br>
<br><br>

**텍스트 문서 확인하기**

- *cat 파일이름.txt*  : 터미널 창에서 텍스트 문서의 내용을 간단히 확인할 수 있다.
    
 ![image%208](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/%5BGit%5D%20깃배쉬(Git%20Bash)%20%20빔%20편집기%20사용하기/image%208.png)
    
<br><br>

> **cat 명령 모음**
> 
> - cat *파일이름.txt* : file의 내용을 화면에 표시한다.
> - cat *파일이름1.txt* > *파일이름2.txt* : file(s)를 차례로 연결해서 새로운 파일인 Newfile을 만든다.
> - cat *파일이름1.txt* >> *파일이름2.txt* : file1의 내용을 file2의 내용 끝에 연결한다.
