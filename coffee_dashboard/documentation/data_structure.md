## Opis danych

### 1. Tabela: Dim_Countries ([Samplemaps](https://simplemaps.com/data/countries))

Tabela wymiarów zawierająca szczegółowe informacje geograficzne, demograficzne oraz ekonomiczne o krajach świata.

---

#### Lista pól i opisy

| Nazwa kolumny | Opis definicji |
| --- | --- |
| **id** | Unikalny identyfikator kraju używany przez rząd USA. |
| **country** | Powszechnie używana nazwa kraju. |
| **iso2** | Dwuliterowy kod kraju (ISO 3166-1 alpha-2). |
| **continent** | Kontynent, na którym znajduje się dany kraj. |
| **population** | Szacunkowa liczba ludności na podstawie spisu powszechnego z najnowszych dostępnych danych. |
| **density** | Gęstość zaludnienia na kilometr kwadratowy. |
| **area** | Całkowita powierzchnia lądowa i wodna ograniczona granicami międzynarodowymi i liniami brzegowymi (km²). |
| **gdp** | Produkt Krajowy Brutto – całkowita wartość wszystkich towarów i usług wytworzonych w danym kraju. |
| **median_age** | Mediana wieku – wiek dzielący populację na dwie liczebnie równe grupy. |
| **language** | Główny język używany w kraju. |
| **religion** | Najczęściej wyznawane religie w kraju (maksymalnie 3, próg min. 10%, rozdzielone znakiem |). |
| **demonym** | Nazwa używana w odniesieniu do mieszkańców danego kraju. |
| **currency** | Oficjalna waluta kraju. |
| **calling_code** | Międzynarodowy numer kierunkowy kraju. |
| **driving_side** | Strona ruchu drogowego (lewa lub prawa). |
| **un_member** | Informacja, czy kraj jest członkiem ONZ (TRUE lub FALSE). |
| **tld** | Krajowa domena najwyższego poziomu (internetowa). |
| **website** | Oficjalna rządowa strona internetowa kraju. |

### 2. Tabela: Fact_Coffee_Quality ([Coffee Quality database from CQI](https://www.kaggle.com/datasets/volpatto/coffee-quality-database-from-cqi))

Tabela faktów zawierająca wyniki ocen sensorycznych (cupping) oraz dane o pochodzeniu i certyfikacji partii kawy.
Pola zostały pogrupowane tematycznie (miary jakości, metadane ziarna i farmy), aby ułatwić zrozumienie ich przeznaczenia w procesie analizy jakości kawy.

---

#### Lista pól i opisy

**1. Miary Jakości (Quality Measures)**

Pola te zawierają punktację przyznaną przez certyfikowanych degustatorów (Q-graders) w skali 0–10.

| Nazwa kolumny | Opis |
| --- | --- |
| **Aroma** | Zapach kawy (suchy i po zalaniu wodą). |
| **Flavor** | Główny profil smakowy kawy. |
| **Aftertaste** | Posmak pozostający w ustach po degustacji. |
| **Acidity** | Kwasowość (jasność) naparu. |
| **Body** | Tekstura i ciężkość kawy w ustach. |
| **Balance** | Harmonia między wszystkimi aspektami smakowymi. |
| **Uniformity** | Jednorodność smaku w różnych filiżankach tej samej próbki. |
| **Clean.Cup** | Czystość naparu (brak obcych smaków). |
| **Sweetness** | Poziom słodyczy odczuwalny w kawie. |
| **Cupper.Points** | Subiektywna ocena ogólna wystawiona przez eksperta. |
| **Total.Cup.Points** | Sumaryczna punktacja jakości (podstawowa miara jakości kawy speciality). |

**2. Metadane Ziarna i Charakterystyka Fizyczna**

Dane techniczne dotyczące surowego ziarna przed wypaleniem.

| Nazwa kolumny | Opis |
| --- | --- |
| **Species** | Gatunek kawy (najczęściej Arabica lub Robusta). |
| **Variety** | Odmiana botaniczna kawy (np. Typica, Bourbon, Caturra). |
| **Processing.Method** | Metoda obróbki (np. Washed, Natural, Honey). |
| **Moisture** | Procentowa zawartość wilgoci w ziarnie. |
| **Color** | Kolor surowego ziarna (np. Green, Bluish-Green). |
| **Quakers** | Liczba niedojrzałych ziaren ujawniających się po wypaleniu. |
| **Category.One.Defects** | Liczba wad kategorii pierwszej (poważne błędy). |
| **Category.Two.Defects** | Liczba wad kategorii drugiej (mniejsze uszkodzenia). |

**3. Dane o Farmie i Pochodzeniu**

Informacje o lokalizacji i producencie kawy.

| Nazwa kolumny | Opis |
| --- | --- |
| **Country.of.Origin** | Kraj pochodzenia. |
| **Region** | Region uprawy w danym kraju. |
| **Farm.Name** | Nazwa plantacji, z której pochodzi kawa. |
| **Producer** | Imię i nazwisko lub nazwa producenta. |
| **Mill** | Zakład przetwórczy (młyn), gdzie ziarno było obrabiane. |
| **Company** | Firma eksportująca lub zgłaszająca kawę do oceny. |
| **Altitude** | Oryginalny wpis dotyczący wysokości upraw (tekst). |
| **altitude_mean_meters** | Uśredniona wysokość uprawy w metrach n.p.m. |

**4. Logistyka i Certyfikacja**

Szczegóły dotyczące partii towaru i instytucji certyfikującej.

