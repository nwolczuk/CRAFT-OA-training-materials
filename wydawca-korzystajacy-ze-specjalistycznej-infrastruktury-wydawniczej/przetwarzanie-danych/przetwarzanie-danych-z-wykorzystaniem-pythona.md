# Przetwarzanie danych z wykorzystaniem Pythona

Poniższa sekcja jest zaproszeniem do świata Pythona - narzędzia, które może znacznie uprościć i zautomatyzować wiele zadań związanych z przetwarzaniem danych. Nie jest to pełnowymiarowy kurs programowania, ale przegląd praktycznych zastosowań, które pokazują, jak nawet proste skrypty mogą wspierać codzienną pracę. Jeśli dopiero zaczynasz swoją przygodę z Pythonem lub szukasz inspiracji dla własnych projektów, te przykłady mogą być dobrym punktem wyjścia.

## Python i Jupyter Lab/Google Colab

**Python** to język programowania ogólnego przeznaczenia, który jest popularny ze względu na swoją prostotę i czytelność.

[Jupyter Lab](https://jupyter.org/try) i [Google Colab](https://colab.research.google.com/) to środowiska interaktywne, które pozwalają tworzyć i wykonywać kod Pythona bezpośrednio w przeglądarce. Idealne do eksploracji danych, czyszczenia, raportowania i wizualizacji.

Typowe zadania, do których można wykorzystać skrypty w Pythonie:

* Walidacja i uzupełnianie metadanych (np. ORCID, DOI, afiliacje)
* Eksport danych do Crossref, PubMed, DOAJ
* Konwersja danych między systemami (np. z OJS do innej platformy)
* Automatyczne raportowanie i synchronizacja z API

### API systemów publikacyjnych (OJS, Crossref, ORCID)

Jednym z częstych działań, do którego wykorzystywany jest Python, to interakcja z API (Application Programming Interface) różnych serwisów. API umożliwia dostęp do danych z systemów takich jak OJS, Crossref czy ORCID w sposób programowy – bez potrzeby ręcznego przeszukiwania interfejsów.

**Przykłady wykorzystania API**

* Pobieranie danych o opublikowanych artykułach z OJS
* Weryfikowanie, czy każdy artykuł ma poprawny DOI (Crossref)
* Pobieranie danych ORCID autorów (np. afiliacje)

**Przykład sprawdzenia, czy wskazane DOI znajduje się w systemie Crossref przy użyciu języka Python i biblioteki `requests`**

```python
import requests

doi = '10.18778/8088-337-6'
response = requests.get(f"https://api.crossref.org/works/{doi}")
if response.status_code == 200:
    print("DOI poprawny")
else:
    print("DOI nie istnieje")
```

{% hint style="info" %}
Możesz wypróbować powyższy fragment kodu korzystając z [Google Colab ](https://colab.research.google.com/)(konieczne jest posiadanie konta Google) lub korzystając z [Jupyter Lab](https://jupyter.org/try).
{% endhint %}

Korzystając ze środowisk interaktywnych i języka Python można również:

* Przetwarzać pliki CSV z danymi redakcyjnymi.
* Tworzyć automatyczne raporty publikacyjne.
* Tworzyć wykresy: liczba zgłoszeń w miesiącu, liczba recenzji, itp.

**Przykład filtrowania i analizy danych**

Zakładając, że posiadamy plik CSV, który zawiera kolumnę **date\_submitted** z datami, możemy zwizualizować, ile zgłoszeń przypada na poszczególne miesiące.

```python
import pandas as pd
df = pd.read_csv('submissions.csv')
df['data'] = pd.to_datetime(df['date_submitted'])
df.groupby(df['data'].dt.month)['id'].count().plot(kind='bar')
```

**Filtrowanie artykułów bez DOI**:

Zakładając, że nasz arkusz posiada kolumnę **doi**, możemy łatwo odfiltrować artykuły, które nie posiadają nadanego numeru.

```python
bez_doi = df[df['doi'].isnull()]
print(bez_doi[['title', 'author', 'date_submitted']])
```

Rozwijając swoje umiejętności z zakresu używania Pythona i korzystania z API, można znacząco poszerzyć możliwości pracy z produkowanymi w trakcie procesu publikacyjnego danymi.

**Jeżeli chcesz zapoznać się z przykładem zadania, w którym wykorzystano skrypt w Pythonie w celu rejestracji numerów DOI dla archiwalnych artykułów, przejdź do sekcji poniżej.**

{% content-ref url="../../use-case-rejestracja-doi.md" %}
[use-case-rejestracja-doi.md](../../use-case-rejestracja-doi.md)
{% endcontent-ref %}
