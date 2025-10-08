# File: C:\Users\LT1A2G\Desktop\SAULIUS\curriculum_readme.md

# BACKEND APRAŠYMAS: MOKYKLOS DALYKŲ TEMŲ IR UGDYMO PLANŲ SISTEMA
# Purpose: Dokumentacija apie Temų (Topics) ir Ugdymo Planų (Curriculum Plans) backend sistemos veikimą
# Updates: 2025-10-08 - Sukurta pradinė dokumentacija
#          2025-10-08 - Papildyta Template/Snapshot logika, filtravimas, kopijavimas, reitingavimas
#          2025-10-08 - Supaprastinta versijai be kodo - skirta ne-IT skaitytojams
#          2025-10-08 - Pridėta Ugdymo Planų funkcionalumas
# Notes: Temas ir ugdymo planus kuria mentorius. Dokumentas aprašo sistemos logiką ir funkcionalumą.

---

## PAGRINDINĖ IDĖJA

### Temų sistema
Temų sistema leidžia mentoriams kurti, dalintis ir tobulinti ugdymo plano šablonus. Sistema užtikrina, kad:
- Mentorius gali sukurti temą ir ją bet kada redaguoti
- Kiti mentorai gali naudoti ir kopijuoti šias temas
- Kai tema naudojama veikloje, sukuriamas jos "užšaldytas" dublikatas
- Populiariausios temos lengvai randamos per reitingavimo sistemą

### Ugdymo planų sistema
Ugdymo planų sistema leidžia mentoriams kurti struktūrizuotus mokymosi planus. Sistema užtikrina, kad:
- To paties dalyko mentorai gali bendradarbiauti kuriant planą
- Planas gali būti pritaikytas konkrečiai mokinių grupei arba vienam mokiniui
- Planas sudarytas iš temų, sudėliotų tam tikra tvarka (seka)
- Galima naudoti bet kurio mentoriaus sukurtas temas

---

## 1. TEMPLATE & SNAPSHOT LOGIKA (ŠABLONAS IR UŽŠALDYTA KOPIJA)

### Kaip veikia temų sistema:

**TEMA (TEMPLATE/ŠABLONAS)**
- Mentorius sukuria Temą kaip šabloną
- Šablonas gali būti redaguojamas bet kada
- Šablonas naudojamas kaip pagrindas veikloms
- Vienas šablonas gali būti panaudotas keliose veiklose

**KOL VEIKLA VYKSTA (IN PROGRESS)**
- Veikla naudoja TEMPLATE (šabloną), ne snapshot'ą
- Mentorius dar gali keisti temos parametrus
- Galima koreguoti jei matoma kad reikia daugiau laiko
- Galima pritaikyti jei mokiniai sunkiai supranta
- **Lankstumas** - mentorius gali reaguoti į situaciją

**VEIKLOS UŽBAIGIMAS → SNAPSHOT SUKŪRIMAS**
- ⚠️ **SVARBU:** Snapshot sukuriamas tik UŽBAIGUS veiklą, ne pradedant!
- Kai mentorius pažymi veiklą kaip "Užbaigta", sistema sukuria snapshot'ą
- Snapshot'as yra užšaldyta kopija su tais parametrais, kurie buvo užbaigimo metu
- Snapshot'as NIEKADA nebebus keičiamas
- Kiekviena užbaigta veikla turi savo nepriklausomą snapshot'ą

**KODĖL SNAPSHOT SUKURIAMAS PABAIGOJE?**
- **Lankstumas mokymosi metu**: Mentorius gali koreguoti temą pagal poreikį
- **Reaguoti į situaciją**: Jei mokiniai nesusidoroja, galima pridėti laiko ar pakeisti kriterijus
- **Realybės atspindys**: Snapshot fiksuoja KAS TIKRAI BUVO MOKOMASI, ne kas buvo planuota
- **Istorinis vientisumas**: Užbaigus, snapshot išsaugo tikrą mokymosi patirtį
- **Mokinių apsauga**: Vertinimas pagal tai, ko buvo mokoma, ne pagal vėlesnius pakeitimus

**PAVYZDYS:**
```
Veiksmai:
1. Mentorius Jonas sukuria temą "Trigonometrija" rugsėjį
2. Rugsėjo 1d. pradeda veiklą su šia tema → naudoja TEMPLATE
3. Rugsėjo 5d. mato kad mokiniai sunkiai supranta
4. Jonas pakeičia temos kriterijus (sumažina slenkstinio lygio reikalavimus)
5. Prideda papildomų pavyzdžių į temos turinį
6. Rugsėjo 15d. užbaigia veiklą → sistema sukuria Snapshot A su GALUTINIU turiniu

7. Spalį Jonas vėl atnaujina originalų šabloną (prideda naujų tikslų)
8. Spalio 1d. pradeda naują veiklą su ta pačia tema → naudoja atnaujintą TEMPLATE
9. Spalio 15d. užbaigia veiklą → sistema sukuria Snapshot B

Rezultatas:
- Snapshot A turi tuos parametrus, kurie buvo rugsėjo PABAIGOJE (po koregavimų)
- Snapshot B turi spalio parametrus
- Snapshot A ir B yra SKIRTINGI
- Mokinių pasiekimai vertinami pagal snapshot'us (ko tikrai buvo mokoma)
```

**TEMOS PAKARTOJIMAS**
Mentorius gali pakartoti temą jei:
- Mokiniai nepasiekė tikslų pirmą kartą
- Reikia daugiau laiko išaiškinti temą
- Mentorius pervertino mokinių galimybes

