Ansible działa jako narzędzie do automatyzacji konfiguracji serwerów poprzez deklarowanie żądanych stanów systemu w plikach YAML zwanych _playbookami_. Jest bezagentowe, co oznacza, że nie wymaga instalowania dodatkowego oprogramowania na zdalnych hostach — korzysta z protokołu SSH do komunikacji z nimi.

**Architektura Ansible

- **Kontroler (Control Node)**: Maszyna, na której instalujesz Ansible i z której zarządzasz konfiguracjami.
- **Zdalne hosty (Managed Nodes)**: Serwery, które konfigurujesz i zarządzasz za pomocą Ansible.
- **Playbooki**: Pliki YAML definiujące zadania (tasks), które Ansible ma wykonać.
- **Inventory**: Lista hostów i grup hostów, na których Ansible wykonuje operacje. Może być plikiem statycznym (`inventory.ini`) lub dynamicznym.
- **Moduły**: Gotowe funkcje w Ansible, które wykonują konkretne zadania, np. instalowanie pakietów, modyfikowanie plików, zarządzanie użytkownikami.

![[Pasted image 20241218200923.png]]

**Jak dziala?

1. **Tworzenie Inventory**
2. **Pisanie Playbooka
3. **Wykonanie Playbooka
4. **Ansible wykonuje zadania**:  Ansible łączy się przez SSH z każdym hostem zdefiniowanym w inventory i wykonuje po kolei zadania z playbooka.
5. **Logowanie i raportowanie**: Po wykonaniu playbooka Ansible zwraca szczegółowe informacje o każdym kroku, co ułatwia debugowanie.

**Zalety użycia Ansible do konfiguracji serwera

1. **Bezagentowość**: Nie wymaga instalacji agenta na zdalnych serwerach, wystarczy SSH i Python.
2. **Idempotencja**: Ansible sprawdza stan serwera przed wykonaniem zadania, aby uniknąć powtarzania działań, które już zostały wykonane.
3. **Deklaratywność**: Opisujesz pożądany stan systemu, a nie konkretne kroki.
4. **Łatwość użycia**: Proste składnie YAML oraz bogata biblioteka gotowych modułów.
5. **Skalowalność**: Możliwość zarządzania setkami lub tysiącami serwerów jednocześnie.