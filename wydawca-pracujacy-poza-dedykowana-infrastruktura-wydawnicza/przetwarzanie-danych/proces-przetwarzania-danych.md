# Proces przetwarzania danych

Aby efektywnie wykorzystywać dane w analizach, raportach oraz procesach decyzyjnych w ramach prac w środowisku wydawnictwa naukowego, konieczne jest ich odpowiednie przygotowanie. Proces przetwarzania danych obejmuje kilka kluczowych etapów – od pozyskania danych ze źródeł, przez ich oczyszczenie, aż po transformację do formy użytecznej dla dalszych działań. Każdy z tych kroków wpływa bezpośrednio na jakość końcowych wyników oraz możliwość ich dalszego wykorzystania i interpretacji.

**Jak przebiega proces przetwarzania danych?**

1.  Ustalanie źródeł danych i dostęp do nich

    Pierwszym krokiem jest określenie, skąd będą pochodzić dane oraz zapewnienie odpowiedniego dostępu. Dla wydawców naukowych mogą to być:

    * Bazy danych naukowe (np. Scopus, Web of Science, PubMed).
    * Systemy zarządzania czasopismami (np. OJS – Open Journal Systems).
    * Repozytoria instytucjonalne (np. arXiv, Zenodo, Europe PMC).
    * Pliki CSV lub Excel zawierające informacje o artykułach i autorach.
    * API zewnętrznych usług (np. CrossRef API do pobierania DOI i metadanych publikacji).


2.  Czyszczenie i walidacja

    Dane pobrane z różnych źródeł często zawierają błędy i niespójności, dlatego wymagają dokładnego czyszczenia i walidacji.

    * Usuwanie duplikatów - Może się zdarzyć, że te same artykuły pojawiają się kilkukrotnie, np. w różnych bazach. Identyfikację duplikatów można wykonać na podstawie DOI, tytułu, autora i daty publikacji.
    * Obsługa brakujących wartości - Brakujące nazwiska autorów, daty publikacji czy afiliacje mogą wpływać na analizy. Można je uzupełniać na podstawie innych źródeł (np. CrossRef API).
    * Wykrywanie i usuwanie anomalii - Typowym przykładem anomalii w danych są błedne wartości spoza przewidzianego zakresu (np. rok 1023 zamiast 2023). Istotnym jest również wychwycenie innych błędów, jak chociażby niepoprawnie przypisane identyfikatory (np. DOI, ORCID, ISSN).
    * Normalizacja wartości - Standaryzacja zapisu nazw autorów. Formatowanie dat (YYYY-MM-DD zamiast DD/MM/YYYY). Ujednolicanie jednostek (np. liczba cytowań w tysiącach).


3.  Transformacja i integracja

    Po oczyszczeniu danych kolejnym krokiem jest ich przekształcenie w jednolity format oraz łączenie informacji z różnych źródeł.

    * Agregacja danych - Grupowanie publikacji według kategorii (np. według dziedzin nauki, instytucji). Sumowanie liczby cytowań dla poszczególnych autorów i czasopism. Obliczanie średnich wskaźników (np. współczynnik akceptacji artykułów, średni czas recenzji).
    * Konwersja formatów danych - CSV → JSON dla kompatybilności z systemami API. XML → CSV dla lepszej czytelności w arkuszach kalkulacyjnych. BibTeX → RIS dla eksportu referencji naukowych.
    * Integracja danych z różnych źródeł - Łączenie wiedzy z różnych źródeł znacząco zwiększa jakość i potencjał opracowywanych danych. W ramach pozyskiwania dodatkowych informacji o autorach można na przykład spróbować łączyć dane z ORCID, Google Scholar i Scopus. W przypadku metadanych można wykorzystać DOI i pozyskiwać informacje za pomocą CrossRef API.



Przestrzeganie opisanych kroków – od przemyślanego pozyskiwania danych, przez ich walidację i normalizację, po integrację i agregację – pozwala zapewnić wysoki poziom jakości danych, spójność analiz i przejrzystość procesu. Dzięki temu można nie tylko uniknąć błędów i niespójności, ale również budować wiarygodne i powtarzalne podstawy do publikacji naukowych, raportów ewaluacyjnych czy analiz wpływu.
