# git rebase

## Испольхование _rebase_ для поддержания акутальности своей ветки

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
При возникновении кофликта  - разрешить его в merge tool, добавить в стейдж: `git add %` и продолжить: `git rebase --continue`. Если изменений в рабочей копии нет - то _continue_ не сработает, нужно пропустить шаг: `git rebase --skip`. Если нужно прервать операцию - выполнить `git rebase --abort`.

### Обновление из remote

`git pull --rebase origin master`

### Передача в remote

`git push origin feature --force`

### Интеграция в основную ветку

`get merge --no-ff`

### Источник

https://habrahabr.ru/post/161009/

## Использование _rebase_ для объединения коммитов в один

Посмотреть, какие коммиты прибавились по сравнению с master: `git cherry -v master` (или просто их количество - `git cherry -v master | wc -l`), затем сделать интерактивный ребейз желаемого кол-ва коммитов: `git rebase -i HEAD~N`

Отредактировать то, что показали в редакторе
```
pick 1111111
squash 2222222
squash 3333333
```
затем отредактировать комментарий к результирующему коммиту. Можно просто использовать новейший коммент (`fixup` вместо `squash`). Запушить насильно: `git push --force`.

### Источник

https://htmlacademy.ru/blog/27-how-to-squash-commits-and-why-it-is-needed

----