```
PAKARTOJIMO SCENARIJUS:
1. Mentorius Jonas vedė "Kvadratinės lygtys" temą spalio 1-15d.
2. Užbaigus veiklą, mato kad tik 30% mokinių pasiekė bazinį lygį
3. Spalio 20d. Jonas vėl pradeda tą pačią temą "Kvadratinės lygtys"
4. Šį kartą prideda papildomų pratybų, sumažina tempą
5. Lapkričio 5d. užbaigia - dabar 80% mokinių pasiekė bazinį lygį
6. Sistema sukuria ATSKIRĄ snapshot'ą antram kartui
7. Abu kartai išsaugoti istorijoje - matoma kur sėkmingiau
```

---

## 2. TEMŲ BENDRINIMAS IR KOLABORACIJA

### Kas mato temas?

**VIEŠA TEMA (is_public = True)**
- Matoma VISIEMS mentoriams
- Bet kuris mentorius gali ją naudoti veiklose
- Bet kuris mentorius gali ją KOPIJUOTI sau

**PRIVATI TEMA (is_public = False)**
- Matoma tik savininkui (kūrėjui)
- Kiti mentorai jos nemato ir negali naudoti
- Naudojama asmeniniams juodraščiams

### Temų kopijavimas

**KAIP VEIKIA KOPIJAVIMAS?**
1. Mentorius Petras randa Jono sukurtą viešą temą "Trigonometrija"
2. Petras nusprendžia ją kopijuoti sau
3. Sistema sukuria NAUJĄ temą su visais Jono temos parametrais
4. Nauja tema priklauso Petrui (jis tampa savininku)
5. Petras gali laisvai redaguoti savo kopiją
6. Jono originali tema lieka nepakitusi

**KODĖL TAI NAUDINGA?**
- Mentorai mokosi vieni iš kitų
- Nereikia kurti visko nuo nulio
- Galima paimti gerą pagrindą ir pritaikyti savo poreikiams
- Skatina bendradarbiavimą ir kokybės kėlimą

**ISTORIJA IR SEKIMAS**
- Sistema prisimena iš kurios temos buvo sukurta kopija (copied_from laukas)
- Galima sekti temos "genealogiją"
- Galima suprasti kurios temos yra populiariausios (daugiausiai kopijuojamos)

---

## 3. REITINGAVIMO SISTEMA

### Kodėl reitinguojamos temos?

Reitingavimas padeda mentoriams rasti geriausias, populiariausias ir labiausiai išbandytas temas.

### Kaip matuojama temos populiarumas?

**PANAUDOJIMŲ SKAIČIUS (usage_count)**
- Kiek kartų tema buvo panaudota veiklose
- Kiekvieną kartą priskiriant temą veiklai, skaičius didėja
- Dažnai naudojamos temos yra patikrintos praktikoje

**ĮVERTINIMAI (average_rating)**
- Mentorai gali įvertinti temą nuo 1.0 iki 5.0 žvaigždučių
- Skaičiuojamas vidutinis įvertinimas iš visų gautų įvertinimų
- Aukštas įvertinimas rodo temos kokybę

**POPULIARUMO BALAS**
- Sistema skaičiuoja bendrą populiarumo balą derinant:
  - 70% - reitingas (kokybė)
  - 30% - panaudojimų skaičius (praktinis patikrinimas)
- Temos pagal nutylėjimą rodomos nuo populiariausių

**PAVYZDYS:**
```
Tema "Trigonometrija A":
- Panaudota 50 kartų veiklose
- Vidutinis įvertinimas: 4.8/5.0
- Populiarumo balas: (4.8 × 0.7) + (5.0 × 0.3) = 4.86

Tema "Trigonometrija B":
- Panaudota 5 kartus veiklose
- Vidutinis įvertinimas: 5.0/5.0
- Populiarumo balas: (5.0 × 0.7) + (1.5 × 0.3) = 3.95

Rezultatas: Tema A bus aukščiau sąraše, nes yra daugiau patikrinta praktikoje.
```

---

## 4. FILTRAVIMO IR PAIEŠKOS GALIMYBĖS

### Pagal ką galima filtruoti temas?

**DALYKAS (Subject)**
- Rodyti tik konkrečiam dalykui skirtas temas
- Pvz: "Rodyti tik matematikos temas"

**KŪRĖJAS (Mentor)**
- Rodyti tik konkretaus mentoriaus sukurtas temas
- Pvz: "Rodyti tik Jono sukurtas temas"

**MOKYMO LYGIAI (Levels)**
- Rodyti temas skirtas konkretiems lygiams
- Pvz: "Rodyti tik pradedančiųjų lygio temas"

**VIEŠUMAS (is_public)**
- Rodyti tik viešas arba tik privačias temas
- Pvz: "Rodyti tik viešas temas"

**BŪSENA (is_deleted)**
- Rodyti aktyvias arba ištrintas temas
- Administratoriams - galimybė atkurti ištrintas temas

### Paieška

**TEKSTO PAIEŠKA**
Galima ieškoti temų pagal:
- Pavadinimą
- Turinį (mokomąją medžiagą)
- Temos žymę/kategoriją

**PAVYZDYS:**
Įvedus "trigonometrija" sistema ras visas temas, kur šis žodis figūruoja pavadinime ar turinyje.

### Rikiavimas

**RIKIAVIMO KRITERIJAI:**
- Pagal reitingą (nuo geriausių)
- Pagal panaudojimų skaičių (nuo populiariausių)
- Pagal sukūrimo datą (nuo naujausių/seniausių)
- Pagal atnaujinimo datą
- Pagal pavadinimą (abėcėlės tvarka)

