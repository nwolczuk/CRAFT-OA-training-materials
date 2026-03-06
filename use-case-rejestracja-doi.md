# USE CASE - rejestracja DOI

Poniżej przedstawiamy opis kolejnych etapów pracy nad zadaniem dotyczącym nadawania numerów DOI archiwalnym artykułom jednego z polskich pism naukowych, które nie wykorzystywało w pracy żadnej platformy publikacyjnej. Opis ten dotyczy specyficznego przypadku, dla którego został przygotowany dedykowany skrypt programistyczny, z tego powodu proces może nie być w pełni replikowalny w innych przypadkach i może wymagać dopasowania do konkretnej sytuacji. Stanowi on jednak doskonały przykład prawdziwego zadania, które unaocznia potencjał drzemiący w metodach automatyzujących pracę.

Choć w przykładzie wykorzystano język programowania Python, nie trzeba posiadać umiejętności technicznych, by skorzystać z podobnych rozwiązań — często wystarczy współpraca z osobą techniczną lub sięgnięcie po gotowe narzędzia.

## Opis problemu

Celem zadania było rejestracja numerów DOI dla archiwalnych artykułów jednego z polskich pism naukowych. Rejestracji należało dokonać za pośrednictwem serwisu [CrossRef](https://www.crossref.org/).&#x20;

Z powodu braku możliwości technicznych po stronie redakcji pisma jedynym rozwiązaniem było manualne wprowadzanie danych za pomocą formularzy rejestracyjnych dostępnych na stronie (np. [webDeposit](https://apps.crossref.org/webDeposit/)). Wadą tego podejścia jest duża czasochłonność procesu, konieczność zaangażowania części redaktorów na dłuższy czas, oraz potencjalnie wysokie prawdopodobieństwo pomyłek podczas wprowadzania danych.&#x20;

W celu przyśpieszenia i ułatwienia prac zdecydowano się zlecić wykonanie skryptu, za pomocą którego możliwe będzie przesłanie paczki danych i hurtowa rejestracja elementów w nich zawartych. Dane należało przygotować w formacie XML zgodnie ze schematem metadanych przewidzianym przez CrossRef (w momencie pisania tekstu aktualna wersja schemat to [5.4.0](https://data.crossref.org/reports/help/schema_doc/5.4.0/index.html)), a następnie przesłać wykorzystąc API serwisu.

{% hint style="info" %}
Szczegółowe informacje o tym jak przygotować plik XML i jak zdeponować go w serwisie znajdziesz w [dokumentacji CrossRef](https://www.crossref.org/documentation/register-maintain-records/direct-deposit-xml/).
{% endhint %}

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption><p>Diagram przepływu danych w opiswyanym zadaniu</p></figcaption></figure>

Zaletą tego podejścia jest jednorazowy nakład pracy. Po opracowaniu skryptu jest on gotowy do użycia wielokrotnie, o ile nie zostaną wprowadzone istotne zmiany po stronie odbiorcy danych. Rozwiązanie to oszczędza czas i nakład pracy redaktorów, oraz zmniejsza prawdopodobieństwo wystąpienia błędów. Tak przygotowane narzędzia zapewniają powtarzalność, przy założeniu, że trzymamy się instrukcji ich używania.

### Podsumowanie korzyści:

✅  **szybszy proces i/lub mniej zaangażowanych osób**

✅ **mniej potencjalnych błędów**

✅  **skalowalność rozwiązania**

✅  **możliwość ponownego wykorzystania**

## Pozyskanie i czyszczenie danych

Pracę nad tym zadaniem podzielić można na dwa etapy, pierwszym z nich jest przygotowanie metadanych, które mają zostać przesłane podczas rejestracji DOI. Metadane nie były udostępnione w przez redakcję, należało pozyskać je z repozytorium, w którym są zdeponowane artykuły.&#x20;

Metadane pozyskano za pomocą protokołu OAI-PMH, a następnie poddano manualnej korekcie tam, gdzie jakość danych nie spełniała wymaganych kryteriów.

{% hint style="info" %}
Więcej o protokole wymiany metadanych OAI-PMH dowiesz się [tutaj](https://www.openarchives.org/pmh/).
{% endhint %}

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption><p>Fragment przykładowego rekordu pochodzącego z repozytorium i udostępnianego przez OAI-PMH.</p></figcaption></figure>

Korekta danych wykonywana była z użyciem arkuszy kalkulacyjnych. Poniżej przedstawiono fragment tabeli z danymi, gdzie każdy wiersz odpowiada jednemu artykułowi. Treści przygotowano tak, aby nie wymagały żadnych kolejnych przetworzeń i oczyszczeń. Nagłówki kolumn oznaczono nazwami odpowiadającymi tagom, w których powinny znaleźć się dane w strukturze pliku XML.

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption><p>Fragment tabeli z ustrukturyzowanymi metadanymi rekordów.</p></figcaption></figure>

## Przygotowanie skryptu i przesłanie danych

Po przygotowaniu danych wejściowych opracowano skrypt w języku Python. Skrypt miał za zadanie dla każdego rocznika pisma automatycznie stworzyć plik XML z metadanymi artykułów do rejestracji, a następnie zdeponować go w serwisie CrossRef za pomocą API. Każdy z plików był następnie weryfikowany i przetwarzany po stronie serwera, co trwało od kilkunastu do kilkudziesięciu minut, by ostatecznie przydzielić wszystkim obiektom numery DOI.

Poniżej przedstawiono fragment kodu w Pythonie, który tworzy jeden z elementów pliku XML na bazie wierszy z tabeli opisywanej wcześniej. Elementy są ustrukturyzowane i łatwo wprowadzić w nich zmiany, gdyby dane wejściowe lub docelowy format się zmieniły.&#x20;

```python
def create_person_metadata(row):
    if row['ORCID']: orcid = 'https://orcid.org/' + row['ORCID']
    else: orcid = ''
    return E.person_name(
                            E.given_name(row['given_name']),
                            E.surname(row['surname']),
                            E.ORCID(orcid),
                            sequence=row['sequence'],
                            contributor_role=row['contributor_role']
                        )
```

Całość skryptu zbudowana jest sekcji odpowiedzialnych za poszczególne wymagane działania. Sekcja odpowiedzialna za stworzenie pliku XML podzielona jest na funkcje tworzące poszczególnych części metadanych (przykład takiej funkcji znajduje się powyżej). Następnie efekt pracy każdej z funkcji jest łączony w całość i zapisywany lokalnie. Pliki można poddać manualnej weryfikacji, aby następnie przesłać je na serwer za pomocą pozostałej części kodu.

{% hint style="info" %}
Pliki można wysłać najpierw na serwer testowy, aby sprawdzić jak będzie przebiegać proces rejestracji.
{% endhint %}

Całość skryptu, również z danymi wejściowymi, znajduje się pod tym linkiem: [https://github.com/CHC-Computations/CRAFT-OA-training-materials/tree/main/DOI\_Crossref\_registration](https://github.com/CHC-Computations/CRAFT-OA-training-materials/tree/main/DOI_Crossref_registration).

Poniżej zaprezentowano fragment efektu prac, czyli jeden z rekordów wyswietlany przez serwis CrossRef wraz z nadanym numerem DOI.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption><p>Jeden z zarejestrowanych rekordów w wynikach wyszukiwania serwisu CrossRef.</p></figcaption></figure>

## Wnioski

Opisany przypadek pokazuje, że nawet redaktorzy, którzy nie korzystają z nowoczesnych platform wydawniczych, mogą znacząco usprawnić swoją pracę dzięki prostym narzędziom do automatyzacji. Stworzenie dedykowanego skryptu pozwoliło nie tylko przyspieszyć cały proces rejestracji DOI, ale również zmniejszyć liczbę błędów i odciążyć redakcję od czasochłonnych zadań.

Rozwiązania tego typu nie zawsze muszą być tworzone od podstaw - w wielu przypadkach wystarczą gotowe narzędzia lub zewnętrzna pomoc techniczna. Kluczem jest dostrzeżenie potencjału w danych i procesach, które do tej pory były wykonywane ręcznie, i zastanowienie się, gdzie warto je zautomatyzować.

Warto traktować takie przykłady jako inspirację do poszukiwania usprawnień we własnych działaniach.
