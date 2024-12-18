Git rebase to komenda w Git, która służy do zmiany podstawy (bazy) bieżącej gałęzi na inną gałąź. Zamiast tworzyć nowy commit scalający, jak robi to git merge, git rebase przepisuje historię commitów, odtwarzając je na szczycie innej gałęzi. Proces ten polega na wzięciu serii commitów z bieżącej gałęzi i ponownym zastosowaniu ich (jeden po drugim) na nowej bazie.

Przyklad:

mkdir -p /tmp/test && cd /tmp/test

git init

git status

git branch --show-current

\> test1.txt && git add . && git commit -m "Add test 1"

git branch test

\> test2.txt && git add . && git commit -m "Add test 2"

git log

git checkout test

\> test3.txt && git add . && git commit -m "Add test 3"

git log && git log master

git branch --show-current

git rebase master

git log