**PAGAL NUTYLĖJIMĄ:**
Temos rodomos nuo populiariausių (reitingas + panaudojimai)

---

## 5. TEMOS STRUKTŪRA IR PARAMETRAI

Kiekviena tema turi šiuos parametrus (analogiški Lesson modeliui):

### Pagrindinė informacija
- **Pavadinimas** - temos pavadinimas
- **Dalykas** - kuriam dalykui priskirta (matematika, lietuvių k. ir kt.)
- **Tema/Kategorija** - temos žymė ar kategorija
- **Mentorius** - kas sukūrė temą
- **Mokomoji medžiaga** - temos turinys, aprašymas

### Mokymo parametrai
- **Mokymo lygiai** - kuriems lygiams tinkama (pradedantis, vidutinis, pažengęs)
- **Gebėjimai** - kokie gebėjimai ugdomi
- **Dorybės** - kokios dorybės ugdomos
- **BUP Kompetencijos** - bendrosios ugdymo programos kompetencijos

### Mokymosi tikslai
- **Tikslai** - ką mokinys turėtų pasiekti
- **Komponentai** - iš kokių dalių susideda tema
- **Fokusas veiksmai** - pagrindiniai veiksmai/veiklos

### Pasiekimo lygiai su procentais
- **Slenkstinis lygis (54%)** - minimalūs reikalavimai
- **Bazinis lygis (74%)** - vidutiniai reikalavimai
- **Pagrindinis lygis (84%)** - geri reikalavimai
- **Aukštesnysis lygis (100%)** - puikūs reikalavimai

### Statistika ir valdymas
- **Panaudojimų skaičius** - kiek kartų panaudota veiklose
- **Vidutinis įvertinimas** - kokį reitingą turi
- **Įvertinimų skaičius** - kiek kartų buvo įvertinta
- **Kopijuota iš** - jei tai kopija, iš kurios temos
- **Viešumas** - ar matoma kitiems mentoriams
- **Sukūrimo data** - kada sukurta
- **Atnaujinimo data** - kada paskutinį kartą redaguota

---

## 6. GALIMI VEIKSMAI SU TEMOMIS IR TEISIŲ VALDYMAS

### Mentorius gali:

**KURTI NAUJĄ TEMĄ**
- Užpildyti visus temos parametrus
- Pasirinkti ar tema bus vieša ar privati
- Tema automatiškai priskiriama kūrėjui

**REDAGUOTI TIK SAVO SUKURTAS TEMAS**
- ⚠️ **SVARBU:** Mentorius gali redaguoti TIK savo sukurtas temas
- Keisti bet kurį savo temos parametrą
- Atnaujinimas nepaveikia jau sukurtų veiklų (snapshots)
- Sistema išsaugo atnaujinimo datą
- **NEGALIMA** redaguoti kitų mentorių temų tiesiogiai

**PERŽIŪRĖTI KITŲ MENTORIŲ TEMAS**
- Gali matyti visas viešas temas
- Gali skaityti visą turinį
- Gali naudoti veiklose
- **BET NEGALI REDAGUOTI**

**KOPIJUOTI KITŲ MENTORIŲ TEMAS**
- Bet kuris mentorius gali kopijuoti viešą temą
- Sukuriama **NAUJA** tema priklausanti kopijuotojui
- Galima pakeisti pavadinimą
- ✅ **TADA GALIMA** laisvai redaguoti kopiją (nes tai jau JŪSŲ tema)
- Kopija tampa visiškai nepriklausoma nuo originalo

**NAUDOJIMO SCENARIJUS:**
```
Situacija: 
Jonas nori naudoti Petro temą "Kvadratinės lygtys", bet nori ją šiek tiek pritaikyti.

KĄ JONAS NEGALI DARYTI:
❌ Tiesiogiai redaguoti Petro temos
❌ Keisti Petro temos turinį
❌ Trinti Petro temą

KĄ JONAS GALI DARYTI:
✅ Peržiūrėti Petro temą
✅ Naudoti Petro temą veikloje (kaip yra)
✅ Kopijuoti Petro temą sau
✅ Redaguoti SAVO KOPIJĄ kaip nori
✅ Pervadinti savo kopiją (pvz., "Kvadratinės lygtys - papildyta")

VEIKSMAI:
1. Jonas randa Petro temą "Kvadratinės lygtys"
2. Jonas spaudžia "Kopijuoti temą"
3. Sistema sukuria naują temą savininkė Jonas
4. Jonas pervadina: "Kvadratinės lygtys - su papildomomis užduotimis"
5. Jonas redaguoja SAVO kopiją:
   - Prideda papildomų pavyzdžių
   - Pakeičia vertinimo kriterijus
   - Pritaiko savo stilių
6. Jonas išsaugo - dabar tai JO tema
7. Petro originali tema lieka nepakitusi
```

**IŠTRINTI SAVO TEMĄ**
- "Švelnusis trynimas" (soft delete) - tema nėra galutinai ištrinama
- Tema tik pažymima kaip ištrinta (is_deleted = true)
- Išsaugo visą istoriją ir ryšius
- Galima atkurti bet kada
- **GALIMA IŠTRINTI** tik savo sukurtas temas

**ATKURTI IŠTRINTĄ TEMĄ**
- Pašalina ištrynimo žymę savo temoje
- Tema vėl tampa aktyvi
- Galima atkurti tik savo ištrintas temas

**ĮVERTINTI TEMĄ**
- Duoti įvertinimą nuo 1.0 iki 5.0
- Padeda kitiems mentoriams rasti kokybiškas temas

