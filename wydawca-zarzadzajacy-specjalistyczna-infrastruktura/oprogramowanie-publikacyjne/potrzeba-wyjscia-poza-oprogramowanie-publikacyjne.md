# Potrzeba wyjścia poza oprogramowanie publikacyjne

Choć systemy publikacyjne są niezwykle rozbudowane i bogate w funkcjonalności, w wielu przypadkach ograniczeniem jest **brak elastycznego dostępu do danych w czasie rzeczywistym**, **ograniczona personalizacja raportów**, lub **brak zaawansowanych narzędzi wizualizacji**.&#x20;

Choć systemy takie jak OJS oferują podstawowe funkcje raportowania i statystyk, w codziennej pracy redakcji — a szczególnie przy zarządzaniu większą liczbą czasopism — często pojawia się potrzeba **szybkiego dostępu do danych w bardziej elastycznej, przejrzystej i interaktywnej formie**. Ograniczeniem jest również, **ograniczona personalizacja raportów**, lub **brak zaawansowanych narzędzi wizualizacji**.  Tu z pomocą przychodzi dashboard zbudowany w Google Sheets (lub Excelu), który pełni rolę **zewnętrznego interfejsu analitycznego**.

#### Główne ograniczenia systemowe:

* Brak interaktywnych pulpitów zarządzania (dashboardów),
* Raportowanie ograniczone do sztywnych szablonów (lub jego całkowity brak),
* Konieczność ręcznego eksportowania danych (np. CSV lub XML),
* Niski poziom integracji z BI (Business Intelligence) oraz narzędziami chmurowymi.

W praktyce oznacza to, że zarządzający infrastrukturą muszą aktywnie **tworzyć „pomosty technologiczne”** – narzędzia, które umożliwiają:

* przetwarzanie danych poza systemem (ETL – Extract, Transform, Load),
* integrację z systemami raportowania instytucjonalnego,
* przejrzystą prezentację danych operacyjnych i statystycznych redakcji.

#### **Zalety zastosowania dashboardu**

1. **Centralizacja informacji**
   * Możesz zestawić w jednym miejscu dane z wielu czasopism lub wielu źródeł (np. OJS, repozytorium, ORCID).
   * W prosty sposób zyskujesz widok przekrojowy (cała instytucja) oraz szczegółowy (pojedynczy tytuł).
2. **Dostępność i współdzielenie**
   * Dashboard może być współdzielony z redaktorami, dyrekcją wydawnictwa, biblioteką czy partnerami instytucjonalnymi.
   * Możliwość ograniczenia uprawnień tylko do odczytu.
3. **Automatyzacja aktualizacji**
   * Dzięki integracji z API OJS (lub prostym eksportom CSV z bazy danych), dane mogą być automatycznie odświeżane.
   * Harmonogramy aktualizacji (np. co 24h) zapewniają aktualność raportów bez konieczności ręcznej ingerencji.
4. **Interaktywność i wizualizacja**
   * Dashboard może zawierać wykresy, mapy, filtry, pola wyboru czasopisma, zakresów dat itp.
   * Możliwość budowania dynamicznych KPI (średni czas recenzji, liczba zgłoszeń w danym okresie, odsetek artykułów bez DOI).

**Kliknij poniżej i sprawdź jak wygląda przykładowy prosty dashboard w Google Sheets.**

{% content-ref url="../../use-case-dashboard-w-google-sheets.md" %}
[use-case-dashboard-w-google-sheets.md](../../use-case-dashboard-w-google-sheets.md)
{% endcontent-ref %}
