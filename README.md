# Vertinimo Sistema (v1.0)

**Versija:** 1.0  
**Data:** 2025-10-03  
**Kam:** Administracija, Mentoriai, Curatoriai

----------

## Turinys

1.  [Įvadas](#%C4%AFvadas)
2.  [BUP limitas ir pamokų planavimas](#bup-limitas-ir-pamok%C5%B3-planavimas)
3.  [Kaip sistema skaičiuoja vertes](#kaip-sistema-skai%C4%8Diuoja-vertes)
4.  [Temų kūrimas žingsnis po žingsnio](#tem%C5%B3-k%C5%ABrimas-%C5%BEingsnis-po-%C5%BEingsnio)
5.  [Tikslų vertės apskaičiavimas](#tiksl%C5%B3-vert%C4%97s-apskai%C4%8Diavimas)
6.  [Mokinio pažangos skaičiavimas](#mokinio-pa%C5%BEangos-skai%C4%8Diavimas)
7.  [Produktyvumo skaičiavimas](#produktyvumo-skai%C4%8Diavimas)
8.  [Praktinis pavyzdys](#praktinis-pavyzdys)
9.  [Dažniausiai užduodami klausimai](#da%C5%BEniausiai-u%C5%BEduodami-klausimai)

----------

## Įvadas

### Kam skirta ši sistema?

Vertinimo sistema leidžia:

-   ✅ **Mokytojams** - laipsniškai planuoti kursą pagal realų laiką ir temas
-   ✅ **Mokiniams** - matyti tikslią pažangą (ne klaidinančią)
-   ✅ **Administracijai** - stebėti BUP atitikimą ir realų progresą
-   ✅ **Tėvams** - sekti vaiko mokymosi tempą

### Pagrindinė idėja

**Kiekvienas kursas = 100%**

Sistema **automatiškai paskirsto** šimtą procentų:

1.  **Tarp jau sukurtų temų** - pagal mentoriaus nustatytą vertę
2.  **Tarp dar nesuplanuoto laiko** - priimant, kad kiekviena pamoka = 1 tema su koeficientu 1.0
3.  **Dinamiškai perskaičiuoja** - kiekvieną kartą sukūrus naują temą
4.  **Mokinio pažanga** - atspindi tikrą progresą kurse

----------

## BUP limitas ir pamokų planavimas

### Kas yra BUP limitas?

**BUP (Bendroji ugdymo programa)** nustato:

-   📚 Kiek valandų per metus turi būti skiriama dalykui
-   ⏱️ Pamokos trukmę (įprastai 45 minutės)
-   📊 Iš anksto žinomas pamokų skaičius per metus

### Skaičiavimas

```
Pavyzdys: Matematika 7 klasė

BUP reikalavimas: 140 valandų per metus
Pamokos trukmė: 45 minutės

Pamokų skaičius = (140 val × 60 min) / 45 min = 186.67 ≈ 187 pamokos
```

### Limito lankstumas

Sistema **leidžia**:

-   ✅ **Viršyti limitą** - jei mokiniui reikia daugiau laiko temai
-   ✅ **Neužpildyti limito** - jei metų pabaigoje lieka nepanaudotų pamokų
-   ✅ **Koreguoti dinamiškai** - temų trukmė ir vertė gali keistis

**Kodėl?**

-   🎓 Realybėje mokiniai mokosi skirtingu tempu
-   🎓 Kai kurios temos gali užtrukti ilgiau nei planuota
-   🎓 Deficitas gali būti kompensuojamas kitose temose

----------

## Kaip sistema skaičiuoja vertes

### Pagrindinis principas

Sistema **nežino** ateityje, kokias temas mentorius sukurs. Todėl:

1.  **Suplanuotoms temoms** - naudoja faktinę vertę ir trukmę
2.  **Nepanaudotam laikui** - priima, kad **1 pamoka = 1 tema su koeficientu 1.0**

### Kodėl taip?

```
Mentorius sukuria 3 temas (15 pamokų) iš 187
Sistema: 
  - 3 temos = 8% kurso (pagal jų vertę)
  - Likę 172 pamokos = 92% kurso (dar nesuplanuota)
  
Mokinys užbaigia 2 temas
Sistema rodo: "5.3% kurso užbaigta" ✅

Realybė: Tiksliai atspindi progresą ✅
```

### Formulė

```
Temos "vienetai" = Trukmė (pamokos) × Vertės koeficientas

Viso vienetų = Σ(sukurtų temų vienetai) + (Likusios pamokos × 1.0)

Temos vertė (%) = (Temos vienetai / Viso vienetų) × 100%
```

### Temos parametrai

Kiekviena tema turi **2 parametrus**:

#### 1. Trukmė (pamokos)

-   Objektyvus matas
-   Kiek pamokų užims tema
-   Nurodo mentorius

**Pavyzdžiai:**

```
Įvadinė tema: 2 pamokos
Standartinė tema: 8 pamokos
Sudėtinga tema: 12 pamokų
Projektas: 20 pamokų
```

#### 2. Vertės koeficientas

-   Subjektyvus matas
-   Atspindi temos svarbą/sudėtingumą
-   Nurodo mentorius pagal išmonę

**Pavyzdžiai:**

```
0.5 - Lengva/trumpa tema
1.0 - Standartinė tema (default)
1.5 - Svarbi/sudėtinga tema
2.0 - Labai svarbi tema
3.0 - Kritinė tema (pvz. egzaminas)
```

**Svarbu:** Koeficientas **ne visada** proporcingas trukmei!

```
Tema A: 10 pamokų, koef. 0.5 → Lengva, bet ilga
Tema B: 5 pamokos, koef. 2.0 → Trumpa, bet labai svarbi
```

----------

## Temų kūrimas žingsnis po žingsnio

### Scenarijus: Matematika 7 klasė

**Pradinė būsena:**

```
BUP limitas: 187 pamokos
Sukurta temų: 0
Sistema priima: 187 pamokos × koef. 1.0 = 187 "vienetų"
```

----------

### Žingsnis 1: Mentorius sukuria pirmą temą

**Tema 1: "Racionalieji skaičiai"**

-   Trukmė: 10 pamokų
-   Vertės koeficientas: 1.0

**Sistema perskaičiuoja:**

```
Tema 1 vienetai = 10 × 1.0 = 10

Nepanaudota = 187 - 10 = 177 pamokų
Nepanaudotos pamokos vienetai = 177 × 1.0 = 177

Viso vienetų = 10 + 177 = 187

Tema 1 vertė = 10 / 187 × 100% = 5.35%
```

**Sistemos ekranas:**

```
┌────────────────────────────────────────┐
│ Matematika 7A - Kurso planavimas       │
├────────────────────────────────────────┤
│                                        │
│ BUP limitas: 187 pamokos               │
│                                        │
│ SUKURTOS TEMOS:                        │
│ 1. Racionalieji skaičiai               │
│    Trukmė: 10 pamokų                   │
│    Koeficientas: 1.0                   │
│    Vertė: 5.35%                        │
│                                        │
│ NEPANAUDOTA:                           │
│ 177 pamokos (94.65%)                   │
│                                        │
│ BENDRA SUMA: 100.00% ✓                 │
└────────────────────────────────────────┘
```

----------

### Žingsnis 2: Mentorius sukuria antrą temą

**Tema 2: "Tiesinės funkcijos"**

-   Trukmė: 12 pamokų
-   Vertės koeficientas: 1.5 (sudėtinga tema)

**Sistema perskaičiuoja:**

```
Tema 1 vienetai = 10 × 1.0 = 10
Tema 2 vienetai = 12 × 1.5 = 18

Nepanaudota = 187 - 10 - 12 = 165 pamokų
Nepanaudota vienetais = 165 × 1.0 = 165

Viso vienetų = 10 + 18 + 165 = 193

Tema 1 vertė = 10 / 193 × 100% = 5.18%  (sumažėjo!)
Tema 2 vertė = 18 / 193 × 100% = 9.33%
```

**Sistemos ekranas:**

```
┌────────────────────────────────────────┐
│ Matematika 7A - Kurso planavimas       │
├────────────────────────────────────────┤
│                                        │
│ BUP limitas: 187 pamokos               │
│                                        │
│ SUKURTOS TEMOS:                        │
│ 1. Racionalieji skaičiai               │
│    Trukmė: 10 pamokų                   │
│    Koeficientas: 1.0                   │
│    Vertė: 5.18% (buvo 5.35%)           │
│                                        │
│ 2. Tiesinės funkcijos                  │
│    Trukmė: 12 pamokų                   │
│    Koeficientas: 1.5                   │
│    Vertė: 9.33%                        │
│                                        │
│ NEPANAUDOTA:                           │
│ 165 pamokos (85.49%)                   │
│                                        │
│ BENDRA SUMA: 100.00% ✓                 │
└────────────────────────────────────────┘
```

**⚠️ Pastaba:** Tema 1 vertė **sumažėjo** nuo 5.35% į 5.18%, nes pridėjus naują temą perskaičiuojamas visas kursas.

----------

### Žingsnis 3: Mentorius sukuria trečią temą

**Tema 3: "Procentai"**

-   Trukmė: 6 pamokos
-   Vertės koeficientas: 0.5 (lengva tema)

**Sistema perskaičiuoja:**

```
Tema 1 vienetai = 10 × 1.0 = 10
Tema 2 vienetai = 12 × 1.5 = 18
Tema 3 vienetai = 6 × 0.5 = 3

Nepanaudota = 187 - 10 - 12 - 6 = 159 pamokų
Nepanaudotos vienetais = 159 × 1.0 = 159

Viso vienetų = 10 + 18 + 3 + 159 = 190

Tema 1 vertė = 10 / 190 × 100% = 5.26%
Tema 2 vertė = 18 / 190 × 100% = 9.47%
Tema 3 vertė = 3 / 190 × 100% = 1.58%
```

**Sistemos ekranas:**

```
┌────────────────────────────────────────┐
│ Matematika 7A - Kurso planavimas       │
├────────────────────────────────────────┤
│                                        │
│ BUP limitas: 187 pamokos               │
│ Panaudota: 28 pamokos (14.97%)         │
│ Liko planuoti: 159 pamokos (85.03%)    │
│                                        │
│ SUKURTOS TEMOS:                        │
│                                        │
│ 1. Racionalieji skaičiai               │
│    └─ 10 pamokų, koef. 1.0             │
│    └─ Vertė: 5.26%                     │
│    └─ ████░░░░░░░░░░░░░░░░              │
│                                        │
│ 2. Tiesinės funkcijos                  │
│    └─ 12 pamokų, koef. 1.5             │
│    └─ Vertė: 9.47%                     │
│    └─ ████████░░░░░░░░░░                │
│                                        │
│ 3. Procentai                           │
│    └─ 6 pamokos, koef. 0.5             │
│    └─ Vertė: 1.58%                     │
│    └─ █░░░░░░░░░░░░░░░░░░               │
│                                        │
│ NEPANAUDOTA:                           │
│ 159 pamokos = 85.03%                   │
│ (sistema priima kaip 159 temas × 1.0)  │
│                                        │
│ BENDRA SUMA: 100.00% ✓                 │
└────────────────────────────────────────┘
```

----------

### Dinaminis perskaičiavimas

**Kiekvieną kartą sukūrus/redagavus/ištrynus temą:**

1.  ✅ Sistema perskaičiuoja visų temų vertes
2.  ✅ Atnaujina nepanaudotų pamokų skaičių
3.  ✅ Perskaičiuoja mokinio pažangą (jei kursas jau vyksta)
4.  ✅ Atnaujina prognozės

**Pavyzdys - Tema ištrinta:**

```
Prieš: 3 temos (28 pamokos), Nepanaudota: 159
Ištrinome Temą 3

Po: 2 temos (22 pamokos), Nepanaudota: 165
Temos 1 ir 2 vertės automatiškai perskaičiuojamos
```

----------

## Tikslų vertės temoje apskaičiavimas

### Kas yra tikslai?

**Tikslas** - konkretus mokymosi rezultatas temoje.

Pavyzdžiai:

-   ✅ "Išspręsti 10 lygčių su vienu nežinomuoju"
-   ✅ "Nubraižyti funkcijos grafiką pagal formulę"
-   ✅ "Apskaičiuoti procentus 5 praktinėse situacijose"

### Tikslų hierarchija

```
KURSAS (100%)
│
└─ TEMA (pvz. 9.47%)
   │
   ├─ Tikslas 1 (pvz. 2.37%)
   ├─ Tikslas 2 (pvz. 4.74%)
   └─ Tikslas 3 (pvz. 2.37%)
```

### Tikslų parametrai

Kiekvienas tikslas turi **koeficientą**:
| Koeficientas | Sudėtingumas | Pavyzdys |
|--------------|--------------|----------|
| 0.5 | Lengvas | Apibréžti, atpažinti |
| 1.0 | Vidutinis | Apskaičiuoti, taikyti |
| 1.5 | Sudėtingas | Analizuoti, palyginti |
| 2.0 | Labai sudėtingas | Sukurti, įvertinti |

### Skaičiavimo formulė

```
Vieno koeficiento vertė = Temos vertė / Σ(tikslų koeficientų)

Tikslo vertė = Koeficientas × Vieno koeficiento vertė
```

### Pavyzdys

**Tema: "Tiesinės funkcijos" (vertė kurse: 9.47%)**

Mentorius sukuria tikslus:
| # | Tikslas | Koeficientas |
|---|---------|--------------|
| 1 | Suprasti sąvoką | 0.5 |
| 2 | Braižyti grafiką | 1.0 |
| 3 | Spręsti lygtis | 1.0 |
| 4 | Analizuoti | 1.5 |
| 5 | Taikyti praktikoje | 2.0 |

**Skaičiavimas:**

```
Koeficientų suma = 0.5 + 1.0 + 1.0 + 1.5 + 2.0 = 6.0

Vieno koeficiento vertė = 9.47% / 6.0 = 1.58%

Tikslo 1 vertė = 0.5 × 1.58% = 0.79%
Tikslo 2 vertė = 1.0 × 1.58% = 1.58%
Tikslo 3 vertė = 1.0 × 1.58% = 1.58%
Tikslo 4 vertė = 1.5 × 1.58% = 2.37%
Tikslo 5 vertė = 2.0 × 1.58% = 3.16%

Validacija: 0.79% + 1.58% + 1.58% + 2.37% + 3.16% = 9.48% ≈ 9.47% ✓
```

**Rezultatų lentelė:**

| Tikslas | Koef. | Vertė kurso | Vertė temos |
|---------|-------|-------------|-------------|
| 1. Suprasti sąvoką | 0.5 | 0.79% | 8.33% |
| 2. Braižyti grafiką | 1.0 | 1.58% | 16.67% |
| 3. Spręsti lygtis | 1.0 | 1.58% | 16.67% |
| 4. Analizuoti | 1.5 | 2.37% | 25.00% |
| 5. Taikyti praktikoje | 2.0 | 3.16% | 33.33% |
| **VISO** | **6.0** | **9.47%** | **100%** |

**Sistemos ekranas:**

```
┌────────────────────────────────────────┐
│ Tema: Tiesinės funkcijos (9.47%)       │
├────────────────────────────────────────┤
│                                        │
│ TIKSLAI:                               │
│                                        │
│ 1. Suprasti sąvoką                     │
│    └─ Koef: 0.5, Vertė: 0.79%          │
│    └─ █░░░░░░░░░░░░░░░░░░               │
│                                        │
│ 2. Braižyti grafiką                    │
│    └─ Koef: 1.0, Vertė: 1.58%          │
│    └─ ██░░░░░░░░░░░░░░░░                │
│                                        │
│ 3. Spręsti lygtis                      │
│    └─ Koef: 1.0, Vertė: 1.58%          │
│    └─ ██░░░░░░░░░░░░░░░░                │
│                                        │
│ 4. Analizuoti                          │
│    └─ Koef: 1.5, Vertė: 2.37%          │
│    └─ ███░░░░░░░░░░░░░░░                │
│                                        │
│ 5. Taikyti praktikoje                  │
│    └─ Koef: 2.0, Vertė: 3.16%          │
│    └─ ████░░░░░░░░░░░░░░                │
│                                        │
│ BENDRA TEMOS VERTĖ: 9.47% ✓            │
└────────────────────────────────────────┘
```

----------

## Mokinio pažangos skaičiavimas

### Kaip veikia?

Mokinio pažanga = **Suma visų užbaigtų tikslų verčių**

### Tikslo būsenos


| Būsena | Completion % | Pavyzdys |
|--------|--------------|----------|
| 🔵 Nepradėta | 0% | Dar nežiūrėjo medžiagos |
| ⏸️ Vyksta | 1-99% | Skaito, sprendžia pratimus |
| ✅ Užbaigta | 100% | Išlaikė testą |

### Formulė

```
Pasiekta vertė = Tikslo vertė × Completion %

Mokinio pažanga = Σ(Pasiekta vertė)
```

### Pavyzdys

**Mokinys Jonas - Tema "Tiesinės funkcijos":**


| Tikslas | Vertė | Completion | Pasiekta |
|---------|-------|------------|----------|
| 1. Suprasti sąvoką | 0.79% | 100% | 0.79% |
| 2. Braižyti grafiką | 1.58% | 75% | 1.19% |
| 3. Spręsti lygtis | 1.58% | 50% | 0.79% |
| 4. Analizuoti | 2.37% | 0% | 0% |
| 5. Taikyti praktikoje | 3.16% | 0% | 0% |
| **Tema viso** | **9.47%** | **~30%** | **2.77%** |

**Skaičiavimas:**

```
Jonas temoje "Tiesinės funkcijos":
= 0.79% + 1.19% + 0.79% + 0% + 0%
= 2.77% kurso
```

**Visos pažangos skaičiavimas:**

Jei Jonas užbaigė:

-   Tema 1 "Racionalieji skaičiai": 5.26% (100%)
-   Tema 2 "Tiesinės funkcijos": 2.77% (~30%)
-   Tema 3 "Procentai": 0% (nepradėta)

```
Bendra Jonas pažanga = 5.26% + 2.77% + 0% = 8.03%
```

**Sistemos ekranas:**

```
┌────────────────────────────────────────┐
│ Jonas Petraitis - Matematika 7A        │
├────────────────────────────────────────┤
│                                        │
│ PAŽANGA: 8.03% / 100%                  │
│ ████░░░░░░░░░░░░░░░░░░░░░░░░░░░░        │
│                                        │
│ TEMOS:                                 │
│                                        │
│ ✅ Racionalieji skaičiai (100%)        │
│    └─ 5.26% pasiekta                   │
│                                        │
│ 🔄 Tiesinės funkcijos (~30%)           │
│    └─ 2.77% pasiekta iš 9.47%          │
│    ├─ ✅ Suprasti sąvoką (100%)        │
│    ├─ 🔄 Braižyti grafiką (75%)        │
│    ├─ 🔄 Spręsti lygtis (50%)          │
│    ├─ ⏸️  Analizuoti (0%)              │
│    └─ ⏸️  Taikyti praktikoje (0%)      │
│                                        │
│ ⏸️  Procentai (0%)                     │
│    └─ 0% pasiekta                      │
│                                        │
│ + Nepanaudota: 159 temos (85.03%)      │
│                                        │
│ REALI PAŽANGA KURSE: 8.03% ✓           │
│ (Ne 50%, kaip rodytų senoji sistema!)  │
└────────────────────────────────────────┘
```

**⭐ Svarbu:** Sistema rodo **tikrą** pažangą kurse, įskaitant dar nesuplanuotas temas!

----------

## Produktyvumo skaičiavimas

### Kas yra produktyvumas?

**Produktyvumas** rodo, ar mokinys mokosi:

-   ⚡ **Greičiau** nei planuota (>100%)
-   ➡️ **Planuotu tempu** (=100%)
-   🐌 **Lėčiau** nei planuota (<100%)

### Formulė

```
Produktyvumas = (Pasiekta pažanga / Planuota pažanga) × 100%
```

### Planuotos pažangos skaičiavimas

```
Planuota = (Praėjusios dienos / Visa kurso trukmė) × 100%
```

### Pavyzdys

**Jonas Petraitis:**

```
Kursas: 180 dienų (rugsėjis–kovas)
Praėjo: 45 dienos
Pasiekta: 8.03%

Planuota = (45 / 180) × 100% = 25%
Produktyvumas = (8.03% / 25%) × 100% = 32.1%
```

**Statusas:** 🔴 **Kritiškai žemas** - Skubi intervencija!

### Produktyvumo statusai


| Procentas | Statusas | Reikšmė |
|-----------|----------|---------|
| < 70% | 🔴 Kritiškai žemas | Mentoriaus intervencija |
| 70-85% | 🟠 Žemas | Reikalinga pagalba |
| 85-100% | 🟡 Žemiau normos | Stebėti |
| 100-115% | 🟢 Normalus | Viskas gerai |
| 115-130% | 🟢 Virš normos | Puikiai |
| 130-150% | 🔵 Aukštas | Labai gerai |
| > 150% | 🟣 Išskirtinis | Ekspertinis lygis |

### Prognozė užbaigimo

```
Vidutinis greitis = Pasiekta / Praėjusios dienos
Liko = 100% - Pasiekta
Liko dienų = Liko / Vidutinis greitis
Prognozuojama data = Dabar + Liko dienų
```

**Jonas pavyzdys:**

```
Vidutinis greitis = 8.03% / 45d = 0.178% per dieną
Liko = 100% - 8.03% = 91.97%
Liko dienų = 91.97% / 0.178% = 516 dienų

Prognozuojama data = Dabar + 516d = 561 diena
Vėlavimas = 561 - 180 = 381 diena ⚠️⚠️⚠️
```

**⚠️ KRITINIS ATVEJIS - Būtina mentoriaus intervencija!**

----------

## Praktinis pavyzdys

### Scenarijus

**Kursas:** Matematika 7 klasė  
**BUP limitas:** 187 pamokos  
**Trukmė:** 180 dienų (2025-09-01 iki 2026-03-01)  
**Mokiniai:** Jonas ir Ona  
**Dabartinė data:** 2025-10-15 (45 dienos praėjo)

----------

### 1 dalis: Mentorius planuoja kursą

#### Savaitė 1 - Pirmosios 3 temos


| Tema | Trukmė | Koef. | Vienetai |
|------|---------|-------|----------|
| 1. Racionalieji skaičiai | 10 pamokų | 1.0 | 10 |
| 2. Tiesinės funkcijos | 12 pamokų | 1.5 | 18 |
| 3. Procentai | 6 pamokos | 0.5 | 3 |

**Sistema skaičiuoja:**

```
Sukurtos temos: 28 pamokos = 31 vienetas
Nepanaudota: 159 pamokų = 159 vienetai
Viso: 190 vienetų

Tema 1: 10 / 190 × 100% = 5.26%
Tema 2: 18 / 190 × 100% = 9.47%
Tema 3: 3 / 190 × 100% = 1.58%
Nepanaudota: 159 / 190 × 100% = 83.68%
```

#### Savaitė 2 - Pridedamos dar 2 temos


| Tema | Trukmė | Koef. | Vienetai |
|------|---------|-------|----------|
| 4. Geometrijos įvadas | 15 pamokų | 1.5 | 22.5 |
| 5. Statistika | 8 pamokos | 1.0 | 8 |

**Sistema perskaičiuoja:**

```
Tema 1-3: 31 vienetas (kaip anksčiau)
Tema 4: 22.5 vienetų
Tema 5: 8 vienetai
Sukurtos: 51 pamoka = 61.5 vienetų

Nepanaudota: 187 - 51 = 136 pamokų = 136 vienetų
Viso: 197.5 vienetų

Tema 1: 10 / 197.5 × 100% = 5.06%
Tema 2: 18 / 197.5 × 100% = 9.11%
Tema 3: 3 / 197.5 × 100% = 1.52%
Tema 4: 22.5 / 197.5 × 100% = 11.39%
Tema 5: 8 / 197.5 × 100% = 4.05%
Nepanaudota: 136 / 197.5 × 100% = 68.86%
```

**Pastaba:** Pirmos 3 temos vertės **sumažėjo**, nes pridėjus naujas temas perskaičiuojamas visas kursas.

#### Savaitė 4 - Pridedama kontrolinis ir projektas


| Tema | Trukmė | Koef. | Vienetai |
|------|---------|-------|----------|
| 6. Kontrolinis darbas | 2 pamokos | 2.0 | 4 |
| 7. Baigiamasis projektas | 20 pamokų | 3.0 | 60 |

**Sistema perskaičiuoja:**

```
Tema 1-5: 61.5 vienetų
Tema 6: 4 vienetai
Tema 7: 60 vienetų
Sukurtos: 73 pamokos = 125.5 vienetų

Nepanaudota: 187 - 73 = 114 pamokų = 114 vienetų
Viso: 239.5 vienetų

Tema 1: 10 / 239.5 × 100% = 4.18%
Tema 2: 18 / 239.5 × 100% = 7.52%
Tema 3: 3 / 239.5 × 100% = 1.25%
Tema 4: 22.5 / 239.5 × 100% = 9.39%
Tema 5: 8 / 239.5 × 100% = 3.34%
Tema 6: 4 / 239.5 × 100% = 1.67%
Tema 7: 60 / 239.5 × 100% = 25.05%
Nepanaudota: 114 / 239.5 × 100% = 47.60%
```

#### Galutinis kurso planas (po 4 savaičių)

```
┌────────────────────────────────────────────────┐
│ MATEMATIKA 7A - KURSO PLANAS                   │
├────────────────────────────────────────────────┤
│                                                │
│ BUP limitas: 187 pamokos                       │
│ Suplanuota: 73 pamokos (39.04%)                │
│ Liko planuoti: 114 pamokų (60.96%)             │
│                                                │
│ SUKURTOS TEMOS:                                │
│                                                │
│ 1. Racionalieji skaičiai                       │
│    └─ 10 pamokų × koef. 1.0 = 4.18%            │
│                                                │
│ 2. Tiesinės funkcijos                          │
│    └─ 12 pamokų × koef. 1.5 = 7.52%            │
│                                                │
│ 3. Procentai                                   │
│    └─ 6 pamokos × koef. 0.5 = 1.25%            │
│                                                │
│ 4. Geometrijos įvadas                          │
│    └─ 15 pamokų × koef. 1.5 = 9.39%            │
│                                                │
│ 5. Statistika                                  │
│    └─ 8 pamokos × koef. 1.0 = 3.34%            │
│                                                │
│ 6. Kontrolinis darbas                          │
│    └─ 2 pamokos × koef. 2.0 = 1.67%            │
│                                                │
│ 7. Baigiamasis projektas                       │
│    └─ 20 pamokų × koef. 3.0 = 25.05%           │
│                                                │
│ SUPLANUOTA VISO: 52.40%                        │
│                                                │
│ NEPANAUDOTA: 114 pamokų = 47.60%               │
│ (sistema priima kaip 114 temų × koef. 1.0)     │
│                                                │
│ KURSO SUMA: 100.00% ✓                          │
└────────────────────────────────────────────────┘
```

----------

### 2 dalis: Tikslai temoje "Tiesinės funkcijos"

**Tema vertė:** 7.52%

Mentorius sukuria tikslus:


| # | Tikslas | Koef. |
|---|---------|-------|
| 1 | Suprasti tiesinės funkcijos sąvoką | 0.5 |
| 2 | Nustatyti funkcijos parametrus | 1.0 |
| 3 | Braižyti funkcijos grafiką | 1.0 |
| 4 | Spręsti lygtis grafiškai | 1.5 |
| 5 | Analizuoti funkcijų savybes | 1.5 |
| 6 | Taikyti praktikoje | 2.0 |

**Sistema skaičiuoja:**

```
Koeficientų suma: 0.5 + 1.0 + 1.0 + 1.5 + 1.5 + 2.0 = 7.5

Vieno koeficiento vertė: 7.52% / 7.5 = 1.00%

Tikslas 1: 0.5 × 1.00% = 0.50%
Tikslas 2: 1.0 × 1.00% = 1.00%
Tikslas 3: 1.0 × 1.00% = 1.00%
Tikslas 4: 1.5 × 1.00% = 1.50%
Tikslas 5: 1.5 × 1.00% = 1.50%
Tikslas 6: 2.0 × 1.00% = 2.01% (adjustment)

Validacija: 0.50% + 1.00% + 1.00% + 1.50% + 1.50% + 2.01% = 7.51% ≈ 7.52% ✓
```

----------

### 3 dalis: Jono pažanga (po 45 dienų)

#### Tema 1: Racionalieji skaičiai (4.18%)

```
✅ Visa tema užbaigta
Pasiekta: 4.18%
```

#### Tema 2: Tiesinės funkcijos (7.52%)


| Tikslas | Vertė | Completion | Pasiekta |
|---------|-------|------------|----------|
| 1. Suprasti sąvoką | 0.50% | 100% | 0.50% |
| 2. Nustatyti parametrus | 1.00% | 100% | 1.00% |
| 3. Braižyti grafiką | 1.00% | 75% | 0.75% |
| 4. Spręsti grafiškai | 1.50% | 25% | 0.38% |
| 5. Analizuoti | 1.50% | 0% | 0% |
| 6. Taikyti praktikoje | 2.01% | 0% | 0% |
| **Tema viso** | **7.52%** | **~35%** | **2.63%** |

#### Tema 3: Procentai (1.25%)

```
🔄 Pradėta, 60% užbaigta
Pasiekta: 0.75%
```

#### Temos 4-7

```
⏸️ Nepradėtos
Pasiekta: 0%
```

#### Jono bendra pažanga

```
Tema 1: 4.18%
Tema 2: 2.63%
Tema 3: 0.75%
Temos 4-7: 0%
Nepanaudota: 0% (dar nesimoko)

BENDRA PAŽANGA: 7.56%
```

----------

### 4 dalis: Onos pažanga (po 45 dienų)

#### Tema 1: Racionalieji skaičiai (4.18%)

```
✅ Visa tema užbaigta
Pasiekta: 4.18%
```

#### Tema 2: Tiesinės funkcijos (7.52%)

```
✅ Visa tema užbaigta
Pasiekta: 7.52%
```

#### Tema 3: Procentai (1.25%)

```
✅ Visa tema užbaigta
Pasiekta: 1.25%
```

#### Tema 4: Geometrijos įvadas (9.39%)


| Tikslo grupė | Completion | Pasiekta |
|--------------|------------|----------|
| Pusė temos | 50% | 4.70% |

#### Temos 5-7

```
⏸️ Nepradėtos
Pasiekta: 0%
```

#### Onos bendra pažanga

```
Tema 1: 4.18%
Tema 2: 7.52%
Tema 3: 1.25%
Tema 4: 4.70%
Temos 5-7: 0%

BENDRA PAŽANGA: 17.65%
```

----------

### 5 dalis: Produktyvumo palyginimas

#### Planuota pažanga (po 45 dienų)

```
Kursas: 180 dienų
Praėjo: 45 dienos

Planuota = (45 / 180) × 100% = 25%
```

#### Jonas

```
Pasiekta: 7.56%
Planuota: 25%
Produktyvumas = (7.56% / 25%) × 100% = 30.2%
```

**Statusas:** 🔴 **KRITIŠKAI ŽEMAS!**

**Prognozė:**

```
Vidutinis greitis: 7.56% / 45d = 0.168% per dieną
Liko: 92.44%
Liko dienų: 92.44% / 0.168% = 550 dienų
Užbaigs: 595 diena (vietoje 180)
Vėlavimas: 415 dienų ⚠️⚠️⚠️
```

#### Ona

```
Pasiekta: 17.65%
Planuota: 25%
Produktyvumas = (17.65% / 25%) × 100% = 70.6%
```

**Statusas:** 🟠 **ŽEMAS** - Reikia pagalbos

**Prognozė:**

```
Vidutinis greitis: 17.65% / 45d = 0.392% per dieną
Liko: 82.35%
Liko dienų: 82.35% / 0.392% = 210 dienų
Užbaigs: 255 diena (vietoje 180)
Vėlavimas: 75 dienos ⚠️
```

----------

### 6 dalis: Palyginamosios ataskaitos

#### Klasės overview

```
┌────────────────────────────────────────────────┐
│ MATEMATIKA 7A - KLASĖS ATASKAITA               │
│ Data: 2025-10-15 (45 dienos nuo pradžios)      │
├────────────────────────────────────────────────┤
│                                                │
│ Mokinių: 2                                     │
│ Vidutinė pažanga: 12.61%                       │
│ Vidutinis produktyvumas: 50.4%                 │
│                                                │
│ PRODUKTYVUMO PASISKIRSTYMAS:                   │
│ 🔴 < 70%: 2 mokiniai (100%)                    │
│ 🟠 70-85%: 0 mokinių (0%)                      │
│ 🟢 > 85%: 0 mokinių (0%)                       │
│                                                │
│ DETALI INFORMACIJA:                            │
│                                                │
│ 1. Ona Stankevičiūtė                           │
│    ├─ Pažanga: 17.65% / 100%                   │
│    ├─ Planuota: 25%                            │
│    ├─ Produktyvumas: 70.6% 🟠                  │
│    ├─ Temos užbaigtos: 3                       │
│    ├─ Temos vyksta: 1                          │
│    └─ Prognozė: +75d vėlavimas                 │
│                                                │
│ 2. Jonas Petraitis                             │
│    ├─ Pažanga: 7.56% / 100%                    │
│    ├─ Planuota: 25%                            │
│    ├─ Produktyvumas: 30.2% 🔴 KRITINIS!        │
│    ├─ Temos užbaigtos: 1                       │
│    ├─ Temos vyksta: 2                          │
│    └─ Prognozė: +415d vėlavimas                │
│                                                │
│ ⚠️ REIKALAUJA DĖMESIO:                         │
│ - Jonas Petraitis (SKUBI INTERVENCIJA!)        │
│ - Ona Stankevičiūtė (konsultacija)             │
│                                                │
│ REKOMENDACIJOS:                                │
│ 1. Jonas - individuali konsultacija ŠIANDIEN   │
│ 2. Ona - papildomos pamokos                    │
│ 3. Peržiūrėti temų sudėtingumą                 │
└────────────────────────────────────────────────┘
```

----------

### 7 dalis: Sistemos ekranų pavyzdžiai

#### Jono dashboard

```
┌────────────────────────────────────────────────┐
│ 👤 JONAS PETRAITIS                             │
│ Matematika 7A                                  │
├────────────────────────────────────────────────┤
│                                                │
│ MANO PAŽANGA                                   │
│ 7.56% ███░░░░░░░░░░░░░░░░░░░░░░░░░░░            │
│                                                │
│ Pasiekta: 7.56%                                │
│ Planuota: 25%                                  │
│ Skirtumas: -17.44% (ATSILIKAI!) ⚠️             │
│                                                │
│ PRODUKTYVUMAS                                  │
│ 30.2% 🔴 KRITIŠKAI ŽEMAS                       │
│                                                │
│ ⚠️ Tau reikia pagalbos!                        │
│ Pasitark su mentoriumi kuo greičiau.           │
│                                                │
│ MANO TEMOS:                                    │
│                                                │
│ ✅ Racionalieji skaičiai (100%)                │
│    └─ 4.18% pasiekta                           │
│    └─ Praleista: 3h 20min                      │
│                                                │
│ 🔄 Tiesinės funkcijos (35%)                    │
│    └─ 2.63% pasiekta iš 7.52%                  │
│    └─ Praleista: 2h 45min                      │
│    │                                           │
│    ├─ ✅ Suprasti sąvoką                       │
│    ├─ ✅ Nustatyti parametrus                  │
│    ├─ 🔄 Braižyti grafiką (75%)                │
│    ├─ 🔄 Spręsti grafiškai (25%)               │
│    ├─ ⏸️ Analizuoti (0%)                       │
│    └─ ⏸️ Taikyti praktikoje (0%)               │
│                                                │
│ 🔄 Procentai (60%)                             │
│    └─ 0.75% pasiekta iš 1.25%                  │
│                                                │
│ ⏸️ Geometrijos įvadas (0%)                     │
│ ⏸️ Statistika (0%)                             │
│ ⏸️ Kontrolinis darbas (0%)                     │
│ ⏸️ Baigiamasis projektas (0%)                  │
│                                                │
│ PROGNOZĖ                                       │
│ Esamu tempu baigsi: 2027-04-19                 │
│ Vėlavimas: ~415 dienų                          │
│                                                │
│ KĄ DARYTI?                                     │
│ 1. Susitikti su mentoriumi ŠIANDIEN            │
│ 2. Skirti daugiau laiko kasdien                │
│ 3. Paprašyti pagalbos su temomis               │
│                                                │
│ [Susitarti konsultacijai] [Žiūrėti medžiagą]  │
└────────────────────────────────────────────────┘
```

#### Onos dashboard

```
┌────────────────────────────────────────────────┐
│ 👤 ONA STANKEVIČIŪTĖ                           │
│ Matematika 7A                                  │
├────────────────────────────────────────────────┤
│                                                │
│ MANO PAŽANGA                                   │
│ 17.65% ████████░░░░░░░░░░░░░░░░░░░░             │
│                                                │
│ Pasiekta: 17.65%                               │
│ Planuota: 25%                                  │
│ Skirtumas: -7.35% (truputį atsilikusi)         │
│                                                │
│ PRODUKTYVUMAS                                  │
│ 70.6% 🟠 Žemas                                 │
│                                                │
│ Dirbi gerai, bet gali greičiau! 💪             │
│                                                │
│ MANO TEMOS:                                    │
│                                                │
│ ✅ Racionalieji skaičiai (100%)                │
│ ✅ Tiesinės funkcijos (100%)                   │
│ ✅ Procentai (100%)                            │
│                                                │
│ 🔄 Geometrijos įvadas (50%)                    │
│    └─ 4.70% pasiekta iš 9.39%                  │
│    └─ Liko ~7 pamokos                          │
│                                                │
│ ⏸️ Statistika (0%)                             │
│ ⏸️ Kontrolinis darbas (0%)                     │
│ ⏸️ Baigiamasis projektas (0%)                  │
│                                                │
│ PROGNOZĖ                                       │
│ Esamu tempu baigsi: 2026-05-15                 │
│ Vėlavimas: ~75 dienos                          │
│                                                │
│ PATARIMAI                                      │
│ • Pagreitink truputį tempą                     │
│ • Skirkgeometrijos užduotims daugiau laiko     │
│ • Planuok 1h kasdien                           │
│                                                │
│ [Tęsti mokymąsi] [Žiūrėti tvarkaraštį]         │
└────────────────────────────────────────────────┘
```

----------

## Dažniausiai užduodami klausimai

### 1. Kodėl temų vertės keičiasi pridedant naujas temas?

**Atsakymas:** Sistema **dinamiškai perskaičiuoja** visas vertes, nes nepanaudotų pamokų skaičius keičiasi.

**Pavyzdys:**

```
Pradžioje:
- Tema 1: 10 vienetų
- Nepanaudota: 177 vienetų
- Viso: 187 vienetų
- Tema 1 vertė: 10/187 = 5.35%

Pridėjus Temą 2:
- Tema 1: 10 vienetų
- Tema 2: 18 vienetų
- Nepanaudota: 159 vienetų
- Viso: 187 vienetų
- Tema 1 vertė: 10/187 = 5.35% (NEKITO, nes viso vienetų suma nepasikeitė)

Bet jei Tema 2 turi kitą koeficientą:
- Tema 2: 12 pamokų × 1.5 = 18 vienetų (ne 12!)
- Viso vienetų: 10 + 18 + 159 = 187 (bet pamokos buvo 22, ne 187)
- Atsiranda neatitikimas!

Teisingas skaičiavimas:
Nepanaudota = 187 - 10 - 12 = 165 pamokų = 165 vienetų
Viso = 10 + 18 + 165 = 193 vienetai
Tema 1 = 10/193 = 5.18% (sumažėjo!)
```

**Išvada:** Kuo didesni koeficientai, tuo daugiau "vienetų" sistemoje, tuo mažesnė kiekvieno elemento procentinė dalis.

### 2. Ar mokinys mato nepanaudotas pamokas savo pažangoje?

**Atsakymas:** **NE**. Nepanaudotos pamokos naudojamos **tik skaičiuojant temų vertes**, bet mokinio pažangoje rodomos tik **sukurtos temos**.

**Pavyzdys:**

```
Sistema skaičiuoja:
- Tema 1: 5.26%
- Tema 2: 9.47%
- Nepanaudota: 85.27%
- VISO: 100%

Mokiniui rodoma:
- Tema 1: 5.26%
- Tema 2: 9.47%
- + Dar bus sukurta ~30 temų (85.27%)
- "Tu pasiekei: 7% iš 100% kurso"
```

### 3. Ar galima keisti temos trukmę/koeficientą jau vykstant kursui?

**Atsakymas:** **TAIP**, bet:

-   ⚠️ Sistema perskaičiuos **visų temų** vertes
-   ⚠️ Mokinio pažanga bus **proporcingai pakoreguota**
-   ⚠️ Produktyvumas gali **šoktelėti** arba **nukristi**

**Pavyzdys:**

```
Prieš:
- Tema 1: 10 pamokų, koef. 1.0, vertė 5.26%
- Jonas užbaigė: 5.26%

Mentorius pakeičia:
- Tema 1: 10 pamokų, koef. 0.5, vertė 2.74%

Po:
- Jonas vis tiek rodoma: 2.74% (ne 5.26%!)
- Jo pažanga sumažėjo nuo 5.26% į 2.74%
```

**Rekomendacija:** Pirmąsias 2 savaites - aktyviai planuoti ir koreguoti. Po to - stabilizuoti.

### 4. Kas nutinka, jei mentorius viršija BUP limitą?

**Atsakymas:** Sistema **leidžia** viršyti, bet **perspėja**.

**Pavyzdys:**

```
BUP limitas: 187 pamokos
Mentorius suplanuoja: 195 pamokas

Sistema:
⚠️ "Viršijote BUP limitą 8 pamokomis (4.3%)"
⚠️ "Patikrinkite ar tikrai reikia tiek laiko"

Bet LEIDŽIA tęsti ✅
```

**Kodėl leidžia?**

-   Kai kuriems mokiniams gali reikėti daugiau laiko
-   Mentorius gali kompensuoti kituose dalykuose
-   Realybė ≠ idealus planas

### 5. Ar sistema įskaičiuoja nepamokų laiką (atostogos, ligos)?

**Atsakymas:** **NE**, sistema skaičiuoja tik **kalendorines dienas**.

**Pavyzdys:**

```
Kursas: 180 dienų (rugsėjis–kovas)
Mokinys sirgo: 10 dienų

Sistema vis tiek skaičiuoja:
Praėjo = 45 dienos (įskaitant ligos dienas)
Planuota = (45/180) × 100% = 25%
```

**Sprendimas:** Mentorius gali **pratęsti kursą** mokiniui:

```
Naujas terminas: 180 + 10 = 190 dienų
Sistema perskaičiuos produktyvumą
```

### 6. Kaip sistema skaičiuoja prognozę, jei mokinys mokosi netolygiai?

**Atsakymas:** Sistema naudoja **vidutinį greitį** nuo kurso pradžios.

**Pavyzdys:**

```
Savaitė 1-2: Labai aktyvus (5% per 2 savaites)
Savaitė 3-4: Sulėtėjo (1% per 2 savaites)
Savaitė 5-6: Vėl aktyvus (4% per 2 savaites)

Vidutinis greitis = 10% / 42d = 0.238% per dieną
Prognozė = 90% / 0.238% = 378 dienos
```

**Pastaba:** Prognozė **kinta** kiekvieną dieną pagal naują vidutinį greitį.

### 7. Ar galima turėti temą be tikslų?

**Atsakymas:** **TAIP**, bet:

-   ⚠️ Mentoriui nebus ką žymėti kaip "užbaigta"
-   ⚠️ Pažanga neaugs
-   ⚠️ Sistema laikys temą "0% užbaigta"
-   ⚠️ Galima taikyti, kad pamokos tikslas išklausyti

**Rekomendacija:** Kiekviena tema turėtų turėti **bent 1 tikslą**.

### 8. Ar mokinys gali "praleisti" temą?

**Atsakymas:** **TAIP**. Mokinys gali:

-   Pradėti Temą 3 nepradėjęs Temos 2
-   Užbaigti temas nesilaikant nustatytos eigos ypač jei dirba savarankiškai
-   Grįžti prie senų temų

**Pavyzdys:**

```
Mokinys:
- ✅ Tema 1 (100%)
- ⏸️ Tema 2 (0%) - praleido
- 🔄 Tema 3 (50%) - mokosi dabar

Pažanga = Tema 1 + Tema 3 = 5.26% + 0.63% = 5.89%
```

**Sistema neblokuoja** - mokinys mokosi savo tempu.

### 9. Kaip veikia "completion %" tikslui?

**Atsakymas:** Mentorius/mokinys **rankiniu būdu** nustato:

-   **0%** - Nepradėta
-   **25%** - Pradėjo skaityti medžiagą
-   **50%** - Suprato koncepciją
-   **75%** - Atliko pratimus
-   **100%** - Išlaikė testą / įvykdė reikalavimus

**Pavyzdys:**

```
Tikslas: "Braižyti grafiką" (vertė 1.58%)

Mokinys:
- Perskaitė teoriją → 25%
  Pasiekta: 1.58% × 25% = 0.40%

- Išsprendė 5 pratimus → 50%
  Pasiekta: 1.58% × 50% = 0.79%

- Išlaikė testą → 100%
  Pasiekta: 1.58% × 100% = 1.58%
```

### 10. Ar sistema automatiškai žymi tikslus kaip "užbaigta"?

**Atsakymas:** **NE**. Sistema **nežino** kada tikslas pasiektas.

**Kas žymi:**

-   **Mokinys** - žymi save (self-assessment)
-   **Mentorius** - tvirtina/koreguoja
-   **Sistema** - automatiškai žymi tik jei mokinys išlaiko testą (jei integruota)

**Rekomendacija:**

```
Geriausias variantas:
1. Mokinys pažymi "užbaigta"
2. Mentorius patvirtina/koreguoja
3. Sistema fiksuoja galutinį completion %
```

----------

## Santrauka

### Pagrindinės formulės

#### 1. Temos vertė

```
Temos vienetai = Trukmė (pamokos) × Vertės koeficientas

Viso vienetų = Σ(sukurtų temų vienetai) + (Nepanaudotos pamokos × 1.0)

Temos vertė (%) = (Temos vienetai / Viso vienetų) × 100%
```

#### 2. Tikslo vertė

```
Vieno koeficiento vertė = Temos vertė / Σ(tikslų koeficientų)

Tikslo vertė = Tikslo koeficientas × Vieno koeficiento vertė
```

#### 3. Mokinio pažanga

```
Pasiekta vertė = Tikslo vertė × Completion %

Mokinio pažanga = Σ(Pasiekta vertė visų tikslų)
```

#### 4. Produktyvumas

```
Planuota = (Praėjusios dienos / Visa kurso trukmė) × 100%

Produktyvumas = (Pasiekta pažanga / Planuota) × 100%
```

#### 5. Prognozė

```
Vidutinis greitis = Pasiekta / Praėjusios dienos

Liko dienų = (100% - Pasiekta) / Vidutinis greitis

Prognozuojama data = Šiandien + Liko dienų
```

----------

### Greita referentinė lentelė

#### BUP limito skaičiavimas

| Dalykas | BUP val/metus | Pamokos (45min) |
|---------|---------------|-----------------|
| Lietuvių kalba | 175 | 233 |
| Anglų kalba | 105 | 140 |
| Matematika | 140 | 187 |
| Istorija | 70 | 93 |
| Fizika | 70 | 93 |
| Biologija | 70 | 93 |

#### Temų vertės koeficientai (pavyzdžiai)


| Koef. | Tipas | Trukmė | Pavyzdys |
|-------|-------|---------|----------|
| 0.3 | Trumpa | 2-3 pamokos | Įvadinė apžvalga |
| 0.5 | Lengva | 4-6 pamokos | Pratybos, kartojimas |
| 1.0 | Standartinė | 8-12 pamokų | Nauja medžiaga |
| 1.5 | Sudėtinga | 12-15 pamokų | Sudėtinga tema |
| 2.0 | Labai svarbi | 15-20 pamokų | Laboratorinis, projektas |
| 3.0 | Kritinė | 20+ pamokų | Egzaminas, diplomas |

#### Tikslų koeficientai (Bloom taksonomija)


| Koef. | Lygis | Veiksmai | Pavyzdys |
|-------|-------|----------|----------|
| 0.5 | Žinojimas | Apibréžti, įvardyti | "Išvardinti 5 sąvokas" |
| 1.0 | Supratimas/Taikymas | Paaiškinti, apskaičiuoti | "Išspręsti 10 uždavinių" |
| 1.5 | Analizė | Palyginti, išskirti | "Palyginti 3 metodus" |
| 2.0 | Sintezė/Vertinimas | Sukurti, įvertinti | "Sukurti projektą" |

#### Produktyvumo interpretacija
| Produktyvumas | Emoji | Statusas | Veiksmai |
|---------------|-------|----------|----------|
| 0-30% | 🔴 | Kritinis | SKUBI intervencija! |
| 30-50% | 🔴 | Labai žemas | Individuali konsultacija |
| 50-70% | 🔴 | Kritiškai žemas | Mentorius + pagalbos planas |
| 70-85% | 🟠 | Žemas | Papildomos konsultacijos |
| 85-100% | 🟡 | Žemiau normos | Stebėti, skatinti |
| 100-115% | 🟢 | Normalus | Palaikyti tempą |
| 115-130% | 🟢 | Virš normos | Pagirti, palaikyti |
| 130-150% | 🔵 | Aukštas | Pasidyti iššūkių |
| 150%+ | 🟣 | Išskirtinis | Pažangesnė medžiaga |

----------

## Naudos administracijai

### ✅ Tikslesnė pažangos apskaita

```
Mentorius sukūrė 5 temas iš 187 pamokų
Mokinys užbaigė 3 temas
Sistema: "8% kurso užbaigta"
Realybė: ~8% kurso užbaigta ✅
```

### ✅ Lankstumas planuojant

**Pranašumai:**

-   📝 Mentorius gali kurti temas laipsniškai
-   📝 Ne būtina planuoti viso kurso iš karto
-   📝 Galima koreguoti dinamiškai
-   📝 Sistema automatiškai perskaičiuoja

### ✅ Realistinės prognozės

**Ką sistema rodo:**

```
"Jonas: +415 dienų vėlavimas"
ne
"Jonas: 30% užbaigta" (klaidinantis metrikos)
```

### ✅ Ankstyvasis perspėjimas

Sistema aptinka problemas **anksčiau**:

```
Sena sistema:
- Savaitė 4: "20% užbaigta" → Atrodo gerai ✅
- Savaitė 20: "Oh ne, jis atsiliko!" ❌

Nauja sistema:
- Savaitė 4: "5% užbaigta, produktyvumas 30%" 🔴
- Intervencija vyksta DABAR ✅
```

### ✅ BUP atitikimas

Sistema **stebi** BUP limitą:

```
┌────────────────────────────────────┐
│ BUP ATITIKIMAS                     │
├────────────────────────────────────┤
│ BUP limitas: 187 pamokos           │
│ Suplanuota: 195 pamokos            │
│ Viršyta: +8 pamokos (4.3%)         │
│                                    │
│ ⚠️ Peržiūrėkite planuojamą apimtį │
└────────────────────────────────────┘
```

----------

## Praktiniai patarimai

### Mokytojams - Kaip planuoti efektyviai

#### Savaitė 1-2: Bazinės temos (20-30% kurso)

Sukurti **svarbiausias/lengviausias** temas:

```
✅ Įvadinė tema
✅ 2-3 bazinės temos
✅ Pirmasis kontrolinis

Kodėl?
- Mokiniai gali pradėti mokytis
- Matoma pradinė pažanga
- Testuojama sistema
```

#### Savaitė 3-4: Pagrindinės temos (40-50% kurso)

Pridėti **pagrindines** temas:

```
✅ Standartinės temos
✅ Pratybų temos
✅ Antrasis kontrolinis

Kodėl?
- Kurso struktūra aiškesnė
- Mokiniai mato kelią į priekį
```

#### Savaitė 5-6: Sudėtingos temos (60-80% kurso)

Pridėti **sudėtingas/projektinius** temas:

```
✅ Sudėtingos temos
✅ Laboratoriniai darbai
✅ Projektai

Kodėl?
- Balansuojama kurso apimtis
- Galutinis planavimas
```

#### Savaitė 7+: Finalizavimas (80-100% kurso)

Užpildyti **likusias** temas:

```
✅ Papildomos temos
✅ Baigiamieji darbai
✅ Kartojimas

Kodėl?
- Kurso struktūra užbaigta
- Sistema stabilizuota
```

### Mokiniams - Kaip sekti savo pažangą

#### Kasdien:

```
📅 Užbaigti bent 1 tikslą
📊 Patikrinti produktyvumą
🎯 Planuoti rytojaus užduotis
```

#### Kas savaitę:

```
📈 Peržiūrėti savaitės pažangą
📋 Palyginti su planuota
💬 Konsultuotis jei produktyvumas < 85%
```

#### Kas mėnesį:

```
📊 Analizuoti tendencijas
🎯 Koreguoti mokymosi strategiją
🏆 Švęsti pasiekimus
```

### Mentoriams - Kaip stebėti klasę

#### Kasdien (5 min):

```
👀 Peržiūrėti alert'us
🔴 Reaguoti į kritines situacijas
💬 Atsakyti į mokinių klausimus
```

#### Kas savaitę (30 min):

```
📊 Klasės produktyvumo ataskaita
👥 Identifikuoti rizikos mokinius
📝 Planuoti intervencijas
```

#### Kas mėnesį (1-2 val):

```
📈 Tendencijų analizė
🎯 Veiksmų plano peržiūra
📋 Kurso plano koregavimas
🏆 Pažymėti geriausius rezultatus
```

----------

## Sistemos privalumai vs Trūkumai

### ✅ Privalumai

**1. Tikslumas**

```
Mokinio pažanga atspindi TIKRĄ progresą kurse,
ne tik užbaigtų temų procentą.
```

**2. Lankstumas**

```
Mentorius gali kurti temas laipsniškai,
sistema automatiškai perskaičiuoja.
```

**3. Realybės atspindėjimas**

```
Sistema leidžia viršyti/neužpildyti BUP limito,
nes realybėje taip ir būna.
```

**4. Ankstyvasis perspėjimas**

```
Problemos aptinkamos ANKSČIAU,
intervencijos efektyvesnės.
```

**5. Skaidrumas**

```
Visi (mokinys, mentorius, tėvai) mato tą patį,
nėra nesusipratimų.
```

### ⚠️ Iššūkiai/Apribojimai

**1. Dinamiškos vertės**

```
Temų vertės keičiasi pridedant naujas temas.
Gali sukelti sumaištį pradžioje.

Sprendimas: Aiškiai paaiškinti mokiniams.
```

**2. Planavimo našta**

```
Mentorius turi nurodyti trukmę IR koeficientą.
Daugiau parametrų = daugiau darbo.

Sprendimas: Pradėti su default koeficientais (1.0).
```

**3. Žema pradinė pažanga**

```
Pradžioje mokinys mato mažą pažangą (5-10%),
gali demotyvuoti.

Sprendimas: Paaiškinti, kad tai normalus procesas.
```

**4. Koeficientų subjektyvumas**

```
Skirtingi mokytojai gali skirti skirtingus koeficientus
tam pačiam turiniui.

Sprendimas: Metodinės gairės/pavyzdžiai.
```