**NAUDOTI TEMĄ VEIKLOJE**
- Priskiriant temą veiklai, sukuriamas snapshot
- Snapshot'as yra užšaldytas ir nebekeičiamas
- Tema automatiškai gauna +1 panaudojimą

### Administratorius papildomai gali:

**MATYTI VISAS TEMAS**
- Įskaitant privačias
- Įskaitant ištrintas

**REDAGUOTI BET KURIOS TEMOS**
- Taisyti klaidas
- Moderuoti turinį

**GALUTINAI IŠTRINTI TEMĄ**
- "Kietusis trynimas" (hard delete)
- Tema ištinama visiškai iš sistemos
- **ATSARGIAI!** Ištrina visus susijusius duomenis

---

## 7. SISTEMŲ SĄVEIKA

### Kaip Temos sąveikauja su kitais sistemos komponentais?

**SU VEIKLOMIS (Activities)**
- Veikla gali turėti vieną ar daugiau temų
- Priskiriant temą, sukuriamas snapshot
- Snapshot'as lieka priskirtas tai veiklai visam laikui

**SU MOKINIAIS**
- Mokiniai dirba su veiklos snapshot'u, ne su originalia tema
- Mokinių pasiekimai vertinami pagal snapshot'o kriterijus
- Jei tema pakeičiama, tai nepaveikia jau dirbančių mokinių

**SU DALYKAIS (Subjects)**
- Kiekviena tema priskirta vienam dalykui
- Galima filtruoti temas pagal dalyką
- Dalykų struktūra padeda organizuoti temas

**SU LYGIAIS (Levels)**
- Tema gali būti priskirta keliems lygiams
- Padeda rasti tinkamo sudėtingumo temas
- Leidžia diferencijuoti mokymą

**SU GEBĖJIMAIS IR DORYBĖMIS**
- Tema gali ugdyti kelis gebėjimus ir dorybę
- Padeda sekti holistinį ugdymą
- Leidžia analizuoti kokius gebėjimus dažniausiai ugdome

---

## 8. DUOMENŲ SAUGUMAS IR ISTORIJA

### Soft Delete (Švelnusis trynimas)

**KAS TAI?**
Kai mentorius "ištrina" temą, ji iš tiesų nėra ištrinama iš duomenų bazės.

**KAIP VEIKIA?**
1. Tema pažymima kaip ištrinta (is_deleted = true)
2. Išsaugoma trynimo data (deleted_at)
3. Tema dingsta iš įprastų sąrašų
4. Bet lieka duomenų bazėje
5. Galima bet kada atkurti

**KODĖL TAIP?**
- **Apsauga nuo klaidų** - galima atkurti jei ištrinome per klaidą
- **Istorija** - išsaugome veiklų ir mokinių duomenų vientisumą
- **Auditas** - galime sekti kas ir kada buvo ištrinta
- **Snapshot'ų apsauga** - snapshot'ai gali turėti nuorodas į originalią temą

### Hard Delete (Kietusis trynimas)

**KAS TAI?**
Visiškas ir negrįžtamas temos ištrynimas iš sistemos.

**KAS GALI?**
Tik administratoriai.

**KADA NAUDOTI?**
- Klaidingi dublikatai
- Netinkamas turinys
- Testavimo duomenys
- **ATSARGIAI!** Veiksmas negrįžtamas.

### Duomenų vientisumas

**SNAPSHOT'Ų NEPRIKLAUSOMYBĖ**
- Snapshot'ai yra visiškai nepriklausomi nuo originalios temos
- Jei ištrinama originali tema (soft delete), snapshot'ai lieka
- Snapshot'ai saugo savo duomenis

**NUORODOS**
- Sistema prisimena ryšius tarp objektų
- Kopijos turi nuorodą į originalą (copied_from)
- Snapshot'ai turi nuorodą į originalią temą (original_topic)
- Tai leidžia sekti istoriją ir genealogiją

---

## 9. PRAKTINIAI NAUDOJIMO SCENARIJAI

### Scenarija 1: Mentorius kuria naują temą

```
1. Jonas prisijungia prie sistemos kaip mentorius
2. Eina į "Temos" skiltį
3. Spaudžia "Sukurti naują temą"
4. Užpildo:
   - Pavadinimas: "Kvadratinės lygtys"
   - Dalykas: Matematika
   - Turinys: [aprašo mokomąją medžiagą]
   - Tikslai: [išdėsto mokymosi tikslus]
   - Pasiekimo lygiai: [nustato kriterijus]
5. Pasirenka "Vieša tema" - kad kiti mentorai galėtų naudoti
6. Išsaugo
7. Tema atsiranda jo temų sąraše ir viešų temų sąraše
```

### Scenarija 2: Mentorius naudoja kitų sukurtą temą

```
1. Petras ieško temos matematikos dalykui
2. Filtruoja: Dalykas = Matematika
3. Rikiuoja pagal reitingą
4. Randa Jono sukurtą "Kvadratinės lygtys" (reitingas 4.8/5.0)
5. Peržiūri temos turinį
6. Spaudžia "Naudoti veikloje"
7. Sistema sukuria snapshot ir priskiria Petro veiklai
8. Jono temos panaudojimų skaičius +1
9. Petras gali įvertinti temą
```

### Scenarija 3: Mentorius kopijuoja ir tobulina temą

