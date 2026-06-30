# InWeek - System Bazy Danych (Firma Logistyczno-Transportowa)

Projekt relacyjnej bazy danych dedykowany dla firmy logistyczno-transportowej "InWeek" (model operacyjny zbliżony do rozwiązań typu InPost). Repozytorium zawiera pełen cykl projektowy: od modelowania koncepcyjnego i diagramów, przez skrypty DDL/DML, aż po kwerendy testowe, widoki i dokumentację końcową.

## 📂 Struktura Repozytorium i Opis Plików

Pliki w projekcie zostały podzielone na cztery logiczne sekcje odpowiadające etapom tworzenia systemu.

### 1. Modelowanie i Wizualizacja (Projekt)
* **`Diagram_przeplywu_danych01.uxf`** – Diagram przepływu danych (Data Flow Diagram) określający, jak informacje przemieszczają się w systemie InWeek.
* **`umlet_useCase.uxf`** – Diagram przypadków użycia (UML Use Case) definiujący interakcje aktorów (np. kurier, klient) z systemem.
* **`diagramy_dmd.zip`** – Archiwum z diagramami modelu danych (Data Model Diagram), w tym schematy logiczne i fizyczne relacji.

### 2. Tworzenie i Inicjalizacja Bazy (Implementacja)
* **`SQL_bazy.ddl`** – Główny plik z kodem Data Definition Language (DDL). Odpowiada za tworzenie struktury bazy: tabel, relacji, kluczy obcych i głównych.
* **`inserty.txt`** – Skrypty Data Manipulation Language (DML) służące do populacji utworzonych tabel danymi początkowymi/testowymi.

### 3. Logika, Walidacja i Eksploatacja (Zapytania)
* **`widoki.txt`** – Skrypty tworzące widoki (VIEWS) ułatwiające przeglądanie złożonych, połączonych danych.
* **`walidacja_constraint.txt`** – Zapytania mające na celu przetestowanie zabezpieczeń i ograniczeń bazy (constraints), weryfikujące czy niemożliwe jest wpisanie nieprawidłowych danych.
* **`walidacja_wpisanych_danych.txt`** – Kwerendy weryfikujące, czy rekordy załadowane z pliku insertów zostały poprawnie zapisane i zachowują integralność.
* **`selekcje.txt`** – Zestaw zapytań wybierających (SELECT), symulujących realne raporty i ekstrakcję danych biznesowych z systemu InWeek.

### 4. Dokumentacja
* **`Sprawozdanie_Projekt_Bazy.pdf`** – Pełne, techniczne podsumowanie projektu, opisujące przyjęte założenia i architekturę.
* **`System Bazy Danych InWeek - Raport Finalny v3.pptx`** – Prezentacja podsumowująca całość rozwiązania z perspektywy biznesowej i technicznej.

---

## ⚙️ Kolejność Uruchamiania i Analizy Projektu

Aby poprawnie odtworzyć i przetestować bazę danych, należy trzymać się poniższej kolejności:

1.  **Analiza architektury:** Zapoznanie się z diagramami w plikach `.uxf` oraz zawartością `diagramy_dmd.zip` w celu zrozumienia założeń biznesowych.
2.  **Inicjalizacja schematu:** Uruchomienie skryptu `SQL_bazy.ddl` w docelowym silniku bazy danych, co utworzy puste tabele powiązane odpowiednimi relacjami.
3.  **Wgrywanie danych:** Wykonanie zapytań z pliku `inserty.txt` w celu wypełnienia bazy danymi testowymi.
4.  **Dodanie logiki biznesowej:** Uruchomienie skryptu `widoki.txt` celem wygenerowania predefiniowanych perspektyw danych.
5.  **Walidacja:** Wykonanie skryptów z plików `walidacja_constraint.txt` oraz `walidacja_wpisanych_danych.txt` w celu sprawdzenia poprawności nałożonych ograniczeń (np. klucze, nullability).
6.  **Eksploatacja (Odpytywanie):** Na sam koniec przetestowanie działania systemu za pomocą przykładowych zapytań raportowych zawartych w `selekcje.txt`.

---

## ⚠️ Rozwiązywanie Problemów (Troubleshooting)

- **Brak widocznych diagramów w Oracle SQL Developer Data Modeler** – Otwarcie pliku `.dmd` nie renderuje automatycznie obszaru roboczego. Aby wyświetlić graf:
  1. Sprawdź spójność struktury: plik wskaźnikowy (np. `diagram_po_normalizacji.dmd`) musi leżeć na tym samym poziomie co folder o dokładnie tej samej nazwie (`diagram_po_normalizacji`), a w jego środku muszą znajdować się katalogi źródłowe (`logical`, `rel`, `pm` itd.). 
  2. Wywołaj widok ręcznie: W górnym menu programu wybierz `View -> Browser`. Rozwiń drzewo projektu, kliknij prawym przyciskiem myszy na interesujący Cię model (np. w sekcji `Logical Model` lub `Relational Models`) i wybierz `Show`.
- **Błąd: "Table already exists" / "Baza już istnieje"** – Przed ponownym uruchomieniem skryptu `SQL_bazy.ddl` upewnij się, że usunięto poprzednie wersje tabel. Zmodyfikuj skrypt DDL dodając dyrektywy `DROP TABLE IF EXISTS ... CASCADE;` na jego początku.
- **Naruszenie kluczy obcych (Foreign Key Constraint Fails)** – Sprawdź kolejność wykonywania zapytań w `inserty.txt`. Tabele słownikowe i nadrzędne (np. klienci, pojazdy) muszą być zasilane danymi przed tabelami podrzędnymi (np. paczki, zlecenia).
- **Błędy kodowania znaków** – Upewnij się, że klient SQL (np. DBeaver, pgAdmin) oraz importowane skrypty `.txt` korzystają z kodowania `UTF-8`.
## 👥 Autorzy

- **[Radek04]**
- **[The1Takashi]**
