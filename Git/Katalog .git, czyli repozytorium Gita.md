
Repozytorium Gita to miejsce, gdzie Git przechowuje wszystko, czego potrze-
buje do zarządzania projektem. W szczególności w repozytorium przechowy-
wana jest cała historia projektu. Normalnie tym repozytorium jest podkatalog
.git, będący podkatalogiem śledzonego katalogu (projektu).

**Git przechowuje historię projektu w podkatalogu .git.**

- Usunięcie tego katalogu spowoduje usunięcie całej historii projektu.
- Skopiowanie tego katalogu to zrobienie kopii zapasowej całej historii projektu.

**Sam katalog .git to repozytorium Gita (ang. Git repository), czyli wszystko, co Git wie o projekcie, w szczególności historia projektu (cała). Jest to tzw. repozytorium lokalne. Lokalne, bo operujemy na nim jak na zwykłym katalogu lokalnym.

Jeśli pracujemy sami i chcemy tylko przechowywać historię projektu lokalnie, wówczas takie lokalne repozytorium to wszystko, czego nam potrzeba. Zazwyczaj jednak współpracujemy z kimś, współdzieląc wykonaną pracę. Takie współdzielenie to,technicznie rzecz biorąc, przesyłanie zapamiętanych wersji projektu pomiędzy kilkoma repozytoriami. 

**Tj. mogę do swojego repozytorium lokalnego pobrać (git fetch)
wersje zapamiętane przez współpracowników w ich repozytoriach (lokalnych z ichpunktu widzenia, zdalnych z mojego) oraz przesłać im (git push) wersje zapamiętane lokalnie u mnie (zdalne z ich punktu widzenia).**