```
1. Ona randa Jono "Kvadratinės lygtys" temą
2. Nori ją naudoti, bet šiek tiek pritaikyti savo stiliui
3. Spaudžia "Kopijuoti temą"
4. Įveda naują pavadinimą: "Kvadratinės lygtys - papildyta versija"
5. Sistema sukuria naują temą priklausančią Onai
6. Ona redaguoja savo kopiją:
   - Prideda papildomų užduočių
   - Pakeičia kai kuriuos pavyzdžius
   - Pritaiko savo mokymo stilių
7. Išsaugo
8. Dabar Ona turi savo temą, kurią gali laisvai naudoti
9. Jono originali tema lieka nepakitusi
```

### Scenarija 4: Tema tobulinama nepažeidžiant esamų veiklų

```
1. Jonas sukūrė "Trigonometrija" temą rugsėjį
2. Priskirta rugsėjo veiklai → sukurtas Snapshot R
3. Mokiniai pradėjo mokytis pagal Snapshot R
4. Spalį Jonas nusprendė patobulinti temą:
   - Pridėti naujų pavyzdžių
   - Pakeisti vertinimo kriterijus
   - Patikslinti tikslus
5. Jonas redaguoja originalią temą ir išsaugo
6. Rugsėjo veikloje mokiniai TOLIAU mokosi pagal senus reikalavimus (Snapshot R)
7. Spalio veikloje Jonas priskiria patobulintą temą → sukurtas Snapshot S
8. Spalio mokiniai mokosi pagal naujus reikalavimus (Snapshot S)
9. Rugsėjo mokiniai nepatyrė jokių pakeitimų - teisingumas išlaikytas!
```

---

## 10. API ENDPOINT'AI (FUNKCIJŲ SĄRAŠAS)

Sistema teikia šias funkcijas per API:

### Temų peržiūra ir paieška
- **Visų temų sąrašas** - su filtravimu ir rikiаvimu
- **Vienos temos detalus vaizdas** - pilna informacija
- **Mano sukurtos temos** - tik prisijungusio mentoriaus temos
- **Viešos temos** - visos viešai prieinamos temos
- **Temos pagal dalyką** - filtruojama pagal subject
- **Temos pagal mentorių** - konkretaus mentoriaus viešos temos
- **Populiariausios temos** - rikiuota pagal reitingą

### Temų valdymas
- **Sukurti naują temą** - mentorius sukuria temą
- **Redaguoti temą** - savininkas redaguoja
- **Ištrinti temą** - soft delete
- **Atkurti temą** - atšaukti ištrynimą
- **Galutinai ištrinti** - tik administratoriams

### Temų naudojimas
- **Kopijuoti temą** - sukurti kopiją sau
- **Įvertinti temą** - duoti reitingą
- **Naudoti veikloje** - sukurti snapshot (vyksta veiklos sistemoje)

---

## 11. SISTEMOS PRANAŠUMAI

### Mentoriams

**LAIKO TAUPYMAS**
- Nereikia kurti visko nuo nulio
- Galima naudoti ir tobulinti kitų darbus
- Greitas prieigos prie kokybiško turinio

**KOKYBĖS UŽTIKRINIMAS**
- Reitingų sistema padeda rasti geriausius pavyzdžius
- Dažnai naudojamos temos yra patikrintos praktikoje
- Galima mokytis iš sėkmingų pavyzdžių

**LANKSTUMAS**
- Galima redaguoti temas neveikiant esamų veiklų
- Vienas šablonas daugeliui veiklų
- Privatumo kontrolė (viešos/privačios temos)

### Mokiniams

**STABILUMAS**
- Reikalavimai nepasikeis mokymosi metu
- Vertinimas pagal aiškius ir pastovius kriterijus
- Nėra neteisingumo dėl pasikeitusių reikalavimų

**KOKYBĖ**
- Mokosi pagal išbandytas ir įvertintas temas
- Mentorai naudoja geriausius šablonus

### Administracijai

**AUDITAS**
- Visa istorija išsaugoma
- Galima sekti kas, ką ir kada keitė
- Snapshot'ai saugo kas konkrečiai buvo reikalaujama

**KONTROLĖ**
- Galimybė moderuoti turinį
- Atkurti ištrintus duomenis
- Pilna sistemos apžvalga

**KOKYBĖS MATAVIMAS**
- Reitingai rodo kokios temos sėkmingos
- Panaudojimų statistika rodo populiarumą
- Galima identifikuoti geriausias praktikas

---

## 12. UGDYMO PLANAI (CURRICULUM PLANS)

### Kas yra ugdymo planas?

**UGDYMO PLANAS** - tai struktūrizuotas mokymosi kelias, sudarytas iš temų sekos, pritaikytas konkretiems mokiniams ar mokinių grupei.

**PAGRINDINIS PRINCIPAS:**
Ugdymo planas = Temų seka + Tvarka + Konkretus mokinys/grupė

### Ugdymo plano struktūra

**PLANO KOMPONENTAI:**
1. **Pavadinimas** - plano aprašomasis pavadinimas
2. **Dalykas** - kuriam dalykui skirtas (matematika, lietuvių k., kt.)
3. **Mokinys/Grupė** - kam skirtas planas
4. **Mentorius/Mentorius** - kas sukūrė ir dalyvauja plane
5. **Temų seka** - sudėliotos temos tam tikra tvarka (1, 2, 3...)
6. **Laikotarpis** - kada planuojama vykdyti

### Bendradarbiavimas tarp mentorių

**BENDRAS PLANO KŪRIMAS**

To paties dalyko mentorai gali kartu kurti ugdymo planą:

