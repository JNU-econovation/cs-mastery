# Git

### 목차
* [Stash](stash)  

  
---  
  

# stash

> A 작업중 commit하지 않고 B작업을 하고 돌아와, 다시 작업을 이어가고 싶을 때 사용하는 기능  

 알고리즘 문제를 풀 때, 문제 번호별로 브랜치를 나누고 문제를 다 풀면, master에 합치는 과정으로 알고리즘 파일을 관리하고 있다. 문제를 푸는 도중에 풀리지 않아 멈춰 놓았다, 다른 문제를 푸려고 다른 브랜치를 파는 경우가 있었는데 이 때마다 풀던 알고리즘을 commit 하고 '푸는중'이라는 메세지를 남겼다. 깃을 배우다 보니 commit이 완성된 작업단위로 메세지를 남기는 것이 좋을 것 같아, 위의 방법을 해결할 기능을 찾던중 **stash**를 알게 되어 정리하고자 한다.  
 
1. git stash
   - `stash`명령을 사용하면 Working Directory에 작업중인 상황을 저장하게 된다.
   - `stash`를 하게 되면 이전 commit 상태로 HEAD가 돌아가게 된다.
2. git stash list
   - 여러번의 stash를 사용할 수 있다.
   - 이를 `git stash list`명령어로 확인 할 수 있다.
3. git stash apply
   - `git stash apply`명령어로 저장한 상태를 다시 불러 올 수 있다.
   - 저장된 상태가 여러개라면 인덱스를 통해 적용할 수 있다.  `git stash apply --index`
   - stash@{0} 형태의 아이디로 접근한 수 있다.
   - index를 입력하지 않은 경우 최근의 상태를 적용한다.
4. git stash drop
   - 원하지 않은 stash 상태를 제거 할 수 있다.
   - apply를 하더라도 stash 스택에서 제거되지 않기 때문에 제거 할 수 있다.
   - apply와 마찬가지로 stash id를 명시하지 않으면 최근의 stash가 삭제된다.
5. git stash save 명칭
   - 원하는 명칭으로 stash를 저장할 수 있다.  
   

![stashtest1](https://user-images.githubusercontent.com/24218456/49492325-2c339f00-f89b-11e8-89dd-eff211dd72e5.png)  

1. `git stash`로 working space에 아무것도 없을을 알 수 있다.
2. 작업후 StashTest.java 파일이 생성되었다.
3. BOJ_2017이라는 tag로 저장되었다.


![stashtest2](https://user-images.githubusercontent.com/24218456/49492326-2c339f00-f89b-11e8-847a-838c44bb5a52.png)  

1. `stash` 명령이후 working space가 비었음을 확인할 수 있다.
2. `git stash list`명령어로 BOJ_2017이라는 이름으로 stash에 상태가 저장되었음을 알 수 있다. 이전에 저장되었던 상태들도 총 4개가 저장되어 있었다.
3. `git stash apply stash@{0}`명령어를 사용하여 id가 stash@{0}인 stash를 불러왔다.
4. -a 다시 StashTest.java파일이 추가된 것을 확인할 수 있다.  


![stashtest3](https://user-images.githubusercontent.com/24218456/49492327-2c339f00-f89b-11e8-9ba1-74e1e41b6b3a.png)  

1. 총 4번의 drop을 하니 다섯번째에서는 더이상 파일이 존재하지 않다고 나온다.
2. git stash list를 확인하니 아무것도 나오지 않음을 알 수 있다.  
  
  
---


