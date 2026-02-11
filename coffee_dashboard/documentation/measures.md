## Miary DAX

#### 1. Arabica Avg Annual Price

**Cel wykorzystania:** Widok: *Global price* – obliczenie średniej rocznej wartości ceny kawy Arabica, niezależnie od ustawionych filtrów na gatunek.

```sql
Arabica Avg Annual Price =
CALCULATE(
    AVERAGE(indicator_prices[price_value]),
    FILTER(
        ALL(indicator_prices[species]),
        indicator_prices[species] = "arabica"
    )
)
```

---

#### 2. Arabica Count

**Cel wykorzystania:** Zastosowane w miarze *Predominant species*.

```sql
Arabica Count =
CALCULATE(
    COUNTROWS ( Fact_Coffee_Quality ),
    Fact_Coffee_Quality[species] = "Arabica"
)
```

---

#### 3. Arabica Quality

**Cel wykorzystania:** Widok: *Coffee Quality* – obliczenie średniego wyniku jakości wyłącznie dla kawy Arabica.

```sql
Arabica Quality =
CALCULATE(
    [Avg Quality Score],
    Fact_Coffee_Quality[species] = "Arabica"
)
```

---

#### 4. Avg Defects

**Cel wykorzystania:** Widok: *Coffee Quality* – obliczenie średniej liczby defektów dla wszystkich rekordów w tabeli.

```sql
Avg Defects =
AVERAGE (
    Fact_Coffee_Quality[TotalDefects]
)
```

---

#### 5. Avg Defects Global

**Cel wykorzystania:** Widok: *Coffee Quality* – obliczenie średniej liczby defektów globalnie, z pominięciem filtrów na kraj.

```sql
Avg Defects Global =
CALCULATE(
    AVERAGE (Fact_Coffee_Quality[TotalDefects]),
    REMOVEFILTERS (Dim_Countries[country])
)
```

---

#### 6. Avg Price Paid to Grower

**Cel wykorzystania:** Zastosowane w miarze *Farmer's Share %*.

```sql
Avg Price Paid to Grower =
AVERAGE(
    'Fact_Exporting_Countries'[price_paid_to_grower]
)
```

---

#### 7. Avg Quality Score

**Cel wykorzystania:** Widok: *Coffee Quality* – obliczenie średniej wartości oceny jakości kawy.

```sql
Avg Quality Score =
AVERAGE(Fact_Coffee_Quality[total_cup_points])
```

---

#### 8. Caffeine per 100

**Cel wykorzystania:** Widok: *Drink Contents* – obliczenie ilości kofeiny w mg na 100 ml napoju.

```sql
Caffeine per 100 =
VAR TotalCaff =
    SUM(Fact_Caffeine_Content[caffeine_mg])
VAR TotalVolume =
    SUM(Fact_Caffeine_Content[volume_ml])
RETURN
    DIVIDE(TotalCaff, TotalVolume) * 100
```

---

#### 9. Calories per 100

**Cel wykorzystania:** Widok: *Drink Contents* – obliczenie liczby kalorii na 100 ml napoju.

```sql
Calories per 100 =
VAR TotalCal =
    SUM(Fact_Caffeine_Content[calories])
VAR TotalVolume =
    SUM(Fact_Caffeine_Content[volume_ml])
RETURN
    DIVIDE(TotalCal, TotalVolume) * 100
```

---

#### 10. Export Last Year

**Cel wykorzystania:** Widok: *Dashboard* – obliczenie całkowitego wolumenu eksportu dla poprzedniego roku względem aktualnie wybranego roku.

```sql
Export Last Year =
CALCULATE(
    [Total Export Volume],
    Dim_Date[year] = MAX(Dim_Date[year]) - 1
)
```

---

#### 11. Farmer's Share %

**Cel wykorzystania:** Widok: *Global price* – obliczenie procentowego udziału ceny otrzymywanej przez rolnika w porównaniu do średniej globalnej ceny.

```sql
Farmer's Share % =
DIVIDE(
    [Avg Price Paid to Grower],
    [Global Avg Price]
)
```

---

#### 12. Global Avg Price

**Cel wykorzystania:** Zastosowane w miarze *Farmer's Share %*.

```sql
Global Avg Price =
CALCULATE(
    AVERAGE(Indicator_Prices[ico_composite_indicator]),
    ALLSELECTED(
        Indicator_Prices[month],
        Indicator_Prices[year]
    )
)
```

---

#### 13. Global Avg Production

**Cel wykorzystania:** Widok: *Global price & KPI 4* – obliczenie średniej produkcji kawy na świecie, niezależnie od filtrowanego kraju.

```sql
Global Avg Production =
AVERAGEX(
    ALL(Fact_Exporting_Countries[country]),
    [Total Production]
)
```

---

#### 14. Max Avg Defects

**Cel wykorzystania:** Widok: *Coffee Quality* – znajdowanie maksymalnej średniej liczby defektów spośród wszystkich krajów.

```sql
Max Avg Defects =
VAR TabelaKraje =
    SUMMARIZE(
        ALL(Dim_Countries[country]),
        Dim_Countries[country],
        "AvgDefects",
        CALCULATE(
            AVERAGE(Fact_Coffee_Quality[TotalDefects])
        )
    )
RETURN
    MAXX(TabelaKraje, [AvgDefects])
```

---

#### 15. Predominant species

**Cel wykorzystania:** Widok: *Coffee Quality* – określanie dominującego gatunku kawy (Arabica lub Robusta) na podstawie większej liczby wystąpień.