**PAVYZDYS:**
```
Matematikos dalykas:
- Mentorius Jonas (algebros specialistas)
- Mentorė Ona (geometrijos specialistė)
- Mentorius Petras (analizės specialistas)

Visi trys kuria bendrą matematikos ugdymo planą 10-tai klasei:
- Jonas prideda savo algebros temas
- Ona prideda savo geometrijos temas
- Petras prideda analizės temas
- Visi kartu sudėlioja seką ir tvarką
```

**BENDRADARBIAVIMO PRIVALUMAI:**
- Kiekvienas mentorius prisideda savo srities temomis
- Galima sudaryti išsamesnį ir visapusiškesnį planą
- Mentorai papildo vienas kito kompetencijas
- Mokiniai gauna kompleksinį ugdymą

### Temų šaltiniai plane

**GALIMA NAUDOTI BET KURIO MENTORIAUS TEMAS**

Kuriant ugdymo planą, galima naudoti:
- ✅ Savo sukurtas temas
- ✅ Kitų to paties dalyko mentorių temas
- ✅ Kitų dalykų mentorių temas (jei tinka)
- ✅ Bet kurias viešas temas sistemoje

**PAVYZDYS:**
```
Mentorius Jonas kuria matematikos planą ir naudoja:
1. Savo temą "Kvadratinės lygtys"
2. Onos temą "Trikampiai" (iš geometrijos)
3. Petro temą "Funkcijos" (iš analizės)
4. Marijos temą "Procentai" (kitos mentorius)

Rezultatas: Išsamus planas iš geriausių temų
```

### Individualizavimas

**PLANAS KONKRETIEMS MOKINIAMS**

Ugdymo planas gali būti pritaikytas:

**1. MOKINIŲ GRUPEI**
- Klasei
- Mokymosi lygio grupei
- Projektinei grupei
- Interesų grupei

**PAVYZDYS:**
```
"10A klasės matematikos ugdymo planas 2024/2025"
- Skirtas 10A klasės mokiniams
- 20 temų per metus
- Sudėliotos nuo paprastesnių prie sudėtingesnių
```

**2. VIENAM MOKINIUI**
- Individualus mokymosi planas
- Pritaikytas mokinio lygiui
- Atsižvelgia į stipriąsias/silpnąsias puses
- Leidžia mokytis savo tempu

**PAVYZDYS:**
```
"Jono individualus matematikos planas"
- Skirtas konkrečiam mokiniui Jonui
- Praleistos bazinės temos (jis jau moka)
- Pridėtos pažangios temos (jo stiprybė)
- Papildomos pratybos silpnose temose
```

### Temų seka ir tvarka

**LOGINIS SUDĖLIOJIMAS**

Ugdymo plane temos sudėliotos tam tikra seka (tvarka):

**SEKA GALI BŪTI NUSTATYTA PAGAL:**
- **Sunkumą** - nuo paprastesnių prie sudėtingesnių
- **Priklausomybę** - vėlesnės temos reikalauja ankstesnių žinių
- **Laikotarpį** - rudens, žiemos, pavasario temos
- **Teminius blokus** - visos algebros temos, tada visos geometrijos
- **Projektus** - temos grupuojamos aplink projektus

**PAVYZDYS:**
```
Matematikos ugdymo planas - Temų seka:

1. TEMA: "Skaičių sistemos" (savaite 1-2)
   → Bazė vėlesnėms temoms

2. TEMA: "Tiesinės lygtys" (savaite 3-4)
   → Reikalauja 1 temos žinių

3. TEMA: "Kvadratinės lygtys" (savaite 5-7)
   → Reikalauja 1-2 temų žinių

4. TEMA: "Funkcijos" (savaite 8-10)
   → Reikalauja 1-3 temų žinių

Ir taip toliau...
```

### Plano kūrimo procesas

**ŽINGSNIS PO ŽINGSNIO:**

**1. PLANO SUKŪRIMAS**
```
Mentorius:
1. Eina į "Ugdymo planai" skiltį
2. Spaudžia "Sukurti naują planą"
3. Užpildo:
   - Pavadinimas: "10A klasės matematika 2024/2025"
   - Dalykas: Matematika
   - Grupė: 10A klasė
   - Laikotarpis: 2024-09-01 iki 2025-06-30
4. Išsaugo planą
```

**2. TEMŲ PRIDĖJIMAS**
```
Mentorius:
1. Atidaro sukurtą planą
2. Spaudžia "Pridėti temą"
3. Pasirenka temą iš sąrašo:
   - Gali filtruoti pagal dalyką
   - Gali ieškoti pagal pavadinimą
   - Mato visų mentorių viešas temas
4. Nustato temos poziciją sekoje (pvz., 1, 2, 3...)
5. Gali nurodyti trukmę (pvz., 2 savaitės)
6. Išsaugo
```

**3. SEKOS REDAGAVIMAS**
```
Mentorius gali:
- Keisti temų tvarką (perkelti aukštyn/žemyn)
- Ištrinti temas iš plano
- Pridėti naujas temas tarp esamų
- Keisti kiekvienos temos trukmę
```

**4. BENDRADARBIAVIMAS**
```
Jei dalyvauja keli mentorai:
1. Pagrindinis mentorius pakviečia kitus mentoriau
2. Pakviesti mentorai gali pridėti savo temas
3. Visi mato visą planą
4. Gali tartis ir keisti seką
5. Sistema saugo kas ką pridėjo/pakeitė
```

### Plano naudojimas

**PRIEŠ PAMOKĄ: PLANO ATIDARYMAS IR TEMŲ PASIRINKIMAS**

