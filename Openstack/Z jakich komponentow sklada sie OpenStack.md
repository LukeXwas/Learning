OpenStack składa się z wielu komponentów (usług), które współpracują ze sobą, aby zapewnić pełną funkcjonalność chmury obliczeniowej. Oto główne komponenty OpenStacka:

### 1. **Compute (Nova)**

- Odpowiada za zarządzanie maszynami wirtualnymi (VM). Nova obsługuje orkiestrację tworzenia, planowania i zarządzania instancjami.

### 2. **Networking (Neutron)**

- Zapewnia elastyczne zarządzanie siecią i IP dla instancji. Obsługuje różne topologie sieciowe, takie jak sieci prywatne, VLAN, VXLAN, SDN (Software-Defined Networking).

### 3. **Storage:**

- **Block Storage (Cinder)** – Umożliwia tworzenie i zarządzanie wolumenami blokowymi (dyski dla instancji VM).
- **Object Storage (Swift)** – Odpowiada za przechowywanie danych w postaci obiektów, podobnie jak Amazon S3.
- **Shared File Systems (Manila)** – Udostępnia współdzielone systemy plików dla instancji.

### 4. **Identity Service (Keystone)**

- Zarządza uwierzytelnianiem i autoryzacją użytkowników oraz usług OpenStacka.

### 5. **Image Service (Glance)**

- Umożliwia zarządzanie obrazami systemów operacyjnych używanych do uruchamiania instancji VM.

### 6. **Dashboard (Horizon)**

- Graficzny interfejs użytkownika (GUI) do zarządzania usługami OpenStacka.

### 7. **Orchestration (Heat)**

- Narzędzie do automatycznego wdrażania aplikacji i zasobów na podstawie szablonów.

### 8. **Telemetry (Ceilometer)**

- Zbiera dane o wydajności i zużyciu zasobów do monitorowania i rozliczeń.

### 9. **Placement**

- Odpowiada za planowanie zasobów i przydzielanie ich instancjom na podstawie dostępności.

### 10. **Database Service (Trove)**

- Umożliwia zarządzanie bazami danych jako usługą (DBaaS).

### 11. **DNS Service (Designate)**

- Zapewnia zarządzanie DNS jako usługą.

### 12. **Bare Metal Service (Ironic)**

- Umożliwia wdrażanie systemów operacyjnych bezpośrednio na fizycznych serwerach (bare-metal).

### 13. **Secrets Management (Barbican)**

- Umożliwia zarządzanie tajnymi danymi, takimi jak klucze szyfrowania.

### 14. **Container Orchestration (Magnum)**

- Zapewnia zarządzanie klastrami kontenerów, np. Kubernetes czy Docker Swarm.

### 15. **Load Balancer (Octavia)**

- Zarządza równoważeniem obciążenia dla aplikacji działających w OpenStacku.