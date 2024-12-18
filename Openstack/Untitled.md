Proces tworzenia nowej instancji (VM) w OpenStacku odbywa się za pomocą komponentu **Nova** (Compute) i składa się z kilku kroków. Poniżej przedstawiam szczegółowy przebieg tego procesu:

### **Podsumowanie kroków**

1. **Uwierzytelnienie** przez Keystone.
2. **Planowanie** przez Nova Scheduler.
3. **Rezerwacja zasobów** (CPU, RAM, Storage).
4. **Konfiguracja sieci** przez Neutron.
5. **Pobranie obrazu** z Glance.
6. **Uruchomienie instancji** przez Nova Compute.
7. **Inicjalizacja** za pomocą cloud-init.

