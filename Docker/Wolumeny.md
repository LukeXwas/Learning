W Dockerze istnieją trzy główne rodzaje wolumenów do zarządzania danymi przechowywanymi w kontenerach. Każdy z nich ma swoje specyficzne zastosowania i cechy. Oto ich szczegółowy opis:
###### **Wolumen nazwany (named volumes)

Wolumeny Docker są zarządzane przez Dockera i przechowywane w katalogu Dockera (`/var/lib/docker/volumes`). Są najczęściej używane do trwałego przechowywania danych poza cyklem życia kontenera.

**Charakterystyka:

- Tworzone i zarządzane przez Docker.
- Łatwe do tworzenia, przenoszenia i kopiowania.
- Dane są przechowywane poza systemem plików kontenera.
- Mogą być współdzielone między wieloma kontenerami.

**Przykład użycia:

```bash
docker run -d -v myvolume:/app/data --name mycontainer nginx
```

To polecenie tworzy lub używa istniejącego wolumenu o nazwie myvolume i montuje go w kontenerze pod ścieżką /app/data.

---
###### **Wolumen wiązany (bind mounts)**

Wiązania pozwalają na montowanie dowolnej ścieżki z systemu plików hosta do kontenera. Dzięki temu kontener ma dostęp do danych z hosta w czasie rzeczywistym.

**Charakterystyka:

- Montują konkretną ścieżkę hosta do ścieżki w kontenerze.
- Bardziej elastyczne niż wolumeny Docker.
- Użytkownik musi dbać o lokalizację i zarządzanie danymi na hoście.
- Przydatne w procesie deweloperskim, gdzie potrzebna jest synchronizacja danych.

**Przykład użycia:

```bash
docker run -d -v /host/path:/container/path --name mycontainer nginx
```

To polecenie montuje katalog /host/path z hosta do /container/path w kontenerze.

---

###### **Wolumeny tymczasowe (tmpfs mount)**

Wolumeny **tmpfs** działają w pamięci RAM i nie zapisują danych na dysku. Są używane do przechowywania danych, które nie muszą być trwałe, np. plików tymczasowych lub buforów.

**Charakterystyka:

- Dane przechowywane tylko w pamięci RAM (znikają po zatrzymaniu kontenera).
- Bardzo szybki dostęp do danych.
- Przydatne, gdy nie potrzebujesz trwałości danych i chcesz uniknąć operacji dyskowych.

**Przykład użycia:

```bash
docker run -d --tmpfs /app/tmp:rw,size=64m --name mycontainer nginx
```

To polecenie tworzy wolumen **tmpfs** o rozmiarze 64 MB, montowany w **/app/tmp**  w kontenerze.

---
##### Podsumowanie

|Rodzaj wolumenu|Zastosowanie|Zalety|Wady|
|---|---|---|---|
|**Wolumen Docker**|Trwałe dane między restartami kontenerów|Proste zarządzanie, izolacja|Przechowywanie w katalogu Dockera|
|**Bind Mount**|Synchronizacja danych z hostem|Elastyczność, dostęp do plików hosta|Brak izolacji|
|**Tmpfs**|Dane tymczasowe w pamięci RAM|Szybkość, brak operacji dyskowych|Brak trwałości|
