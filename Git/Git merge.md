
**Git merge** to komenda służąca do łączenia zmian z różnych gałęzi w repozytorium Git. Działa poprzez analizę dwóch gałęzi: aktualnie wybranej oraz tej, którą chcemy do niej scalić. Gdy wykonujemy git merge, Git znajduje wspólnego przodka (punkt w historii, od którego obie gałęzie zaczęły się rozchodzić), porównuje zmiany w obu gałęziach i łączy je w jedną całość. W efekcie powstaje nowy commit scalający, który zawiera pełną historię z obu gałęzi.

**Git merge trójstronny

**Git merge - fast-foward

Scalana gałąź nie tworzy żadnej alternatywnej historii w stosunku do gałęzi głównej, gałęzie nie rozrosły się na dwa różne sposoby. Scalana gałąź jest prostą (liniową) kontynuacją gałęzi głównej. Albo jeszcze inaczej: feature kontynuuje wzrost master, master wskazuje na pewne miejsce w historii wzrostu feature. Zamiast więc tworzyć niepotrzebne byty, wystarczy zmienić czubek master — przesunąć ref (jakim jest master) wzdłuż linii zmian wyznaczonej przez feature. Po takiej akcji gałąź feature jest wcielona do gałęzi master, obie głęzie wskazują ten sam commit.

Przyklad fast-foward

mkdir -p /tmp/test && cd /tmp/test

git init

echo > test.txt

git add . && git commit -m "Add test 1"

git log

git branch test

echo > test.txt

git add . && git commit -m "Add test 2"

git log

git checkout master 

git merge test

git log

