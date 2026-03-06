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

### **Walidacja i standaryzacja metadanych – skrypty Python + biblioteka Pandas**

**Przykładowe zastosowanie:**

Walidacja poprawności DOI i ORCID w pliku eksportu z OJS (zakładamy, że plik articles.csv posiada kolumny DOI i ORCID):

```python
import pandas as pd
import re

df = pd.read_csv("articles.csv")

def validate_doi(doi):
    return bool(re.match(r"^10\.\d{4,9}/[-._;()/:A-Z0-9]+$", doi, re.I))

def validate_orcid(orcid):
    return bool(re.match(r"^https?://orcid\.org/\d{4}-\d{4}-\d{4}-\d{4}$", orcid))

df["DOI_status"] = df["DOI"].apply(lambda x: "OK" if validate_doi(str(x)) else "Invalid")
df["ORCID_status"] = df["ORCID"].apply(lambda x: "OK" if validate_orcid(str(x)) else "Invalid")

df.to_excel("validated_articles.xlsx", index=False)

```

{% hint style="info" %}
Możesz wypróbować powyższy fragment kodu korzystając z [Google Colab ](https://colab.research.google.com/)(konieczne jest posiadanie konta Google) lub korzystając z [Jupyter Lab](https://jupyter.org/try).
{% endhint %}

### ETL – ekstrakcja, transformacja i ładowanie danych

Poniżej zaprezentowane jest przykładowe wykorzystanie Pythona oraz zapytania SQL do wygenerowania raportu, który pokaże listę artykułów z tytułami i datami zgłoszenia — tylko w języku angielskim.

Bazą SQL, którą odpytamy może być na przykład baza MySQL powiązana z oprogramowaniem OJS.

**Przykład zapytania SQL:**

```sql
SELECT 
    s.submission_id, 
    s.date_submitted, 
    ps.setting_value AS title
FROM 
    submissions s
JOIN 
    publications p ON s.current_publication_id = p.publication_id
JOIN 
    publication_settings ps ON p.publication_id = ps.publication_id
WHERE 
    ps.setting_name = 'title' 
    AND ps.locale = 'en_US';
```

**To zapytanie zwraca:**

* ID artykułu
* Datę zgłoszenia
* Tytuł w języku angielskim

**Skrypt w Pythonie łączący się z bazą SQL i generujący raport na bazie powyższego zapytania**

```python
import pandas as pd
import mysql.connector

# Konfiguracja połączenia z bazą danych OJS
conn = mysql.connector.connect(
    host="localhost",
    user="ojs_user",
    password="twoje_haslo",
    database="ojs"
)

# Zapytanie SQL
query = """
SELECT 
    s.submission_id, 
    s.date_submitted, 
    ps.setting_value AS title
FROM 
    submissions s
JOIN 
    publications p ON s.current_publication_id = p.publication_id
JOIN 
    publication_settings ps ON p.publication_id = ps.publication_id
WHERE 
    ps.setting_name = 'title' 
    AND ps.locale = 'en_US';
"""

# Wczytanie danych do DataFrame
df = pd.read_sql(query, conn)

# Zapisz jako plik Excel
df.to_excel("raport_artykulow.xlsx", index=False)

# Zamknij połączenie
conn.close()

print("Raport został zapisany jako 'raport_artykulow.xlsx'")
```

**Jeżeli chcesz zapoznać się z przykładem zadania, w którym wykorzystano skrypt w Pythonie w celu rejestracji numerów DOI dla archiwalnych artykułów, przejdź do sekcji poniżej.**

{% content-ref url="../../use-case-rejestracja-doi.md" %}
[use-case-rejestracja-doi.md](../../use-case-rejestracja-doi.md)
{% endcontent-ref %}
