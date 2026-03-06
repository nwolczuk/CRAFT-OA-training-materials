# USE CASE - dashboard w Google Sheets

Poniżej prezentujemy przykładowy dashboard stworzonego w Google Sheets na podstawie danych wyeksportowanych z systemu OJS. Celem tego przykładu jest pokazanie, jak w prosty sposób można przekształcić surowe dane redakcyjne w zestawienia i wizualizacje wspierające monitorowanie procesu publikacyjnego.

To nie jest gotowe rozwiązanie produkcyjne, lecz demonstracja możliwości. Poniżej znajdują się również krótkie opisy, jak wykonać poszczególne elementy prezentowanego dashboardu. Tego typu rozwiązania można z łatwością dostosować do własnych potrzeb i rozwijać je wraz z rosnącą skalą danych.

## Przykładowy Dashboard w Google Sheets bazujący na danych wyeksportowanych z OJS

{% embed url="https://docs.google.com/spreadsheets/d/1kTA3q4Yyj6LMntOV0jE1QIMD8BK4_wk3e3N_6ZoHQHo/" fullWidth="true" %}
Source: [https://docs.google.com/spreadsheets/d/1kTA3q4Yyj6LMntOV0jE1QIMD8BK4\_wk3e3N\_6ZoHQHo/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1kTA3q4Yyj6LMntOV0jE1QIMD8BK4_wk3e3N_6ZoHQHo/edit?usp=sharing)
{% endembed %}

### **1. Liczba zgłoszeń wg statusu**

#### **Cel:** Śledzenie bieżącego stanu zgłoszeń (np. "Submitted", "In Review", "Accepted", "Published").

#### **Jak wykonać:**

1. Przejdź do nowego arkusza `Dashboard`.
2. Wybierz: **Wstaw > Tabela przestawna**.
3. Źródło danych: cały zakres z arkusza z danymi (np. `Dane_OJS_Surowe!A1:A1000`).
4. W polach tabeli:
   * **Wiersze:** `Status`
   * **Wartości:** Zlicz dowolną kolumnę niepustą, np. `Submission ID` (ustaw agregację na "Licznik").
5. Na bazie tej tabeli przestawnej stwórz **wykres kolumnowy**:
   * Kliknij na tabelę > Wstaw > Wykres > Kolumnowy.
6. Dodaj tytuł wykresu: `Statusy zgłoszeń`.

### **2. Redaktorzy – liczba przypisanych zgłoszeń**

#### **Cel:** Weryfikacja obciążenia pracą poszczególnych redaktorów.

#### **Jak wykonać:**

1. Utwórz tabelę przestawną:
   * **Wiersze:** `"Given Name (Editor 1)"`, `"Family Name (Editor 1)"` (lub scal w jedną kolumnę przed analizą).
   * **Wartości:** `Submission ID` (licznik).
2. Wstaw **wykres słupkowy poziomy**, który pokaże obciążenie każdego redaktora.
3. Dodaj tytuł: `Liczba zgłoszeń przypisanych redaktorom`.

### **3. Udział zgłoszeń z uzupełnionym ORCID**

#### **Cel:** Ocena jakości metadanych i zgodności z wymaganiami w zakresie numerów ORCID.

#### **Jak wykonać:**

1.  W arkuszu pomocniczym dodaj kolumnę:

    ```excel-formula
    =IF(OR(ISBLANK(D2); D2 = ""); "Brak ORCID"; "ORCID OK")
    ```

    _(przy założeniu, że `D2` to komórka z `ORCID iD (Author 1)`)_
2. Stwórz tabelę przestawną z podsumowaniem:
   * Wybierz nową kolumnę ze statusem ORCID.
   * Policz dowolną spójną niepustą kolumnę, np. Submission ID.
3. Wstaw **wykres pierścieniowy** bazujący na  wcześniej wykonanej tabeli.
4. Dodaj tytuł: `Udział zgłoszeń z ORCID`.

### 4. Liczba zgłoszeń miesięcznie

#### Cel: Śledzenie liczby zgłoszeń w poszczególnych miesiącach.

#### Jak wykonać:

1. Dodaj kolumnę pomocniczą, aby wyodrębnić miesiąc i rok z daty przesłania:
   1. Zakładając, że daty przesłania znajdują się w kolumnie B, w kolumnie C wpisz:\
      `=TEXT(B2, "RRRR-MM")`. Formatuje to datę do postaci `2024-05`, umożliwiając grupowanie według miesiąca.
   2. Skopiuj formułę w dół kolumny.
2. Utwórz tabelę przestawną:
   1. Wybierz pełny zakres danych.
   2. Przejdź do **Wstaw** > **Tabela przestawna** i umieść ją w nowym arkuszu dla przejrzystości.
3. Skonfiguruj tabelę przestawną:
   1. **Wiersze**: Wybierz kolumnę pomocniczą z formatem "RRRR-MM" (np. kolumna C).
   2. **Wartości**: Użyj `Submission ID` (lub innej niepustej kolumny) i ustaw **Summarize by: COUNTA**.

Google Sheets automatycznie pogrupuje zgłoszenia po miesiącach.
