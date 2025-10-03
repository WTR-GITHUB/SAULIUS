
# Savarankiško darbo sluoksnis - Formulės ir logika

**Versija:** 1.0  
**Data:** 2025-10-03

## Pagrindinė koncepcija
KURSAS = Pamokos (0-100%) + Savarankiškas darbas (0-∞%)
Galutinė pažanga = Pamokų pažanga + Savarankiško darbo pažanga


## 1. Savarankiško darbo struktūra

## 1. Savarankiško darbo struktūra
```
Savarankiškas darbas:
├─ Pavadinimas
├─ Trukmė (valandos, ne pamokos!)
├─ Vertės koeficientas
├─ Statusas: PRIVALOMAS arba NEPRIVALOMAS
├─ Ryšys:
│  ├─ Priskirtas 1 temai
│  ├─ Priskirtas kelioms temoms
│  └─ Bendras pool (bet kuriai temai)
└─ Tikslai (optional):
   ├─ Tikslas 1 (koeficientas)
   ├─ Tikslas 2 (koeficientas)
   └─ ...
```


## 2. Vertės skaičiavimas

### 2.1. Savarankiško darbo "vienetai"
Savarankiško darbo vienetai = Trukmė (val) × Vertės koeficientas


**Pavyzdys:**

Rašinys:
- Trukmė: 3 valandos
- Koeficientas: 1.5
- Vienetai = 3 × 1.5 = 4.5

### 2.2. Bazinė savarankiško darbo vertė
Bazinė vertė = (Savarankiško darbo vienetai / Pamokų vienetų suma) × 100%

Kur:
- Pamokų vienetų suma = Viso vienetų (kaip apskaičiuota pamokose)

**Pavyzdys:**
- Pamokų vienetai: 239.5 (iš pamokų skaičiavimo)
- Savarankiškas darbas vienetai: 4.5
- Bazinė vertė = (4.5 / 239.5) × 100% = 1.88%

### 2.3. Jei savarankiškas darbas turi tikslus
Tikslo vertė (savarankiško darbo) =
(Tikslo koef. / Σ tikslų koef.) × Bazinė savarankiško darbo vertė


**Pavyzdys:**

Rašinys (1.88%):
- Tikslas 1: Paruošti planą (koef. 0.5)
- Tikslas 2: Parašyti tekstą (koef. 1.0)
- Tikslas 3: Pataisyti klaidas (koef. 0.5)
- Suma koef: 2.0

Rezultatai:
- Tikslas 1: (0.5 / 2.0) × 1.88% = 0.47%
- Tikslas 2: (1.0 / 2.0) × 1.88% = 0.94%
- Tikslas 3: (0.5 / 2.0) × 1.88% = 0.47%

## 3. Mokinio pažangos skaičiavimas

### 3.1. Pamokų pažanga (kaip anksčiau)
Pamokų pažanga = Σ(Pamokų tikslų pasiekta vertė)


### 3.2. Savarankiško darbo pažanga

**Jei BE tikslų:**
Savarankiško darbo pasiekta = Bazinė vertė × Completion %


**Jei SU tikslais:**
Savarankiško darbo pasiekta = Σ(Tikslo vertė × Completion %)


### 3.3. Galutinė pažanga
Galutinė pažanga = Pamokų pažanga + Savarankiško darbo pažanga


**Pavyzdys:**

Mokinys Jonas:
- Pamokos: 50%
- Savarankiškas darbas: +12%
- Galutinė: 62%

## 4. Privalomas vs Neprivalomas

### 4.1. Neprivalomas (bonusas)
Galutinė pažanga = Pamokų pažanga + Savarankiško darbo pažanga


Gali būti > 100% ✅

### 4.2. Privalomas
Kursas = Pamokos + PRIVALOMAS savarankiškas darbas = 100%


Jei neatlieka privalomo:
- Maksimali pažanga < 100%

**Skaičiavimas:**
Privalomų savarankiškų darbų vertė = X%

Pamokų dalis kurse = (100% - X%) / 100%
Savarankiško darbo dalis = X% / 100%

Galutinė pažanga =
(Pamokų pažanga × Pamokų dalis) +
(Savarankiško darbo pažanga × Savarankiško darbo dalis)


**Pavyzdys:**

Privalomas savarankiškas darbas: 20%  
Pamokos: 80%

Mokinys:
- Pamokos: 90% užbaigta
- Savarankiškas: 50% užbaigta
- Galutinė = (90% × 0.8) + (50% × 0.2) = 72% + 10% = 82%

## 5. Multi-tema savarankiškas darbas

### 5.1. Priskirtas kelioms temoms

Savarankiškas darbas paskirstomas proporcingai temų vertėms

