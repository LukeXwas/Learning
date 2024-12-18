Git fetch to komenda w Git, która służy do pobierania najnowszych zmian z zdalnego repozytorium (np. z GitHub, GitLab) bez automatycznego łączenia ich z lokalnymi gałęziami. Dzięki git fetch możesz zobaczyć, jakie zmiany pojawiły się na zdalnym repozytorium, zanim zdecydujesz, czy i jak chcesz je zintegrować ze swoim lokalnym kodem.

Przyklad:

1. Pobieranie zmian ze zdalnego repozytorium:

git fetch origin master

2. Sprawdzenie pobranych zmian:

git log origin/master

3. Po fetchu możesz zdecydować, czy zaktualizować lokalną gałąź:

git merge origin/main

**Git pull

Pobiera zmiany i automatycznie je łączy z twoją lokalną gałęzią (w praktyce jest to kombinacja git fetch + git merge





