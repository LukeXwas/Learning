Git cherry-pick to komenda w Git, która pozwala skopiować konkretny commit z jednej gałęzi do innej. Działa na poziomie pojedynczych commitów, umożliwiając przeniesienie wybranych zmian bez konieczności łączenia całych gałęzi.

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

git log && git log master

git branch --show-current

git cherry-pick \<sha-1 z mastera>

git log

 