OLAP – Sales Data Warehouse (SSIS + SSAS)
Struktura repozytorium
•	/Sprzedaz – projekt analizy sprzedaży
•	/MarzaCen – projekt analizy realizacji targetów
Struktura projektu
/Sprzedaz
  /SSIS
    /*.dtsx
  /SSAS
    /2026
      model OLAP
/MarzaCen
  /SSIS
    /*.dtsx
  /SSAS
      model OLAP

## Disclaimer
Repozytorium ma charakter edukacyjny i portfolio. Nie zawiera świadomie żadnych poufnych danych ani elementów produkcyjnej infrastruktury.

## Przegląd SPRZEDAZ
Projekt przedstawia rozwiązanie hurtowni danych dla obszaru sprzedaży (Sales DWH) zaprojektowane w oparciu o stack Microsoft BI:
•	SSIS (SQL Server Integration Services) – procesy ETL
•	SSAS (SQL Server Analysis Services) – model analityczny OLAP (kostki)
Architektura została zaprojektowana w podejściu year-based, gdzie każdy rok (np. 2026) posiada:
•	dedykowany pipeline ETL (SSIS)
•	osobną kostkę analityczną (SSAS)

## Architektura
Data flow:
Source Systems → SSIS (ETL) → Data Warehouse → SSAS Cube → Reporting
Rozwiązanie składa się z dwóch głównych warstw:
•	ETL (SSIS) – przygotowanie danych
•	OLAP (SSAS) – warstwa analityczna

## SSIS – ETL (na przykładzie 2026)
Dla roku 2026 zaimplementowano dedykowany pipeline ETL realizujący pełny proces przetwarzania danych sprzedażowych.
Zakres procesu
Pipeline SSIS odpowiada za:
1.	Extract
o	pobieranie danych ze źródeł (bazy danych MS SQL Server)
2.	Transform
o	czyszczenie i standaryzacja danych
o	mapowanie kluczy (powiązanie faktów z wymiarami)
o	walidacja i przygotowanie danych analitycznych
3.	Load
o	załadunek do struktur hurtowni:
	tabela faktów
	tabel wymiarów (np. produkt, sklep, czas)
Charakterystyka podejścia
•	logika ETL jest izolowana per rok
•	każdy pipeline może być uruchamiany niezależnie

Zalety
•	prostota implementacji
•	łatwe debugowanie
•	izolacja błędów między latami

## SSAS – OLAP (na przykładzie 2026)
Dla roku 2026 została utworzona dedykowana kostka OLAP, bazująca na danych przygotowanych przez SSIS.
Model analityczny
Kostka zawiera:
•	Measures (miary)
agregacje biznesowe (np. sprzedaż, ilość)
•	Dimensions (wymiary)
kontekst analizy (np. czas, produkt, klient)
•	Hierarchies (hierarchie)
umożliwiają analizę typu drill-down (np. rok → miesiąc → dzień)

Funkcjonalność
SSAS umożliwia:
•	szybkie zapytania analityczne
•	analizę wielowymiarową
•	agregacje danych na różnych poziomach

Przepływ danych (dla 2026)
SSIS (ETL 2026)
      ↓
Data Warehouse (fact + dimensions)
      ↓
SSAS Cube 2026
      ↓
Raportowanie (Excel / Power BI)

## Decyzje projektowe
Year-based architecture
Projekt wykorzystuje podejście:
•	osobny ETL per rok
•	osobna kostka per rok
Uzasadnienie
•	prostsza implementacja
•	izolacja danych historycznych
•	niezależne przetwarzanie

## Możliwości modyfikacji
Z perspektywy architektonicznej rozwiązanie można rozwinąć:
SSAS
•	zastosowanie jednej kostki z partycjonowaniem (per rok)

________________________________________
## Podsumowanie
Projekt implementuje kompletny pipeline BI:
•	ETL (SSIS) → Data Warehouse → OLAP (SSAS)




OLAP MarzaCen (SSIS + SSAS)
## Przegląd
Projekt przedstawia rozwiązanie analityczne skoncentrowane na analizie marży i cen, zbudowane w oparciu o Microsoft BI stack:
•	SSIS (SQL Server Integration Services) – procesy ETL
•	SSAS (SQL Server Analysis Services) – model OLAP
Celem projektu jest umożliwienie analizy:
•	Rzeczywistej sprzedaży vs target

## Architektura
Data flow:
Source Data → SSIS (ETL) → Data Warehouse → SSAS Cube → Reporting
Rozwiązanie składa się z:
•	ETL (SSIS) – przygotowanie danych
•	OLAP (SSAS) – warstwa analityczna


## SSIS – ETL (na przykładzie 2026)
Procesy ETL odpowiadają za przygotowanie danych potrzebnych do analizy marży.
Zakres procesu
Pipeline SSIS realizuje:
1. Extract
•	pobranie danych sprzedażowych (z poprzedniej hurtowni danych SPRZEDAZ2026) i cenowych

2. Transform
Kluczowa część projektu:
•	pobieranie plików z ustalonymi przez DH targetami
•	przekształcenie danych cenowych
•	mapowanie produktów / klientów
•	walidacja i czyszczenie danych

3. Load
•	zapis danych do hurtowni:
o	tabel faktów (sprzedaż + marża)
o	tabel wymiarów (produkt, klient, czas)

## Charakterystyka ETL
•	pipeline skoncentrowany na logice biznesowej (rzeczywista sprzedaż vs target i wykonanie)
•	przygotowanie danych pod analizę wielowymiarową

SSAS – OLAP (na przykładzie MarżaCen2026)
Model SSAS umożliwia analizę marży i cen w różnych przekrojach.
## Model zawiera:
Measures (miary)
•	wartość sprzedaży
•	koszt
•	marża
•	wskaźniki (np. % marży)
________________________________________
Dimensions (wymiary)
•	produkt
•	klient
•	czas
•	(opcjonalnie: kanał sprzedaży, segment)
________________________________________
Hierarchies
•	czas (rok → miesiąc → dzień)
•	produkt (kategoria → produkt)
________________________________________
## Funkcjonalność
SSAS umożliwia:
•	analizę sprzedaży i wykonanie targetu
•	identyfikację produktów o niskiej rentowności
•	analizę trendów cenowych

## End-to-End Flow
SSIS (ETL – pricing & margin)
      ↓
Data Warehouse
      ↓
SSAS Cube (Margin Analysis)
      ↓
Raportowanie (Excel / Power BI)
________________________________________
# Design Decisions
Model analityczny skoncentrowany na marży
Projekt skupia się na:
•	przekształceniu danych sprzedażowych w dane analityczne
•	wyliczeniu marży jako kluczowego KPI
________________________________________
## Podsumowanie
Projekt implementuje rozwiązanie analityczne skoncentrowane na:
•	analizie sprzedaży vs target
•	analizie cen
•	wsparciu decyzji biznesowych
Stanowi przykład praktycznego wykorzystania:
•	SSIS do przetwarzania danych
•	SSAS do analizy wielowymiarowej
