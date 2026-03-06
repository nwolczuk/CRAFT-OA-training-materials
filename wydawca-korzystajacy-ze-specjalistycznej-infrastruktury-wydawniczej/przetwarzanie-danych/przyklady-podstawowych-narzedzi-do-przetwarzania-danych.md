# Przykłady podstawowych narzędzi do przetwarzania danych

W pracy z danymi – czy to przy zarządzaniu zgłoszeniami, tworzeniu raportów, czy analizach – warto korzystać z dostępnych narzędzi, które mogą znacznie uprościć i usprawnić te procesy. Poniższe przykłady pokazują, co można osiągnąć przy użyciu popularnych i często bezpłatnych rozwiązań, takich jak arkusze kalkulacyjne czy narzędzia do czyszczenia danych.

Nie jest to instrukcja obsługi, lecz zarys możliwości – pomocny przy wyborze podejścia dostosowanego do własnych potrzeb. Celem jest pokazanie potencjału narzędzi, które mogą podnieść jakość danych i zautomatyzować część pracy.

### Arkusze kalkulacyjne

To narzędzia łatwo dostępne i intuicyjne, idealne do prostego porządkowania, filtrowania i analizowania danych. Sprawdzają się szczególnie dobrze przy pracy z mniejszymi zbiorami, umożliwiają szybkie wykrywanie braków, tworzenie zestawień czy generowanie raportów.

Przykłady oprogramowania do pracy z arkuszami:

1. Google Sheets
2. Excel
3. LibreOffice Calc

#### Co można zrobić?

* Uporządkować dane zgłoszeń (np. imiona i nazwiska, afiliacje, ORCID).
* Automatycznie wykrywać i oznaczać braki (np. brak DOI, brak recenzenta).
* Tworzyć raporty do PDF lub Google Docs.

#### Przykład działania:

1. **Import danych z pliku CSV (np. eksport z OJS):**
   * Excel: zakładka „Dane” → „Z pliku tekstowego” → Power Query → załaduj dane i przekształć kolumny.
   * Google Sheets: Plik → Importuj → CSV.
2. **Dodanie kolumny z automatycznym sprawdzaniem poprawności formatu DOI (Google Sheets)**:

Zakładając, że nasze dane zawierają w kolumnie C informację o DOI, który najczęściej ma następujący format 10.xxxx/xxxxx, możemy sprawdzić ich poprawność z wykorzystaniem wyrażeń regularnych (RegEx, język znaczników służący do wyszukiwania wzorców).

```excel-formula
=IF(REGEXMATCH(C2, "^10\.\d{4,9}/[-._;()/:A-Z0-9]+$"), "OK", "Niepoprawny DOI")
```

{% hint style="info" %}
`^10\.` – zaczyna się od „10.”

`\d{4,9}` – 4 do 9 cyfr

`/...` – ukośnik, po którym może być ciąg znaków: litery, cyfry, znaki specjalne

`REGEXMATCH` zwraca `TRUE` lub `FALSE`
{% endhint %}

### Narzędzia do czyszczenia i eksploracji danych - [OpenRefine](https://openrefine.org/)

Jest to narzędzie służące do oczyszczania, organizowania i przetwarzania danych. Pozwala na usuwanie duplikatów, konsolidowanie danych pochodzących z różnych źródeł oraz przekształcanie danych do odpowiednich formatów. Jego elastyczność sprawia, że nadaje się zarówno do prostych zadań, jak i bardziej skomplikowanych procesów związanych z przetwarzaniem danych. Dzięki OpenRefine można poprawić jakość danych, usuwając błędy i niespójności, co wpływa na dokładność analiz i raportów.

**Co można zrobić?**

* Ujednolicić nazwy instytucji i autorów.
* Wyszukać i poprawić niejednolite afiliacje.
* Zidentyfikować duplikaty zgłoszeń lub autorów.

**Przykład działania:**

1. **Import danych z CSV**:
   * Otwórz OpenRefine → Nowy projekt → wybierz plik CSV z metadanymi.
2. **Fasetowanie i grupowanie danych**:
   * Wybierz kolumnę „Afiliacja” → „Facet” → „Text Facet” → zobacz wszystkie unikalne wartości.
   * Scal podobne (np. „Uniwersytet Warszawski” i „UW”) przez „Cluster and Edit”.
3. **Eksport danych**:
   * Po zakończeniu → „Export” → CSV → dane gotowe do załadowania z powrotem do arkusza.

{% hint style="info" %}
Szczegółowe informacje i przykłady użycia znajdziesz w oficjalnej dokumentacji OpenRefine: [https://openrefine.org/docs](https://openrefine.org/docs).
{% endhint %}
