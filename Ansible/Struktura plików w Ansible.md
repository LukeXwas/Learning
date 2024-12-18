project/
│-- inventory/
│   ├── production
│   └── staging
│-- roles/
│   └── webserver/
│       ├── tasks/
│       │   └── main.yml
│       ├── handlers/
│       │   └── main.yml
│       ├── templates/
│       │   └── index.html.j2
│       ├── files/
│       │   └── example.conf
│       ├── vars/
│       │   └── main.yml
│       └── defaults/
│           └── main.yml
│-- group_vars/
│   ├── webservers.yml
│   └── dbservers.yml
│-- host_vars/
│   └── server1.example.com.yml
│-- playbooks/
│   ├── webserver.yml
│   └── dbserver.yml
│-- ansible.cfg
└-- site.yml

**Opis poszczególnych elementów

1. inventory
	1. Zawiera pliki `inventory` (inwentarz), które definiują grupy hostów i poszczególne maszyny.
Przykład `production.ini`:

\[webservers]
server1.example.com
server2.example.com

\[dbservers]
db1.example.com

2. **roles/
	1. Zawiera role, które pozwalają na podział konfiguracji na mniejsze, wielokrotnego użytku jednostki. Każda rola ma standardowy zestaw katalogów:
