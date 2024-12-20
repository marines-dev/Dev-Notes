# [Git] 깃배쉬(Git Bash) : 브랜치 사용하기

<br><br>

## 브랜치(Branch)

버전 관리 시스템에서 브랜치는 기존 파일을 그대로 유지하고, 여러 작업 단위로 다른 브랜치로 분기(Branch)하여 독립적으로 관리할 수 있다. 다른 브랜치에서 해당 파일 내용을 수정 및 추가할 수 있으며, 다른 브랜치에 있던 파일을 main 브랜치에 병합(Merge)할 수 있다. 브랜치는 커밋을 가리키는 포인터와 비슷하다. 

![image](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image.png)

<br><br>

> **브랜치의 기능적 원리 참고하기**
> 
> 
> [Git - 브랜치란 무엇인가](https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
> 

<br><br>
<br><br>

### **main 브랜치**

깃 저장소를 생성하면 기본으로 생성되는 브랜치이다. 깃의 이전 버전에서는 master라는 이름을 사용했다.

(HEAD → main)에서 HEAD는 가장 최신 버전의 브랜치를 가리킨다. 현재 가장 최신 버전의 브랜치가 main이라는 의미이다.

![image%201](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%201.png)

새로운 브랜치를 생성하지 않은 저장소에서 git log 명령어로 출력하여 가장 최신 버전의 브랜치가 main임을 알 수 있다.

<br><br>
<br><br>

### **브랜치 생성하기**

- git branch *브랜치이름* : 깃에서 브랜치를 생성한다.
- git branch : 브랜치 정보를 표시한다. 브랜치 이름 앞에 * 표시는 현재 작업 중인 브랜치를 의미한다.

![image%202](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%202.png)

branch1, branch2의 2개의 브랜치를 생성 후 브랜치의 정보를 확인해보면, 현재 저장소에 총 3개의 브랜치가 존재하는 것을 확인할 수 있다.

<br><br>

![image%203](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%203.png)

git log 명령어 커밋 로그를 확인해보면, 가장 최신 버전을 추가한 브랜치는 HEAD가 가리키는 main 브랜치, branch1, branch2가 최신 버전임을 알 수 있다.

<br><br>

![image%204](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%204.png)

main 브랜치에서 커밋의 최신 버전이 Ver3일 때, Dev 브랜치를 따로 만들면 main 브랜치의 Ver3까지의 버전을 가지고 Dev 브랜치가 생성된다.

<br><br>
<br><br>

### **브랜치 전환하기**

브랜치를 전환하면서 작업할 수 있다. 깃의 이전 버전에서는 checkout을 사용했다.

- git switch *브랜치이름* :  브랜치를 전환한다.

<br><br>

> **git log 명령 옵션**
> 
> 
> 브랜치 관련 명령 옵션이다.
> 
> - git log —branches : —branches 옵션을 추가하면 브랜치마다 최신 버전 정보를 한눈에 볼 수 있다.
> - git log —branches —graph : 각 브랜치의 버전 정보 관계를 수직선으로 표시한다.
> - git log *브랜치이름*..*브랜치이름* : 왼쪽 브랜치의 버전 정보를 기준으로 제외하여 오른쪽 브랜치의 버전 정보를 표시한다.

<br><br>

![image%205](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%205.png)

브랜치를 전환한 후 디렉터리 경로 뒤에 현재 작업 중인 브랜치가 branch1로 바뀌었다.

<br><br>

![image%206](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%206.png)

branch1 브랜치는 main 브랜치의 test.txt 파일을 가지고 있으므로 수정 및 커밋이 가능하다. 이때 main 브랜치에는 적용되지 않는다. 커밋 로그를 확인해보면 branch1에서 vs4 버전을 만들었고 HEAD가 가리키는 최신 버전의 브랜치는 branch1임을 알 수 있다.

<br><br>

![image%207](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%207.png)

이번에는 Branch1.txt 파일을 새로 생성한후 커밋하여 버전을 추가하였다. 마찬가지로 branch1에서 새로 작업했기 때문에 main 브랜치에는 적용되지 않는다.

<br><br>

![image%208](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%208.png)

이번에는 main 브랜치로 전환하여 test.txt 파일을 수정 및 커밋한다. main 브랜치에서 수정한 버전 또한 main에만 종속하는 독립적인 버전이다.

<br><br>

![image%209](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%209.png)

Dev 브랜치에서 만든 버전은 main 브랜치에 적용되지 않으며, 마찬가지로 Dev 브랜치 생성 이후 main 브랜치에서 만든 버전은 Dev 브랜치에 적용되지 않으므로 버전을 따로 관리할 수 있게 된다.

<br><br>
<br><br>

### 브랜치 병합하기

각각 브랜치에서 커밋을 하여 버전을 만든 후, 필요에 따라 main 브랜치에서 분기한 브랜치의 버전을 병합(merge)할 수 있다. 그러므로 브랜치 병합 작업은 main 브랜치에서 해야한다.

- git merge *브랜치이름* : main 브랜치에서 브랜치를 병합한다.

<br><br>

![image%2010](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2010.png)

main 브랜치에서 Dev 브랜치를 병합하면 Dev 브랜치의 Ver5 버전이 main 브랜치의 Ver7 버전과 합쳐저 새로운 버전 Ver8을 추가한다.

<br><br>

**서로 다른 파일 병합하기**

브랜치 간에 서로 다른 파일을 병합하는 방법이다. 

<br><br>

![image%2011](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2011.png)

main 브랜치로 전환 후 브랜치 안에 있는 파일들을 확인해 보면 test.txt, test2.txt 파일이 존재한다. 이후에 branch2를 병합한 후 다시 파일 유무를 확인해보면 branch2에 있는 branch2.txt 파일이 추가된 것을 알 수 있다.

<br><br>

![image%2012](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2012.png)

참고로 git merge 명령어를 실행하게 되면 빔 편집기가 자동으로 실행되는데, 이때 "Merge branch 'branch2"라는 기본 커밋 메시지가 입력되어 있다. 원하는 커밋 메시지로 수정 및 저장하여 빔 편집기를 종료하면 버전이 추가된다.

<br><br>

> **빨리 감기 병합(fast-forward merge)**
main 브랜치에서 브랜치를 분기한 후에 main 브랜치에 추가된 버전이 없다면, 다른 브랜치를 병합할 때 빨리 감기 병합으로 작업하게 된다.
> 

<br><br>
<br><br>

 **같은 파일의 다른 위치를 수정할 경우 병합하기**

브랜치 간에 같은 파일의 다른 위치를 수정할 경우 병합하는 방법이다.

<br><br>

![image%2013](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2013.png)

새로운 저장소에서 테스트를 진행하겠다. 
main 브랜치에서 note 파일을 생성한 후 vim 편집기로 내용을 입력하고 커밋까지 완료한다.
note 문서의 내용은 추후에 각각의 브랜치가 같은 note 문서의 서로 다른 2번째, 4번째 라인에서 각자 내용을 추가할 것이므로 알아보기 쉽게 2개의 #title 키워드 아래에 라인을 한 칸씩 추가하였다.

<br><br>

![image%2014](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2014.png)

other 브랜치를 생성한 후 전환하여 note 파일을 열고 비어있는 2번째 라인에 "other에서 2번째 줄에 입력했다."라는 내용을 추가한 후 커밋하였다.

<br><br>

![image%2015](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2015.png)

다시 main 브랜치로 전환 후 note 파일을 열고 비어있는 4번째 라인에 "main에서 4번째 줄에 입력했다."라는 내용을 추가 후 커밋하였다.

<br><br>

![image%2016](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2016.png)

other 브랜치를 병합한 후 note 파일의 내용을 확인해보면 main 브랜치와 other 브랜치의 수정 내용이 합쳐진 것을볼 수 있다. 이렇게 같은 파일에서 서로 다른 위치를 수정했을 경우 자동으로 병합할 수 있다.

<br><br>

![image%2017](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2017.png)

git merge 명령어를 실행하게 되면 빔 편집기가 자동으로 실행되는데, 기본 커밋 메시지를 사용하거나 원하는 커밋 메시지로 수정 및 저장하여 빔 편집기를 종료하면 새로운 버전이 추가된다.

<br><br>

**같은 파일의 같은 위치를 수정할 경우 병합하기**

브랜치 간에 같은 파일의 같은 위치 수정할 경우 병합하는 방법이다. 깃에서는 줄 단위로 변경 여부를 확인하기 때문에 서로 다른 브랜치에서 같은 파일의 같은 라인을 수정한 후 브랜치를 병합하면 충돌(conflict)이 발생한다. 병합할 때, 충돌이 발생하면,  자동으로 병합될 수 없으므로 사용자가 직접 충돌한 위치를 수정한 후 커밋해야 한다. 

<br><br>

![image%2018](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2018.png)

main 브랜치에서 빔 편집기로 note를 열고 5번째 라인에 "main에서 5번째 줄에 입력했다'라는 내용을 추가 및 커밋하였다.

<br><br>

![image%2019](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2019.png)

이번에는 other 브랜치로 전환 후 note를 열고 5번째 라인에 "other에서 5번째 줄에 입력했다'라는 내용을 추가 및 커밋하였다. 이렇게 서로 다른 브랜치에서 같은 note 파일의 수정 위치를 같게 한다.

<br><br>

![image%2020](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2020.png)

다시 main 브랜치로 전환 후 other 브랜치를 병합하면 "CONFLICT (content) : Merge conflict in note"라는 경고 메시지가 표시된다. 이 메시지는 note 파일이 자동으로 병합하면서 충돌이 발생했다는 뜻이다.

<br><br>

![image%2021](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2021.png)

vim 편집기로 충돌이 발생한 note 파일을 열고 내용을 확인해 보면, 브랜치 간에 병합하면서 충돌이 발생한 내용이 수정되어 기록되어 있다.

<br><br>

![image%2022](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2022.png)

수정된 내용을 참고하여 원하는 내용으로 다시 수정한 후 저장 및 빔 편집기를 종료한다.

<br><br>

![image%2023](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2023.png)

수정한 note 파일을 수동으로 직접 커밋하여 충돌을 해결한다.

<br><br>

> **병합 자동화 프로그램**
> 
> 
> 깃을 자동으로 병합하고, 충돌을 해결하는 프로그램이다. 병합 알고리즘에는 2 way merge와 3 way merge가 있는데, 3 way merge가 훨씬 효율적이므로 3 way merge를 지원하느 프로그램을 선택하자. 
> 
> - P4Merge : 무료, 직관적, 편리, 병합 기능 우수, 단축키를 지원하지 않음
> - meld : 무료, 오픈 소스, 파일 비교, 직접 편집 가능
> - Kdiff3 무료, 편리, 병합 기능 우수, 한글 깨질 수 있음
> - Araxis Merge : 유료, 용량 큰 파일에서도 잘 작동함.

<br><br>
<br><br>

**특정 버전으로 병합하기**

브랜치 전체를 병합하지 않고,  특정 버전만 병합할 수 있다. 병합 후 새로운 버전이 생성되는 것이 아닌, 병합한 브랜치의 특정 버전이 그대로 추가된다. 

브랜치 병합은 필요한 브랜치의 필요한 버전만 사용하자.

- git cherry-pick *커밋해시* : 커밋 해시의 버전을 병합한다.

<br><br>

![image%2024](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2024.png)

other 브랜치로 전환하여 각각 note2와 note3 파일을 생성하고 커밋한다.

<br><br>

![image%2025](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2025.png)

다시 main 브랜치로 전환하여 other 브랜치의 "note2 추가" 커밋 메시지의 커밋해시를 복사하여 git cherry-pick 명령어 뒤에 추가하여 특정 버전으로 병합을 한다. 커밋 로그를 확인해보면 other 브랜치에서 추가했던 "note2 추가" 커밋 메시지의 버전이 그대로 main 브랜치의 최신 버전으로 추가된 것을 알 수 있다.

<br><br>
<br><br>

### **브랜치 삭제하기**

브랜치를 병합한 후 더 이상 사용하지 않는 브랜치는 깃에서 삭제할 수 있다. 삭제한 브랜치는 실제로 저장소에서 삭제하는 것이 아닌 버전 관리에서 제외하는 것으로 같은 이름으로 다시 브랜치를 만들면 에전에 작업한 버전을 그대로 불러온다. 저장소의 기본 브랜치인 main브랜치에서 브랜치를 삭제해야 한다

- $ git branch -d *브랜치이름* : 브랜치이름과 같은 브랜치 삭제하기

![image%2026](https://github.com/marines-dev/Dev-Notes/raw/main/이미지%20참조/깃배쉬(Git%20Bash)%20브랜치%20사용하기/image%2026.png)

테스트할 저장소의 브랜치 정보를 확인하면 main까지 총 6개의 브랜치가 존재하는 것을 알 수 있다. 이어서 branch3 브랜치를 삭제한 후 다시 브랜치 정보를 확인해보면 정상적으로 삭제가 되고, 총 5개의 브랜치가 남아있게 되었다.
