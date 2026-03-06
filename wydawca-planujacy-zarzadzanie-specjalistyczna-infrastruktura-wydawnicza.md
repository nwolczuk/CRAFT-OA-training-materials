---
icon: face-monocle
---

# Wydawca planujący zarządzanie specjalistyczną infrastrukturą wydawniczą

Proces przechodzenia na samodzielnie zarządzaną infrastrukturę publikacyjną to nie tylko decyzja technologiczna, ale przede wszystkim transformacja operacyjna i organizacyjna. Aby zmiana była skuteczna i przyniosła długofalowe korzyści, warto zadbać o kilka strategicznych obszarów:

#### 1. **Opracowanie realistycznej mapy transformacji**

Zanim organizacja podejmie działania techniczne, konieczne jest przygotowanie szczegółowej mapy przejścia. Powinna ona zawierać:

* audyt obecnej infrastruktury i zależności (hosting, systemy zarządzania, zewnętrzne API),
* zidentyfikowanie komponentów, które można przejąć wewnętrznie (np. system publikacyjny, zarządzanie użytkownikami),
* określenie, które usługi będą wymagały stopniowego uniezależnienia (np. DOI, backup, support techniczny).

{% hint style="info" %}
Wydawca korzystający z zewnętrznego hostingu OJS może najpierw uruchomić testową instancję OJS na własnym serwerze, aby zbudować kompetencje przed migracją produkcyjną.
{% endhint %}

#### 2. **Budowanie wewnętrznych kompetencji technicznych**

Przejście na własną infrastrukturę nie musi oznaczać od razu pełnego zespołu IT, ale powinno zakładać:

* zatrudnienie (lub rozwinięcie) osoby technicznej znającej podstawy administrowania systemami Linux, bazami danych i PHP (OJS),
* rozwijanie podstawowej znajomości systemów wersjonowania (np. Git) i struktur pluginowych,
* inwestycję w szkolenia i dokumentację — zarówno wewnętrzną, jak i korzystanie z zasobów społeczności open source (PKP Docs, PKP Forum).

{% hint style="info" %}
Zespół redakcyjny nie musi być techniczny, ale powinien rozumieć strukturę pracy systemu i wiedzieć, które procesy można automatyzować.
{% endhint %}

#### 3. **Stopniowe przejmowanie odpowiedzialności za komponenty systemu**

Nie ma konieczności budowania wszystkiego od razu. Warto zacząć od:

* zarządzania konfiguracją systemu (np. `config.inc.php` w OJS),
* samodzielnej aktualizacji oprogramowania (np. upgrade do najnowszej wersji OJS),
* integracji oficjalnych pluginów (Crossref, ORCID, XML export),
* testowania lokalnych modyfikacji na środowisku deweloperskim.
