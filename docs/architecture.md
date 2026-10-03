# Arhitektūra

## Mērķis

Vietne ir neliela, ātra un viegli uzturama statiska mājaslapa. Tā tiek veidota
ar tīru HTML, CSS un JavaScript, neizmantojot ietvarus, pakotņu pārvaldnieku vai
būvēšanas procesu.

Galvenie principi:

- saturs un semantiskā struktūra atrodas HTML;
- izskats un responsīvais izkārtojums atrodas CSS;
- JavaScript nodrošina tikai interaktivitāti;
- pamatinformācijai jābūt pieejamai arī tad, ja JavaScript nav ielādēts;
- produkcijā tiek publicēti tie paši faili, kas atrodas projekta mapē.

## Sistēmas pārskats

```text
Lietotāja pārlūks
        │
        │ HTTPS pieprasījums
        ▼
      nginx
        │
        │ statiski faili
        ▼
/var/www/vjaanis.gleeze.com/
        ├── index.html
        └── assets/
            ├── css/styles.css
            ├── js/main.js
            └── images/
```

nginx apkalpo statiskos failus. Vietnei nav servera puses lietotnes, API,
datubāzes vai lietotāju kontu. HTTP pieprasījumi tiek pāradresēti uz HTTPS, un
TLS sertifikātu pārvalda servera `acme.sh` konfigurācija.

## Plānotā failu struktūra

```text
hello-world/
├── AGENTS.md
├── CLAUDE.md
├── README.md
├── index.html
├── assets/
│   ├── css/
│   │   └── styles.css
│   ├── js/
│   │   └── main.js
│   └── images/
│       └── ...
└── docs/
    ├── architecture.md
    ├── design.md
    ├── content.md
    ├── development.md
    └── testing.md
```

Sākotnējā Hello World versijā CSS atrodas `index.html`. Kad dizains tiek
paplašināts, stilus pārvieto uz `assets/css/styles.css`. JavaScript failu
`assets/js/main.js` pievieno tikai tad, kad rodas vajadzība pēc interaktīvas
uzvedības.

## Komponentu atbildības

### HTML

`index.html` satur:

- dokumenta metadatus, valodu, virsrakstu un aprakstu;
- semantiskos elementus, piemēram, `header`, `nav`, `main`, `section` un `footer`;
- visu galveno tekstu un saites;
- pieejamības atribūtus, ja ar semantisku HTML vien nepietiek;
- atsauces uz CSS un JavaScript failiem.

HTML nedrīkst saturēt biznesa loģiku. Iekļautos stilus izmanto tikai ļoti mazai
sākotnējai lapai; augot vietnei, tos pārvieto uz CSS failu.

### CSS

`assets/css/styles.css` atbild par:

- krāsām, fontiem un atstarpēm;
- izkārtojumu ar Flexbox un Grid;
- responsīvu darbību dažādos ekrāna platumos;
- fokusa, hover un citiem interaktīvo stāvokļu noformējumiem;
- samazinātu kustību lietotājiem ar `prefers-reduced-motion`.

Krāsas un bieži lietotus izmērus definē kā CSS mainīgos `:root` blokā. Klašu
nosaukumiem jāapraksta elementa loma, piemēram, `.hero`, `.site-nav` un
`.button--primary`.

### JavaScript

`assets/js/main.js` atbild tikai par pārlūka interaktivitāti, piemēram:

- mobilās izvēlnes atvēršanu;
- akordeonu vai dialogu vadību;
- formas lauku pārbaudi pirms nosūtīšanas;
- neliela lietotāja stāvokļa saglabāšanu `localStorage`.

JavaScript raksta kā nelielus, neatkarīgus moduļus vai funkcijas. DOM elementus
atlasa ar skaidrām klasēm vai `data-*` atribūtiem. Pirms notikuma piesaistes
pārbauda, vai elements eksistē. Skriptu ielādē ar `defer`, lai tas nebloķētu HTML
attēlošanu.

## Datu un notikumu plūsma

Vietnes pamata plūsma ir vienvirziena:

```text
HTML ielāde → CSS noformējums → JavaScript inicializācija
                                      │
                                      ▼
                              lietotāja darbība
                                      │
                                      ▼
                         konkrēta DOM elementa izmaiņa
```

