# OLAP – Sales Data Warehouse (SSIS + SSAS)

## Disclaimer
Repozytorium ma charakter edukacyjny i portfolio.
Nie zawiera świadomie żadnych poufnych danych ani elementów produkcyjnej infrastruktury.
Projekt został przygotowany jako element portfolio prezentujący kompetencje w obszarze Data Warehouse, ETL oraz Business Intelligence.

## Struktura repozytorium

```text
/Sprzedaz
├── SSIS
└── SSAS

/MarzaCen
├── SSIS
└── SSAS
```

## O projekcie

Repozytorium zawiera dwa projekty Business Intelligence zrealizowane w technologii Microsoft SQL Server:

- **Sprzedaz** – hurtownia danych i analiza sprzedaży
- **MarzaCen** – analiza realizacji targetów, cen i marży

Wykorzystane technologie:

- SQL Server
- SSIS (SQL Server Integration Services)
- SSAS (SQL Server Analysis Services)
- OLAP
- Data Warehouse

## Disclaimer

Projekt ma charakter edukacyjny i portfolio. Nie zawiera świadomie żadnych danych poufnych ani elementów środowiska produkcyjnego.

---

# Projekt: Sprzedaz

## Cel projektu

Budowa hurtowni danych wspierającej analizę sprzedaży w różnych przekrojach biznesowych.

## Architektura

```text
Źródła danych
      ↓
SSIS (ETL)
      ↓
Data Warehouse
      ↓
SSAS Cube
      ↓
Excel / Power BI
```

## ETL (SSIS)

Proces ETL realizuje:

- pobieranie danych z baz SQL Server,
- czyszczenie i standaryzację danych,
- mapowanie kluczy biznesowych,
- walidację danych,
- ładowanie danych do hurtowni.

## Model OLAP (SSAS)

### Miary

- Wartość sprzedaży brutto/netto
- Ilość sprzedaży
- Liczba transakcji
 -Liczba klientów

### Wymiary

- Czas
- Towar
- Sklep
- VAT
- nr paragonu
- Płatność

### Hierarchie

- Rok → Miesiąc → Dzień
- Grupa produktu → Produkt

## Funkcjonalności

- analiza sprzedaży,
- analiza trendów,
- agregacje wielowymiarowe,
- hierarchie drill-down

---

# Projekt: MarzaCen

## Cel projektu

Analiza realizacji targetów handlowych, cen sprzedaży oraz marży.

## Architektura

```
Sprzedaz DWH
      ↓
SSIS (ETL)
      ↓
Data Warehouse
      ↓
SSAS Cube
      ↓
Excel / Power BI
```

## ETL (SSIS)

Proces obejmuje:

- pobieranie danych sprzedażowych,
- import targetów handlowych,
- transformacje danych cenowych,
- przygotowanie danych do analizy.

## Model OLAP (SSAS)

### Miary

- Sprzedaż brutto/netto
- Realizacja targetu

### Wymiary

- Czas
- Towar
- Sklep
- VAT
- nr paragonu
- Płatność

### Hierarchie

- Rok → Miesiąc → Dzień
- Kategoria → Produkt

## Funkcjonalności

- analiza sprzedaży vs target,
- analiza rentowności produktów,
- analiza trendów cenowych.

---

## Podsumowanie

Repozytorium prezentuje praktyczne wykorzystanie:

- SSIS do budowy procesów ETL,
- hurtowni danych SQL Server,
- SSAS do modelowania kostek OLAP,
- Excel / Power BI jako warstwy raportowej.