**LANKSTUMAS PASKUTINĘ MINUTĘ:**
```
Scenarijus:
1. Mentorius Jonas ateina į pamoką
2. Atidaro ugdymo planą "10A klasė - Matematika"
3. Plane matoma seka:
   ✅ Tema 1: "Skaičių sistemos" (jau pravestas)
   ✅ Tema 2: "Tiesinės lygtys" (jau pravestas)
   → Tema 3: "Kvadratinės lygtys" (sekanti pagal planą)
   → Tema 4: "Nelygybės"
   → Tema 5: "Funkcijos"

4. PASKUTINĘ MINUTĘ Jonas nusprendžia:
   "Mokiniai dar neparuošę kvadratinėms lygtis, geriau pirmiau pamokysiu nelygybių"

5. Jonas SUKEIČIA VIETOMIS:
   → Tema 3: "Nelygybės" (dabar eina trečia)
   → Tema 4: "Kvadratinės lygtys" (nukelta į ketvirtą)
   
6. Sistema AKIMIRKSNIU pakoreguoja planą
7. Jonas pradeda pamoką su "Nelygybės" tema
```

**ĮVYKDYTŲ TEMŲ UŽFIKAVIMAS:**
- Ugdymo planas automatiškai fiksuoja jau įvykdytas temas
- Jau pravestos temos pažymėtos ✅ ir NEGALIMA jų sukeisti vietomis
- Sistema neleidžia keisti jau užbaigtų temų sekos
- **KODĖL?** Išsaugoma logiška mokymosi istorija

**TEMŲ PAKARTOJIMAS PLANE:**
Mentorius gali pakartoti temą net jei ji jau buvo pravesta:

```
Pakartojimo scenarijus:
1. Planas rodo:
   ✅ Tema 3: "Kvadratinės lygtys" (pravesta, 40% mokinių nepasiekė tikslų)
   → Tema 4: "Nelygybės" (sekanti)

2. Mentorius mato kad reikia pakartoti "Kvadratinės lygtys"
3. Sistema leidžia pridėti temą į planą DAR KARTĄ:
   ✅ Tema 3: "Kvadratinės lygtys" (1-as kartas - nepakankama)
   → Tema 3.1: "Kvadratinės lygtys" (2-as kartas - pakartojimas)
   → Tema 4: "Nelygybės"

4. Mentorius veda temą antrą kartą su papildomomis prityrimis
5. Šįkart mokiniai pasiekia gerus rezultatus
6. Abi temos versijos išsaugotos plane su rezultatais
```

**SNAPSHOT'AI TEMOMS**
⚠️ **SVARBU:** Snapshot'as sukuriamas tik UŽBAIGUS veiklą!

**KOL VEIKLA VYKSTA (IN PROGRESS):**
- Naudojamas TEMPLATE (šablonas), ne snapshot'as
- Mentorius gali keisti temos parametrus mokymosi metu
- Gali koreguoti kriterijus jei matoma kad reikia
- Gali pridėti papildomų užduočių ar pavyzdžių
- **LANKSTUMAS** - reagavimas į realią situaciją

**UŽBAIGUS VEIKLĄ:**
- Sistema sukuria snapshot'ą su GALUTINIU turiniu
- Snapshot'as užšaldomas ir nebekeičiamas
- Mokinių pasiekimai vertinami pagal snapshot'ą
- Išsaugoma tikra mokymosi patirtis

```
Pavyzdys:
1. Planas turi temą "Trigonometrija"
2. Mentorius pradeda veiklą → naudoja template
3. Pamokų metu mato kad reikia papildomo laiko
4. Pakeičia temos kriterijus (sumažina reikalavimus)
5. Prideda papildomų pratybų
6. Užbaigia veiklą → sistema sukuria snapshot su GALUTINIAIS parametrais
7. Jei vėliau originalus šablonas keičiamas, snapshot lieka nepakitęs
```

### Plano pritaikymas

**LANKSTUMAS IR PRITAIKYMAS**

**PLANO KOPIJAVIMAS**
- Galima nukopijuoti esamą planą
- Pritaikyti kitai grupei/mokiniui
- Pakeisti temų seką ar turinį

**PAVYZDYS:**
```
Scenarijus:
1. Jonas sukūrė planą "10A klasė - matematika"
2. Ona nori panašų planą 10B klasei
3. Ona kopijuoja Jono planą
4. Pervadina į "10B klasė - matematika"
5. Pritaiko temų seką 10B klasės lygiui:
   - Pašalina per sudėtingas temas
   - Prideda papildomų bazinių temų
   - Pakeičia tvarką
6. Rezultatas: Pritaikytas planas 10B klasei
```

