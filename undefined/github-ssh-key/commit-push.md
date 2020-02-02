# commit, push

## Git

![](../../.gitbook/assets/image%20%287%29.png)





**commit**

로컬 저장소로 소스코드를 올립니다. 원격 저장소까지 올라가지는 않기 때문에 github 페이지에서 확인할 수 없습니다.

**push**

로컬 저장소의 소스를 원격 저장소로 올립니다. push 후에 github 페이지에서 확인이 가능합니다

![](../../.gitbook/assets/image%20%2824%29.png)

**pull**

원격 저장소의 소스를 로컬 컴퓨터로 가져옵니다

![](../../.gitbook/assets/image%20%2818%29.png)



**branch**

branch 를 이용하면 작업공간을 분리할 수 있습니다.

**merge**

branch 끼리 합치는 행위를 merge 라고 합니다

![](../../.gitbook/assets/image%20%281%29.png)

**pull Request**

pull Request 를 통하는 branch 는 바로 merge 되지 않습니다.  
merge 위한 과정에 대한 논의를 할 수 있습니다.

### 실습

1. 먼저 git repository 를 생성합니다.
2. 만들어진 git repo 를 `git clone` 명령어를 이용하여 local 에 생성합니다. ssh 등록을 했다면 ssh url 을 이용합니다

![](../../.gitbook/assets/image%20%288%29.png)

```text
$ git clone <본인 repo url>
```

1. root path 에 `README.md` 파일을 생성합니다.

```text
# Javascript PalyGround
```

1. `git add` 명령어를 이용하여 우리가 만든 파일을 git 관리 대상으로 추가합니다. 후 `status` 명령어를 이용하여 추가가 잘 되었는지 확인합니다.

```text
$ git add .
$ git status 
```

1. `git commit` 명령어를 이용하여 우리가 작업한 내용에 대한 설명을 추가합니다. `log` 명령어를 이용하여 메세지를 확인합니다.

```text
$ git commit -m "README.md 파일 추가"
$ git log 
```

```text
Author: olaf <appear.ko@gmail.com>
Date:   Sat Jul 13 21:02:41 2019 +0900

    README.md 파일 추가
```

1. `git push` 명령어를 이용하여 작업한 내용들을 marster remote 서버에 추가합니다.

```text
$ git push origin master
```

![](../../.gitbook/assets/image%20%2820%29.png)

1. branch 추가해보겠습니다. master 를 본딴 새로운 공간을 생성합니다. `-b` 옵션은 새로운 브렌치를 생성합니다. 이미 존재하는 브렌치라면 생략가능합니다. branch 명령어를 이용하여 현재 어디 브렌치에 있는지 알 수 있습니다.

```text
$ git checkout -b add-week-folder
$ git branch
```

```text
* add-week-folder
  master
```

1. 1\_week 폴더를 생성합니다. 1\_week 폴더 안에 README.md 파일을 추가합니다.

```text
# 1 주차 스터디
```

1. `git add .` 명령어를 이용하여 git 의 관리대상으로 추가합니다.

```text
$ git add .
```

1. `git commit` 명령어를 이용하여 작업 내용을 추가합니다.

```text
$ git commit -m "1_week 폴더 추가"
```

1. `git push` 명령어를 이용하여 remote 서버에 추가할건데 master 로 바로 올리지 않습니다. 우리가 만든 브렌치에 추가합니다.

```text
$ git push origin add-week-folder
```

![](../../.gitbook/assets/image%20%2811%29.png)



![](../../.gitbook/assets/image%20%2810%29.png)

1. 메인 페이지로 가보시면 어떠한 브렌치에 작업이 생겼다는것을 알려줍니다. 오른쪽의 초록버튼 compare & pull request 라는 버튼을 눌러 pull request 를 생성할거에요



왼쪽이 합쳐질 곳 오른쪽이 합칠 대상 입니다. 즉 add-week-folder 브렌치를 master 브렌치로 합치겠다라는 것 입니다.  
합쳐지기전까지는 master 에 우리가 작업한 내용이 추가되지 않습니다. 분리된 공간에 추가를 했기 때문입니다.

아래 초록색 버튼을 클릭하여 pull request 를 생성합니다.

1. merge 버튼을 클릭하여 우리가 작업한 내용을 master 에 합쳐줍니다

![](../../.gitbook/assets/image%20%2813%29.png)