| Nazwa kolumny | Opis |
| --- | --- |
| **Lot.Number** | Numer partii towaru. |
| **ICO.Number** | Numer identyfikacyjny International Coffee Organization. |
| **Number.of.Bags** | Liczba worków w danej partii. |
| **Bag.Weight** | Waga pojedynczego worka. |
| **Harvest.Year** | Rok zbiorów. |
| **Grading.Date** | Data przeprowadzenia oceny jakości. |
| **Expiration** | Data ważności certyfikatu jakości. |
| **Certification.Body** | Nazwa organizacji wystawiającej certyfikat. |
| **In.Country.Partner** | Partner krajowy współpracujący z CQI. |

### 3. Tabela: Fact_Caffeine_Content ([Caffeine Content of Drinks](https://www.kaggle.com/datasets/heitornunes/caffeine-content-of-drinks))

Tabela faktów zawierająca szczegółowe dane na temat zawartości kofeiny, kaloryczności oraz objętości różnych rodzajów napojów.

---

#### Lista pól i opisy

| Nazwa kolumny | Opis definicji |
| --- | --- |
| **drink_name** | Nazwa napoju (lub produktu, np. liście herbaty/kawa mielona). |
| **volume_ml** | Objętość płynu w mililitrach. W przypadku kawy mielonej lub herbaty jest to objętość naparu uzyskana przy przygotowaniu zgodnie z zaleceniami dostawcy. |
| **calories** | Ilość kalorii w danej objętości napoju. |
| **caffeine_mg** | Zawartość kofeiny wyrażona w miligramach. |
| **type** | Kategoria napoju. Główne typy to: *Coffee, Energy Drinks, Energy Shots, Soft Drinks, Tea, Water*. |
| **CaffeineIntensity** | *Pole dodatkowe (prawdopodobnie wyliczone):* Wskaźnik intensywności kofeiny (np. stosunek kofeiny do objętości lub kategoryzacja mocy). |
| **IsHighCalorie** | *Pole dodatkowe (prawdopodobnie wyliczone):* Flaga logiczna (True/False) określająca, czy napój charakteryzuje się wysoką zawartością kalorii. |

---

#### Kluczowe informacje o danych

* **Przygotowanie naparów**: Wartości dla kawy mielonej i liści herbaty odnoszą się do gotowego napoju przygotowanego według instrukcji.
* **Brak kalorii**: Niektóre pozycje (jak czysta kawa czy herbata) mają 0 kalorii, ponieważ ich kaloryczność zależy od indywidualnie dodanej ilości cukru lub mleka.
* **Pochodzenie**: Dane pochodzą z serwisu *Caffeine Informer*.


### 4.1 Tabela: Fact_exporting_Countries ([ICO Coffee Dataset (Worldwide)](https://www.kaggle.com/datasets/yamaerenay/ico-coffee-dataset-worldwide))

Tabela zawiera kluczowe wskaźniki ekonomiczne dla krajów będących producentami i eksporterami kawy.

---

#### Lista pól i opisy

| Nazwa kolumny | Opis |
| --- | --- |
| **country** | Nazwa kraju eksportującego. |
| **year** | Rok kalendarzowy lub rok zbiorów (crop year), którego dotyczą dane. |
| **total_production** | Całkowita produkcja kawy w danym kraju. |
| **domestic_consumption** | Konsumpcja wewnętrzna kawy przez mieszkańców kraju eksportującego. |
| **export** | Całkowity eksport kawy we wszystkich formach. |
| **gross_opening_stock** | Stan zapasów początkowych brutto w kraju eksportującym. |
| **price_paid_to_grower** | Średnia cena płacona bezpośrednio plantatorom (hodowcom) za kawę. |
| **IsMajorProducer** | Flaga logiczna określająca, czy dany kraj należy do grupy głównych światowych producentów. |

### 4.2 Tabela: Fact_importing_countries ([ICO Coffee Dataset (Worldwide)](https://www.kaggle.com/datasets/yamaerenay/ico-coffee-dataset-worldwide))

Tabela gromadzi dane dotyczące obrotu i konsumpcji kawy w krajach, które są głównie odbiorcami surowca.

---

#### Lista pól i opisy

| Nazwa kolumny | Opis |
| --- | --- |
| **country** | Nazwa kraju importującego. |
| **year** | Rok, którego dotyczą statystyki. |
| **import** | Ilość kawy zaimportowanej przez dany kraj. |
| **disappearance** | Wskaźnik "znikania" towaru z rynku, interpretowany jako realna konsumpcja w kraju importującym. |
| **inventories** | Stan zapasów zielonej (surowej) kawy w magazynach kraju importującego. |
| **re_export** | Ilość kawy, która po imporcie została ponownie wyeksportowana do innych krajów. |
| **retail_price** | Średnia cena detaliczna kawy palonej oferowana konsumentom końcowym. |


### 4.3 Tabela: indicator_prices ([ICO Coffee Dataset (Worldwide)](https://www.kaggle.com/datasets/yamaerenay/ico-coffee-dataset-worldwide))

Tabela rynkowa zawierająca uśrednione wskaźniki cenowe ICO dla głównych grup handlowych kawy.

---

#### Lista pól i opisy

| Nazwa kolumny | Opis |
| --- | --- |
| **year** | Rok notowania ceny. |
| **month** | Miesiąc notowania ceny (umożliwia analizę sezonowości). |
| **ico_composite_indicator** | Złożony wskaźnik cenowy ICO (Composite Indicator Price) – średnia ważona cen kawy na rynkach światowych. |
| **colombian_milds** | Wskaźnik cenowy dla łagodnych kaw z Kolumbii. |
| **other_milds** | Wskaźnik cenowy dla pozostałych kaw typu "Milds". |
| **brazilian_naturals** | Wskaźnik cenowy dla kaw naturalnych z Brazylii. |
| **robustas** | Wskaźnik cenowy dla kawy gatunku Robusta. |