Statiskajam saturam nav ārēja datu avota. Ja nepieciešams saglabāt nebūtisku
izvēli, piemēram, aizvērtu paziņojumu, to glabā `localStorage`. Personas datus,
paroles un slepenu informāciju pārlūka krātuvē neglabā.

## Lapas un navigācija

Sākotnēji vietne ir viena lapa `index.html`, un sadaļu saitēm izmanto fragmentus,
piemēram, `#par-mani` un `#kontakti`. Ja vēlāk rodas vairākas neatkarīgas satura
lapas, katrai izveido savu `.html` failu un izmanto parastas relatīvās saites.

izveidot vismaz 4–5 saturiski atšķirīgas sadaļas.

Klienta puses maršrutētājs nav paredzēts. Katrai adresei jāatveras tieši un jābūt
saprotamai bez JavaScript.

## Ārējās atkarības

Pamatversijai nav ārēju JavaScript vai CSS bibliotēku. Priekšroka ir sistēmas
fontiem, lokāliem attēliem un pārlūka standarta iespējām. Ārēju resursu drīkst
pievienot tikai ar skaidru ieguvumu, izvērtējot:

- veiktspēju un pieejamību;
- privātumu un sīkdatņu lietojumu;
- licences nosacījumus;
- darbību gadījumā, ja ārējais resurss nav sasniedzams.

## Pieejamība un pārlūku atbalsts

Vietnei jādarbojas aktuālajās Chrome, Firefox, Safari un Edge versijās. Galvenās
darbības pārbauda ar tastatūru un vismaz 320 pikseļu platu skatu.

Obligātās prasības:

- pareiza virsrakstu secība un semantisks HTML;
- redzams tastatūras fokuss;
- pietiekams teksta kontrasts;
- attēliem atbilstošs `alt` teksts;
- formas laukiem saistīti `label` elementi;
- JavaScript papildina lapu, nevis padara pamatinformāciju nepieejamu.

## Drošība

Tā kā vietne ir statiska, uzbrukuma virsma ir neliela. Projektā nedrīkst atrasties
API atslēgas, paroles, privātās atslēgas vai citi piekļuves dati. Lietotāja ievadi
nedrīkst ievietot DOM ar `innerHTML`; teksta attēlošanai izmanto `textContent`.

Visi produkcijas pieprasījumi izmanto HTTPS. Ja vēlāk pievieno ārējus skriptus vai
API, atsevišķi jāizvērtē satura drošības politika, CORS un ievades validācija.

## Veiktspēja

- CSS un JavaScript failiem jāpaliek maziem un bez neizmantota koda.
- Attēlus pirms publicēšanas samazina līdz vajadzīgajam izmēram un optimizē.
- Attēliem zem pirmā ekrāna izmanto `loading="lazy"`.
- JavaScript ielādē ar `defer`.
- Trešo pušu fontus un skriptus pēc iespējas neizmanto.

Atsevišķu failu minificēšana sākotnējā posmā nav vajadzīga, jo lasāms avota kods
ir svarīgāks un vietnes apjoms ir mazs.

## Izstrāde un publicēšana

Lokālai apskatei pietiek atvērt `index.html` pārlūkā. Ja tiek izmantoti pieprasījumi
ar `fetch` vai pārlūka drošības ierobežojumi traucē `file://` režīmā, projektu
palaiž ar vienkāršu lokālu statisko serveri uz `127.0.0.1`.

Produkcijā avota faili tiek kopēti uz:

```text
/var/www/vjaanis.gleeze.com/
```

nginx konfigurācija un HTTPS sertifikāti nav šī projekta repozitorija daļa.
Publicēšanas un pārbaudes komandas ir aprakstītas `development.md` un
`testing.md`.

## Kad arhitektūru pārskatīt

Tīrs HTML/CSS/JS paliek izvēlētā arhitektūra, kamēr vietne ir pārsvarā statiska.
Arhitektūru pārskata, ja parādās kāda no šīm prasībām:

- autentificēti lietotāji;
- koplietojami vai serverī glabāti dati;
- maksājumi;
- sarežģīta satura pārvaldība vairākiem redaktoriem;
- liels skaits atkārtotu lapu, ko manuāli uzturēt kļūst neērti.

Šādas prasības nenozīmē automātisku ietvara ieviešanu. Vispirms dokumentē
konkrēto problēmu, datu plūsmu un vienkāršāko risinājumu.
