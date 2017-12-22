# git rebase

### Обновление своей ветки до master
```
  master
    ↓
A ← B
 ↖
  C ← D ← E
          ↑
       feature
          ↑
        HEAD
```
`feature> git rebase master`
```
  master
    ↓
A ← B
     ↖
      C' ← D' ← E'
                ↑
             feature
                ↑
              HEAD
```
При возникновении кофликта разрешить его в merge tool, добавить в стейдж `git add %` и продолжить `git rebase --continue`. Если изменений в рабочей копии нет - то _continue_ не сработает, нужно пропустить шаг `git rebase --skip`. Если нужно прервать операцию - выполнить `git rebase --abort`.

### Обновление из remote

`git pull --rebase origin master`

### Передача в remote

`git push origin feature --force`

### Интеграция в основную ветку

`get merge --no-ff`