**Pavyzdys:**

Projektas "Funkcijų tyrimas" (vertė 5%):
- Susijęs su:
  - Tema A (vertė 10%)
  - Tema B (vertė 15%)

Paskirstymas:
- Tema A dalis: 10 / (10+15) = 40%
- Tema B dalis: 15 / (10+15) = 60%

Projekto vertė:
- Tema A: 5% × 40% = 2%
- Tema B: 5% × 60% = 3%

### 5.2. Bendras pool

Vertė pridedama prie bendros pažangos, nesusiejama su konkrečia tema

**Pavyzdys:**

Mokinys:
- Pamokos: 50%
- Bendras pool savarankiškas: +8%
- Galutinė: 58%

(8% nepriskirti jokiai temai)

## 6. Produktyvumo skaičiavimas

### 6.1. Planuota pažanga (kaip anksčiau)
Planuota = (Praėjusios dienos / Kurso trukmė) × 100%


### 6.2. Pasiekta pažanga (su savarankišku darbu)
Pasiekta = Pamokų pažanga + Savarankiško darbo pažanga


### 6.3. Produktyvumas
Produktyvumas = (Pasiekta / Planuota) × 100%


**Pavyzdys:**

Po 45 dienų (planuota 25%):
- Pamokos: 20%
- Savarankiškas: +8%
- Pasiekta: 28%
- Produktyvumas = (28% / 25%) × 100% = 112%

**Pastaba:** Savarankiškas darbas padidina produktyvumą! ✅

## 7. Vizualizacija sistemoje

**Variantas B: Bendra juosta su split**
```
┌────────────────────────────────────────┐
│ JONAS PETRAITIS - Pažanga              │
├────────────────────────────────────────┤
│                                        │
│ 62% ████████████░░░░░░░░░░░░░░░         │
│     └─ 50% pamokos                     │
│     └─ +12% savarankiškas              │
│                                        │
│ Planuota: 25%                          │
│ Produktyvumas: 248% 🟣                 │
└────────────────────────────────────────┘
```

## 8. Formulių santrauka

### Savarankiško darbo vertė

1. **Vienetai**
Vienetai = Trukmė (val) × Koeficientas


2. **Bazinė vertė**
Bazinė vertė = (Vienetai / Pamokų_vienetų_suma) × 100%


3. **Tikslo vertė** (jei yra tikslų)
Tikslo vertė = (Tikslo_koef / Σ_tikslų_koef) × Bazinė_vertė


### Mokinio pažanga

4. **Savarankiško darbo pasiekta**
   - BE tikslų: `Bazinė_vertė × Completion%`
   - SU tikslais: `Σ(Tikslo_vertė × Completion%)`

5. **Galutinė pažanga**
Galutinė pažanga = Pamokų_pažanga + Savarankiško_darbo_pažanga


### Privalomas savarankiškas darbas

6. **Jei PRIVALOMAS:**
Pamokų_dalis = (100% - Privalomų_vertė) / 100%
Savarankiško_dalis = Privalomų_vertė / 100%

Galutinė = (Pamokų_pažanga × Pamokų_dalis) +
(Savarankiško_pažanga × Savarankiško_dalis)


### Multi-tema paskirstymas

7. **Temos dalis**
Temos_dalis = Temos_vertė / Σ_susijusių_temų_verčių


8. **Savarankiško darbo dalis temai**
Savarankiško_darbo_dalis_temai =
Savarankiško_darbo_vertė × Temos_dalis


### Produktyvumas

9. **Produktyvumas**
Produktyvumas =
((Pamokų_pažanga + Savarankiško_pažanga) / Planuota) × 100%


## 9. Klausimai/Pastabos

1. **Ar savarankiško darbo trukmė skaičiuojama valandoms ar pamokoms?**
   - Dabar priėmiau: valandos (nes nesusijęs su BUP pamokų sistema)

2. **Ar savarankiško darbo bazinė vertė skaičiuojama nuo pamokų vienetų sumos?**
   - Dabar priėmiau: taip (kad būtų proporcinga su pamokų sistema)
   - Alternatyva: Mentorius nustato absoliučią vertę (pvz. "Rašinys = 2%")

3. **Ar privalomi savarankiški darbai "atima" iš pamokų 100%?**
   - Dabar priėmiau: taip (pamokos tampa <100% jei yra privalomų)
   - Alternatyva: Pamokos lieka 100%, privalomi reikalingi pasiekti 100%

4. **Ar multi-tema savarankiškas darbas automatiškai paskirstomas?**
   - Dabar priėmiau: taip, proporcingai temų vertėms
   - Alternatyva: Mentorius rankiniu būdu nustato %

---