**PLANO ATNAUJINIMAS**
- Planas gali būti redaguojamas mokymosi metu
- Galima pridėti papildomų temų
- Galima pakeisti seką jei reikia
- Tačiau jau pradėtos temos (su snapshot'ais) lieka nepakeistos

### Plano stebėsena

**KĄ GALIMA SEKTI:**

**PROGRESĄ**
- Kurios temos jau įvykdytos
- Kurios temos vykdomos dabar
- Kurios temos laukia ateityje
- Kiek laiko užtruko kiekviena tema

**REZULTATUS**
- Mokinių pasiekimus kiekvienoje temoje
- Bendrus rezultatus pagal planą
- Problemines temas (kur mokiniai sunkiai sekasi)
- Sėkmingas temas (kur mokiniai puikiai sekasi)

**STATISTIKĄ**
- Kiek temų plane
- Kiek skirtingų mentorių temos naudojamos
- Bendra plano trukmė
- Plano įvykdymo procentas

### Plano pranašumai

**MOKINIAMS:**
- ✅ Aiškus mokymosi kelias
- ✅ Suprantama tvarka ir seka
- ✅ Nuoseklus žinių kaupimas
- ✅ Pritaikymas individualiam lygiui

**MENTORIAMS:**
- ✅ Struktūrizuotas mokymas
- ✅ Lengva planuoti ir organizuoti
- ✅ Galimybė bendradarbiauti
- ✅ Pakartotinis planų naudojimas
- ✅ Geriausių temų panaudojimas

**ADMINISTRACIJAI:**
- ✅ Aiški ugdymo strategija
- ✅ Sekamas progresas
- ✅ Matoma kokybė (kokie planai naudojami)
- ✅ Bendradarbiavimo skatinimas

### Praktinis pavyzdys

**PILNAS SCENARIJUS:**

```
SITUACIJA:
10-oje klasėje mokosi mokiniai skirtingų lygių. Matematikos mentorius Jonas nusprendžia sukurti 
individualizuotus ugdymo planus.

VEIKSMAI:

1. SUKURIA PAGRINDĄ PLANĄ:
   Pavadinimas: "10 klasė - Matematika - Bazinis lygis"
   Dalykas: Matematika
   Grupė: 10A klasės bazinio lygio mokiniai (12 mokinių)

2. PRIDEDA TEMAS IŠ SKIRTINGŲ ŠALTINIŲ:
   - Tema 1: "Skaičių sistemos" (savo tema)
   - Tema 2: "Algebrinės išraiškos" (Onos tema - ji gerai paaiškina)
   - Tema 3: "Tiesinės lygtys" (Petro tema - populiariausia, 4.9 reitingas)
   - Tema 4: "Nelygybės" (savo tema)
   - ... ir taip toliau 20 temų

3. NUSTATO SEKĄ:
   Sudėlioja nuo paprasto prie sudėtingo
   Kiekviena tema 2-3 savaitės

4. PAKVIEČIA BENDRADARBIAUTI:
   Pakviečia Oną padėti su geometrijos temomis
   Ona prideda 5 geometrijos temas ir sudėlioja jas sekoje

5. KOPIJUOJA PAŽANGIAM LYGIUI:
   Kopijuoja planą
   Pervadina: "10 klasė - Matematika - Pažengęs lygis"
   Pritaiko pažengusiems mokiniams (5 mokiniai):
   - Pašalina bazines temas (jau moka)
   - Prideda pažangias temas
   - Sutrumpina trukmę (mokosi greičiau)

6. KURIA INDIVIDUALŲ PLANĄ:
   Mokinys Tomas turi sunkumų su algebra
   Sukuria: "Tomo individualus planas"
   Prideda papildomų algebros temų
   Sumažina geometrijos temų (gerai sekasi)
   Tomas mokosi savo tempu

REZULTATAS:
- 12 mokinių mokosi pagal bazinį planą
- 5 mokiniai mokosi pagal pažengusių planą
- Tomas mokosi pagal individualų planą
- Visi gauna optimalų ugdymą savo lygiui
```

---

## 13. SANTRAUKA

### Pagrindinės sistemos savybės:

✅ **Template/Snapshot architektūra** - šablonai ir užšaldytos kopijos
✅ **Temų bendrinimas** - visi mentorai mato viešas temas
✅ **Kopijavimo galimybė** - kopijuoti ir tobulinti kitų temas
✅ **Reitingavimas** - rasti geriausias temas pagal įvertinimus
✅ **Filtravimas** - paieška pagal dalyką, kūrėją, lygius
✅ **Istorijos saugojimas** - soft delete, pilnas auditas
✅ **Duomenų vientisumas** - snapshot'ai nepriklausomi nuo originalų
✅ **Statistika** - panaudojimai, reitingai, populiarumas
✅ **Teisių valdymas** - kas gali kurti, redaguoti, matyti
✅ **Lankstumas** - viešos/privačios temos, redagavimas

### Pagrindiniai vartotojų veiksmai:

**Mentorius gali:**
- ✅ Kurti naujas temas
- ✅ Redaguoti **TIK SAVO** sukurtas temas
- ✅ Peržiūrėti visas viešas temas
- ✅ Naudoti bet kurio mentoriaus temas veiklose
- ✅ Kopijuoti kitų mentorių temas sau
- ✅ Redaguoti savo kopijas kaip nori
- ✅ Įvertinti kitų mentorių temas
- ✅ Ištrinti ir atkurti **TIK SAVO** temas
- ✅ Kurti ugdymo planus su bet kurių mentorių temomis
- ✅ Bendradarbiauti su to paties dalyko mentoriais

**Mentorius NEGALI:**
- ❌ Redaguoti kitų mentorių temų tiesiogiai
- ❌ Ištrinti kitų mentorių temų
- ❌ Keisti kitų mentorių temų turinio

**SPRENDIMAS:** Jei nori tobulinti kito mentoriaus temą → nukopijuoti sau ir redaguoti kopiją!

**Sistema automatiškai:**
- Sukuria snapshot'us naudojant temą veikloje
- Skaičiuoja reitingus ir populiarumą
- Apsaugo mokinių duomenis nuo pakeitimų
- Išsaugo visą istoriją
- Stebi kas, ką ir kada sukūrė/pakeitė

### Galutinis rezultatas:

Sistema, kuri skatina:
- 🤝 **Bendradarbiavimą** tarp mentorių
- 📈 **Kokybės kėlimą** per reitingus ir dalijimąsi
- ⏱️ **Efektyvumą** per pakartotinį naudojimą
- ⚖️ **Teisingumą** per nepakeičiamus snapshot'us
- 📊 **Skaidrumą** per pilną auditą ir istoriją
