# Git 원격 저장소 활용

Git 원격 젖아소 기능을 제공해주는 서비스는 `gitlab`,  `bitbucket`, `github` 등이 있다.

## 0. 원격 저장소 설정

```bash
$ git remote add origin {URL}
$ git remote add origin https://github.com/LimHyeonJin/TIL.git
```

* git, 원격 저장소를 추가(`add`)하고 `origin`이라는 이름으로 url으로 설정

  git아 원격저장소를 추가해줘 origin이라는 이름으로 url을

* 설정된 저장소를 확인하기 위해서는 아래의 명령어를 사용한다.

  ```bash
  $ git remote -v
  origin  https://github.com/LimHyeonJin/TIL.git (fetch)
  origin  https://github.com/LimHyeonJin/TIL.git (push)
  ```

  

## 원격 저장소에 `push`

```bash
$ git push -u origin master
Logon failed, use ctrl+c to cancel basic credential prompt.
Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 8 threads
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 43.89 KiB | 8.78 MiB/s, done.
Total 14 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/LimHyeonJin/TIL.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