```sql
Predominant species =
VAR ArabicaCnt = [Arabica Count]
VAR RobustaCnt = [Robusta Count]
RETURN
    SWITCH(
        TRUE(),
        ArabicaCnt > RobustaCnt, "Arabica",
        RobustaCnt > ArabicaCnt, "Robusta",
        "Brak dominującego"
    )
```

---

#### 16. Production % of Global

**Cel wykorzystania:** Widok: *Dashboard* – obliczenie udziału produkcji danego kraju w całkowitej globalnej produkcji.

```sql
Production % of Global =
DIVIDE(
    [Total Production],
    CALCULATE(
        [Total Production],
        ALL(Fact_Exporting_Countries)
    )
)
```

---

#### 17. Production Efficiency

**Cel wykorzystania:** Widok: *Global price* – obliczenie efektywności produkcji kawy jako produkcja na jednostkę powierzchni kraju.

```sql
Production Efficiency =
DIVIDE(
    [Total Production],
    SUM('Dim_Countries'[area])
)
```

---

#### 18. Production Last Year

**Cel wykorzystania:** Widok: *Dashboard* – obliczanie całkowitej produkcji z poprzedniego roku względem aktualnie wybranego roku.

```sql
Production Last Year =
VAR CurrentYear = SELECTEDVALUE(Dim_Date[year])
RETURN
    IF(
        NOT ISBLANK(CurrentYear),
        CALCULATE(
            [Total Production],
            ALL(Dim_Date),
            Dim_Date[year] = CurrentYear - 1
        )
    )
```

---

#### 19. Production YTD

**Cel wykorzystania:** Obliczenie łącznej produkcji narastająco od początku roku do wybranej daty.

```sql
Production YTD =
CALCULATE(
    [Total Production],
    DATESYTD(Dim_Date[Date])
)
```

---

#### 20. Robusta Avg Annual Price

**Cel wykorzystania:** Widok: *Global price* – obliczanie średniej rocznej ceny kawy Robusta, niezależnie od filtrów na gatunek.

```sql
Robusta Avg Annual Price =
CALCULATE(
    AVERAGE(indicator_prices[price_value]),
    FILTER(
        ALL(indicator_prices[species]),
        indicator_prices[species] = "robusta"
    )
)
```

---

#### 21. Robusta Count

**Cel wykorzystania:** Zastosowane w miarze *Predominant species*.

```sql
Robusta Count =
CALCULATE(
    COUNTROWS ( Fact_Coffee_Quality ),
    Fact_Coffee_Quality[species] = "Robusta"
)
```

---

#### 22. Robusta Quality

**Cel wykorzystania:** Widok: *Coffee Quality* – obliczanie średniej oceny jakości wyłącznie dla kawy Robusta.

```sql
Robusta Quality =
CALCULATE(
    [Avg Quality Score],
    Fact_Coffee_Quality[species] = "Robusta"
)
```

---

#### 23. Rolling Avg Price (3M)

**Cel wykorzystania:** Obliczanie średniej ceny globalnej z ostatnich 3 miesięcy.

```sql
Rolling Avg Price (3M) =
AVERAGEX(
    DATESINPERIOD(
        Dim_Date[Date],
        LASTDATE(Dim_Date[Date]),
        -3,
        MONTH
    ),
    [Global Avg Price]
)
```

---

#### 24. Rolling Avg Price (3Y)

**Cel wykorzystania:** Obliczenie średniej ceny globalnej z ostatnich 3 lat.

```sql
Rolling Avg Price (3Y) =
AVERAGEX(
    DATESINPERIOD(
        Dim_Date[Date],
        LASTDATE(Dim_Date[Date]),
        -3,
        YEAR
    ),
    [Global Avg Price]
)
```

---

#### 25. Total Export Volume

**Cel wykorzystania:** Widok: *Dashboard KPI 2* – obliczanie całkowitego wolumenu eksportu kawy.

```sql
Total Export Volume =
SUM(Fact_Exporting_Countries[export])
```

---

#### 26. Total Import Volume

**Cel wykorzystania:** Obliczenie całkowitego wolumenu importu kawy.

```sql
Total Import Volume =
SUM(Fact_Importing_Countries[import])
```

---

#### 27. Total Production

**Cel wykorzystania:** Widok: *Dashboard & Global price* – obliczanie całkowitej produkcji kawy.

```sql
Total Production =
SUM(Fact_Exporting_Countries[total_production])
```

---

#### 28. Trade Volume

**Cel wykorzystania:** Widok: *Dashboard KPI 3* – obliczanie całkowitego wolumenu handlu jako suma importu i reeksportu.

```sql
Trade Volume =
SUMX(
    Fact_Importing_countries,
    [import] + [re_export]
)
```

---

#### 29. Defect Colour

**Cel wykorzystania:** Widok: *Coffee Quality* – przypisywanie koloru w zależności od tego, czy średnia liczba defektów w kraju jest wyższa od średniej globalnej.

```sql
Defect Colour =
VAR KrajDef = [Avg Defects]
VAR GlobalDef = [Avg Defects Global]
RETURN
    IF(
        KrajDef > GlobalDef,
        "#D64242",
        "#774E45"
    )
```

---

#### 30. Avg Quality Score Global

**Cel wykorzystania:** Widok: *Coffee Quality* – obliczenie globalnej średniej oceny jakości kawy (z pominięciem filtrów kraju).

```sql
Avg Quality Score Global =
CALCULATE(
    AVERAGE ( Fact_Coffee_Quality[total_cup_points] ),
    REMOVEFILTERS ( 'Dim_Countries'[country] )
)
```