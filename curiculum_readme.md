# Kurikulumo aprašas (README)

Trumpa šio dokumento apžvalga: čia pateikiami kurso tikslai, auditorija, reikalavimai, programos struktūra, tvarkaraštis, vertinimas, naudojami įrankiai ir gairės, kaip prisidėti prie turinio tobulinimo.

## Tikslai
- Aiškiai apibrėžti mokymosi tikslus ir laukiamus rezultatus
- Nurodyti kurso turinio struktūrą ir moduliais suskirstytas temas
- Aprašyti vertinimo tvarką ir kriterijus
- Pateikti rekomenduojamą tvarkaraštį ir medžiagas

## Tikslinė auditorija
- Pradedantieji ir/ar pažengę dalyviai, norintys sistemingai įsisavinti temas
- Dalyviai, turintys bazines kompiuterinio raštingumo žinias

## Reikalavimai (priešreikalavimai)
- Bazinės žinios: terminalo naudojimas, teksto redagavimas, versijavimas (nebūtina, bet rekomenduojama)
- Techniniai reikalavimai: kompiuteris su modernia naršykle ir stabilus interneto ryšys
- (Pasirinktinai) Įdiegtos įrankių grandinės, nurodytos žemiau esančiame skyriuje „Įrankiai ir aplinka“

## Programos struktūra
Žemiau pateikiama siūloma modulių struktūra. Prireikus, koreguokite modulių skaičių, temas ir trukmę.

| Modulis | Pagrindinės temos | Trukmė | Mokymosi rezultatai |
|---|---|---|---|
| 1. Įvadas | Kurso apžvalga, aplinkos paruošimas | 2–4 val. | Supranta kurso tikslus, geba paruošti darbo aplinką |
| 2. Pagrindai | Esminės sąvokos ir terminai | 4–6 val. | Įsisavina pagrindines sąvokas ir darbo eigą |
| 3. Praktika | Praktiniai pratimai ir mini-užduotys | 6–8 val. | Taiso klaidas, taiko žinias sprendžiant užduotis |
| 4. Projektas | Mažo projekto kūrimas | 8–12 val. | Savarankiškai įgyvendina pilną sprendimą |

## Tvarkaraštis (pavyzdys)
- Savaitė 1: Įvadas, aplinka, esminės sąvokos
- Savaitė 2: Gylinimasis į pagrindus, praktika
- Savaitė 3: Projekto planavimas, prototipo kūrimas
- Savaitė 4: Projekto realizacija, peržiūra ir pristatymas

## Įrankiai ir aplinka
- Operacinė sistema: Linux, macOS arba Windows
- Redaktorius/IDE: VS Code (arba alternatyva)
- Versijavimas: Git + GitHub/GitLab
- Papildomi įrankiai: nurodykite specifinius SDK, kalbų versijas ar priklausomybes, jei aktualu

## Įdiegimas / paruošimas
1. Įsidiekite rekomenduojamą redaktorių/IDE
2. Įsidiekite reikalingas kalbų versijas/SDK (jei taikoma)
3. Paruoškite projektinę aplinką (repo klonavimas, priklausomybių diegimas, testų paleidimas)

```bash
# Pavyzdžiai (koreguokite pagal kursą)
# Repo klonavimas
git clone <REPO_URL>
cd <REPO_KATALOGAS>

# Priklausomybių diegimas (pvz., Node.js aplinka)
npm ci

# Testų paleidimas
npm test
```

## Mokymosi rezultatai
Sėkmingai baigęs(-usi) kursą dalyvis:
- Supranta pagrindines kurso srities sąvokas ir metodikas
- Geba pritaikyti žinias praktikoje kuriant/prototipuojant sprendimus
- Geba dirbti su naudotais įrankiais ir darbo eiga
- Geba savarankiškai toliau gilinti žinias

## Vertinimas
- Dalyvavimas ir aktyvumas: 10 %
- Namų darbai/užduotys: 30 %
- Tarpinis vertinimas (jei taikoma): 20 %
- Baigiamasis projektas: 40 %

Projektų vertinimo gaires (pavyzdys):
- Reikalavimų atitikimas ir funkcionalumas
- Kodo/konstrukcijos aiškumas ir tvarkingumas
- Testuojamumas ir kokybės praktikos
- Dokumentavimas ir pristatymas

## Medžiagos ir nuorodos
- Oficiali dokumentacija: nurodykite svarbiausias dokumentacijas
- Vadovai/straipsniai: papildomos nuorodos gilinimuisi
- Pavyzdiniai projektai: repozitorijos ar demonstraciniai pavyzdžiai

## Kaip prisidėti
- Siūlykite pataisas ir papildymus per Pull Request
- Diskutuokite dėl reikšmingų pakeitimų prieš pateikdami PR
- Laikykitės vieningo stiliaus ir pateikite aiškius aprašus

## Licencija
Jei nenurodyta kitaip, turinys gali būti platinamas pagal „Creative Commons Attribution-ShareAlike 4.0“ (CC BY-SA 4.0) licenciją.

## Pakeitimų žurnalas
- v0.1.0: Pirminė kurikulumo README versija
