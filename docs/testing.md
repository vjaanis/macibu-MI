# Pārbaudes

## Mērķis

Šis dokuments nosaka pārbaudes nelielai statiskai HTML/CSS/JavaScript vietnei.
Mērķis ir laikus atrast bojātu saturu, saites, izkārtojumu, pieejamības un
JavaScript kļūdas, kā arī pārliecināties, ka publicētā versija sakrīt ar avotu.

Vietnei nav būvēšanas procesa vai testu ietvara. Tāpēc pārbaudes apvieno vienkāršas
komandrindas pārbaudes ar mērķtiecīgu apskati pārlūkā. Ja projekts kļūst lielāks,
automatizāciju pievieno tikai atkārtotām un kļūdām pakļautām pārbaudēm.

## Testēšanas principi

- Pārbauda mainīto uzvedību un tās tuvākās atkarības.
- Vispirms izmanto ātras un lētas pārbaudes, pēc tam pārlūka un produkcijas testus.
- MI ģenerētu kodu vienmēr pārbauda ar reālu izpildi vai vizuālu apskati.
- Testu rezultāts “komanda neizmeta kļūdu” nav pietiekams vizuālam uzdevumam.
- Publicēto vietni pārbauda atsevišķi no lokālajiem avota failiem.
- Kļūdas izlabo avota projektā, nevis tikai `/var/www/` produkcijas kopijā.
- Neizmanto `-k` vai citu TLS pārbaudes apiešanu gala HTTPS testā.

## Pārbaudes apjoms pēc izmaiņas

| Izmaiņa | Obligātais minimums |
| --- | --- |
| Teksts vai metadati | saturs, pareizrakstība, virsraksti, `<title>`, meta apraksts |
| HTML struktūra | validitāte, semantika, saites, tastatūras secība |
| CSS vai dizaina tokens | 320 px, planšetes un darbvirsmas skats, kontrasts, fokuss |
| Jauns UI komponents | visi stāvokļi, tastatūra, mobilais skats, atkārtota izmantošana |
| JavaScript | sintakse, galvenais scenārijs, kļūdas scenārijs, bez-JS režīms |
| Attēls vai cits aktīvs | URL, formāts, izmērs, `alt`, izkārtojuma stabilitāte |
| Navigācija | visas saites, aktīvais stāvoklis, fragments, atpakaļ poga |
| Forma | etiķetes, validācija, kļūdas, tastatūra, datu nosūtīšana |
| nginx vai publicēšana | `nginx -t`, HTTP → HTTPS, TLS, statusi, žurnāli |

Dokumentācijas izmaiņām nav jāpārbauda visa vietne, ja tās nemaina izpildāmo kodu.
Tomēr pārbauda dokumenta struktūru, failu atsauces un komandu piemēru atbilstību
dzīvajam projektam.

## Testēšanas vides

### Lokālais avots

Vienkāršu lapu var atvērt kā `file://`. Ja vietne izmanto `fetch`, moduļus vai
citas funkcijas, kam vajadzīgs HTTP konteksts, palaiž īslaicīgu serveri tikai uz
localhost:

```bash
python3 -m http.server 8080 --bind 127.0.0.1
```

Pēc pārbaudes serveri aptur. Lokālo portu nepublicē internetā.

### Produkcija

Produkcijas adrese ir:

```text
https://vjaanis.gleeze.com
```

Produkcijā pārbauda tikai pēc tam, kad lokālās pārbaudes ir sekmīgas un izmaiņa
ir publicēta. Produkcijas pārbaudes nedrīkst mainīt vai dzēst lietotāja datus.

## Ātrā pārbaude pirms publicēšanas

Katram koda uzdevumam izpilda vismaz šo kontrolsarakstu:

1. atver mainītos failus un pārbauda, ka nav nejaušu vai nepabeigtu izmaiņu;
2. pārbauda HTML dokumenta pamatstruktūru un lokālo failu ceļus;
3. ja ir JavaScript fails, izpilda `node --check`;
4. apskata lapu vismaz mobilajā un darbvirsmas platumā;
5. pārbauda mainītās darbības ar peli un tastatūru;
6. pārlūka konsolē nav jaunu kļūdu;
7. izpilda uzdevuma pieņemšanas kritērijus.

Ja projektā ir plānotā failu struktūra, pamata komandas ir:

```bash
test -s index.html
test -s assets/css/styles.css
node --check assets/js/main.js
```

Komandu izpilda tikai failam, kas projektā eksistē. Pašreizējai Hello World
versijai CSS vēl ir iekļauts `index.html`, un JavaScript faila nav.

## HTML pārbaude

### Dokumenta pamati

Pārbauda, ka:

- pirmajā rindā ir `<!doctype html>`;
- `<html>` elementam ir pareizs `lang`, šajā projektā `lang="lv"`;
- ir `meta charset="utf-8"` un viewport meta tags;
- katrai lapai ir unikāls un saturam atbilstošs `<title>`;
- meta apraksts īsi raksturo konkrēto lapu;
- lapā ir viens galvenais `h1`;
- virsrakstu līmeņi veido loģisku hierarhiju;
- galvenais saturs atrodas `main` elementā;
- ID vērtības ir unikālas.

### Semantika

- Navigācijai izmanto `nav`, lapas galvenei `header`, kājenei `footer`.
- Saiti izmanto pārejai uz adresi, pogu — darbībai pašreizējā lapā.
- Sarakstam izmanto `ul`, `ol` vai `dl`, nevis tikai vizuāli līdzīgas rindas.
- Tabulu izmanto tabulāriem datiem, nevis izkārtojumam.
- Formas laukam ir programmatiski saistīts un redzams `label`.
- `button` elementam norāda `type`, īpaši formā.

### HTML validācija

Ja sistēmā pieejams HTML validators, pārbauda visas `.html` lapas un izlabo
kļūdas. Brīdinājumu izvērtē pēc konteksta; to nedrīkst ignorēt bez iemesla.

Var izmantot W3C Nu HTML Checker pārlūkā vai projektā jau pieejamu lokālu
validatoru. Ja validatora nav, validāciju neaizstāj ar jaunas smagas atkarības
instalēšanu vienam nelielam labojumam; veic rūpīgu struktūras pārbaudi pārlūkā.

## Saites un aktīvi

Pārbauda:

- katra navigācijas saite atver paredzēto lapu vai sadaļu;
- fragmenta saites `#id` mērķis eksistē;
- iekšējās saites neizmanto nevajadzīgi absolūtu produkcijas domēnu;
- ārējā saite izmanto HTTPS, ja tas ir pieejams;
- CSS, JavaScript, attēli, fonti un ikonas neatbild ar `404`;
- failu nosaukumu lielie un mazie burti sakrīt arī Linux serverī;
- nav atsauču uz lokāliem datora ceļiem.

Publiska resursa pārbaudes piemērs:

```bash
curl -fsSI https://vjaanis.gleeze.com/
curl -fsSI https://vjaanis.gleeze.com/assets/css/styles.css
curl -fsSI https://vjaanis.gleeze.com/assets/js/main.js
```

Otrās un trešās komandas izmanto tikai tad, kad šie faili ir publicēti.

## CSS un responsīvā dizaina pārbaude

Lapu pārbauda vismaz šādos viewport izmēros:

| Skats | Platums × augstums | Ko pārbaudīt |
| --- | --- | --- |
| mazs telefons | `320 × 568` | pārplūde, pogas, teksta aplaušana |
| tipisks telefons | `390 × 844` | navigācija, atstarpes, skāriena mērķi |
| planšete | `768 × 1024` | kolonnu maiņa un tukšā telpa |
| klēpjdators | `1366 × 768` | pirmā ekrāna saturs un navigācija |
| plats ekrāns | `1920 × 1080` | maksimālais satura platums un rindas garums |

Katrā skatā pārbauda:

- nav horizontālas ritināšanas;
- teksts nepārklājas un netiek nogriezts;
- attēli saglabā proporcijas;
- saturs nav nepamatoti izstiepts platā ekrānā;
- galvenās darbības ir redzamas un sasniedzamas;
- skāriena mērķi ir vismaz `44 × 44` pikseļi;
- izkārtojums darbojas arī starp dokumentētajiem robežpunktiem.

Papildus pārbauda lapu ar `200%` pārlūka tālummaiņu un palielinātu noklusējuma
fonta izmēru. Saturs drīkst kļūt garāks, bet nedrīkst pazust vai pārklāties.

## Vizuālā kvalitāte

Salīdzina rezultātu ar `docs/design.md`:

- izmantota dokumentētā gaiši zaļā un bēšā palete;
- krāsas, atstarpes, rādiusi un ēnas nāk no dizaina tokeniem;
- atkārtoti elementi lieto vienus un tos pašus komponentus;
- galvenā un sekundārā darbība vizuāli atšķiras;
- fokusa stāvoklis ir skaidri redzams;
- minimālisma dizainu nepārslogo gradienti, smagas ēnas vai dekorācijas;
- teksta rindu garums un sadaļu atstarpes paliek ērti lasāmas.

Ja izmaiņa ir vizuāla, ekrānuzņēmums palīdz pārbaudīt kopskatu, bet neaizstāj
interaktivitātes, tastatūras un responsivitātes testus.

## Pieejamības pārbaude

### Tastatūra

Izmantojot tikai tastatūru:

1. ar `Tab` var sasniegt katru interaktīvo elementu;
2. fokusa secība atbilst vizuālajai secībai;
3. fokusa indikators vienmēr ir redzams;
4. saites un pogas aktivizējas ar paredzēto taustiņu;
5. mobilā izvēlne, akordeons un dialogs ir atverams un aizverams;
6. fokuss neiestrēgst un nepazūd;
7. izlaišanas saite ļauj pāriet uz galveno saturu, ja navigācija ir gara.

### Ekrānlasītāja pamati

Pārbauda pārlūka pieejamības kokā vai ar ekrānlasītāju:

- lapai ir saprotams nosaukums un orientieri;
- interaktīvajiem elementiem ir pieejami nosaukumi;
- attēlu `alt` teksti apraksta saturu, nevis atkārto blakus tekstu;
- dekoratīvi attēli netiek nevajadzīgi nolasīti;
- kļūdas un dinamiskie statusi tiek paziņoti;
- `aria-expanded`, `aria-current` un citi stāvokļi mainās kopā ar UI.

### Kontrasts un kustība

- parasta teksta kontrasts ir vismaz `4.5:1`;
- liela teksta un būtisku UI robežu kontrasts ir vismaz `3:1`;
- informācija nav atkarīga tikai no krāsas;
- ar ieslēgtu `prefers-reduced-motion: reduce` nav nevajadzīgas kustības;
- mirgojošs saturs netiek izmantots.

Automātisks pieejamības rīks var atrast biežas kļūdas, bet tas neaizstāj manuālu
tastatūras un satura saprotamības pārbaudi.

## JavaScript pārbaude

### Sintakse

```bash
node --check assets/js/main.js
```

### Funkcionālie scenāriji

Katram interaktīvam komponentam pārbauda:

- sākotnējo stāvokli;
- galveno lietotāja darbību;
- atkārtotu darbību, piemēram, atvērt → aizvērt → atvērt;
- malu gadījumu, piemēram, tukšu vērtību vai neesošu saglabātu stāvokli;
- tastatūras vadību;
- ARIA stāvokļa maiņu;
- kļūdu neesamību pārlūka konsolē.

Piemēri:

| Komponents | Scenāriji |
| --- | --- |
| Mobilā izvēlne | atveras, aizveras, aizveras pēc saites, atjauno `aria-expanded` |
| Akordeons | saturs atveras un aizveras, fokuss paliek uz vadības elementa |
| Dialogs | fokuss nonāk dialogā, `Escape` aizver, fokuss atgriežas |
| Forma | tukšs, nederīgs un derīgs lauks, kļūdas teksts, nosūtīšana |
| `localStorage` | nav datu, ir derīgi dati, ir bojāti dati, krātuve nav pieejama |

### Darbība bez JavaScript

Pārlūkā atspējo JavaScript vai bloķē skripta failu. Pārbauda, ka:

- galvenais saturs joprojām ir redzams;
- parastās saites turpina darboties;
- navigācija nav pilnībā paslēpta;
- JavaScript atkarīga funkcija nepārvēršas maldinošā, šķietami aktīvā vadīklā.

## Satura un SEO pārbaude

- Valoda atbilst `docs/content.md`.
- Nav drukas, pieturzīmju un faktu kļūdu.
- `<title>` ir konkrēts un nav vienāds visām lapām.
- Meta apraksts atbilst redzamajam saturam.
- Virsraksti īsi apkopo sadaļas.
- Saites teksts ir saprotams ārpus teikuma; neizmanto tikai “šeit”.
- Kanoniskā adrese, Open Graph dati un favicon tiek pārbaudīti, ja tie ir pievienoti.
- Lapa nesatur pagaidu tekstu, piemēram, “Lorem ipsum”, `TODO` vai atkļūdošanas datus.

Ātra pagaidu teksta meklēšana:

```bash
rg -n -i 'lorem|todo|fixme|console\.log|debugger' . \
  --glob '*.html' --glob '*.css' --glob '*.js'
```

## Veiktspējas pārbaude

Nelielai statiskai vietnei jāielādējas bez liekas JavaScript un ārējām
atkarībām. Pārbauda:

- attēli nav lielāki par reāli vajadzīgo izšķirtspēju;
- zem pirmā ekrāna esošiem attēliem ir `loading="lazy"`;
- attēliem norādīts `width` un `height` vai `aspect-ratio`;
- JavaScript ielādējas ar `defer`;
- nav neizmantotu fontu, bibliotēku vai lielu datu failu;
- tīkla panelī nav kļūdainu, dublētu vai bloķējošu pieprasījumu;
- ielādes laikā saturs būtiski nepārvietojas.

Pārlūka Lighthouse vai līdzīgu rīku izmanto diagnostikai. Rezultāta skaitlis nav
vienīgais pieņemšanas kritērijs; būtiskāka ir atrastās problēmas ietekme uz
lietotāju.

## Drošības un privātuma pārbaude

- Projektā un publicētajos failos nav tokenu, paroļu vai privāto atslēgu.
- Publiskajā JavaScript nav slepenu konfigurācijas vērtību.
- Lietotāja teksts netiek ievietots ar `innerHTML`.
- Ārējie skripti un resursi ir apzināti, nepieciešami un dokumentēti.
- Veidlapas nenosūta datus neparedzētam adresātam.
- `localStorage` nesatur personas vai sensitīvus datus.
- Publiskā lapa neielādē nevajadzīgus izsekotājus vai sīkdatnes.
- HTTPS sertifikāts ir derīgs īstajam domēnam.

Ātra sensitīvu marķieru meklēšana nav pilnvērtīgs slepeno datu skeneris, bet var
palīdzēt pamanīt acīmredzamu kļūdu:

```bash
rg -n -i 'api[_-]?key|secret|password|private[_-]?key|bearer ' . \
  --glob '*.html' --glob '*.css' --glob '*.js'
```

Katrs atradums jāizvērtē kontekstā, jo parauga teksts var nebūt noslēpums.

## Pārlūku pārbaude

Pirms būtiskas publicēšanas pārbauda aktuālā Chrome vai Chromium, Firefox un,
ja pieejams, Safari. Mazam labojumam pietiek ar galveno pārlūku un mērķētu
saderības pārbaudi, ja izmantota jauna CSS vai JavaScript iespēja.

Pārbauda:

- izkārtojumu un fontu aizvietošanu;
- fokusa un formu elementu izskatu;
- navigāciju un JavaScript darbības;
- CSS funkcijas, kurām var būt atšķirīgs atbalsts;
- skāriena uzvedību reālā mobilajā ierīcē, ja izmaiņa to būtiski skar.

## Produkcijas pārbaude

### Pirms publicēšanas

```bash
sudo nginx -t
```

Statisku failu maiņai nginx pārlāde nav vajadzīga. `nginx -t` ir obligāts, ja
mainīta nginx konfigurācija, un droša papildu pārbaude pirms nozīmīgas
publicēšanas.

### Pēc publicēšanas

```bash
curl -fsSI http://vjaanis.gleeze.com/
curl -fsSI https://vjaanis.gleeze.com/
curl -fsS https://vjaanis.gleeze.com/ | rg '<title>|Hello,'
```

Sagaidāmais rezultāts:

- HTTP atbild ar `301 Moved Permanently`;
- `Location` norāda `https://vjaanis.gleeze.com/`;
- HTTPS atbild ar `200` bez sertifikāta pārbaudes apiešanas;
- `Content-Type` ir atbilstošs resursam;
- publicētajā HTML ir jaunais saturs;
- CSS, JavaScript un attēlu resursi atbild ar `200`;
- nav negaidītu novirzīšanu ciklu vai `404`.

TLS sertifikāta pārbaude:

```bash
openssl s_client \
  -connect vjaanis.gleeze.com:443 \
  -servername vjaanis.gleeze.com </dev/null 2>/dev/null \
  | openssl x509 -noout -subject -issuer -dates -ext subjectAltName
```

Sertifikātam jābūt derīgam pārbaudes datumā, un `subjectAltName` jāsatur
`vjaanis.gleeze.com`.

Ja produkcijas pārbaude neizdodas, neuzskata darbu par pabeigtu. Pārbauda nginx
kļūdu žurnālu un publicēto failu tiesības, izlabo cēloni un atkārto pārbaudi.

## Regresijas pārbaude

Pēc izmaiņas papildus jaunajai funkcijai pārbauda vismaz:

- sākumlapas ielādi;
- galveno navigāciju;
- galveno aicinājumu uz darbību;
- mobilā izkārtojuma pamata plūsmu;
- tastatūras fokusu;
- JavaScript konsoles kļūdu neesamību;
- tos komponentus, kuri izmanto mainītos dizaina tokenus vai kopīgās funkcijas.

Jo kopīgāks ir mainītais kods, jo plašāka ir regresijas pārbaude. Viena dizaina
tokena maiņa var skart visas kartītes un pogas, bet vienas rindkopas teksts — tikai
konkrēto sadaļu.

## Kļūdu prioritātes

| Līmenis | Piemērs | Rīcība |
| --- | --- | --- |
| Bloķējoša | lapa neatveras, TLS kļūda, galvenā darbība nedarbojas | nepublicē vai nekavējoties atjauno darbību |
| Augsta | navigācija nav lietojama telefonā, būtiska pieejamības kļūda | izlabo pirms nodošanas |
| Vidēja | bojāts sekundārs izkārtojums vai nepareizs komponenta stāvoklis | izlabo uzdevuma ietvaros |
| Zema | neliela atstarpe vai kosmētiska neatbilstība | dokumentē un plāno, ja nav uzdevuma tvērumā |

Kļūdas prioritāti nosaka ietekme uz lietotāju, nevis tas, cik viegli vai grūti to
izlabot.

## Pārbaudes ziņojuma piemērs

MI aģenta vai izstrādātāja nodošanas ziņojums var būt īss:

```text
Pārbaudīts:
- HTML saturs un iekšējās saites;
- 320 px, 390 px un 1366 px izkārtojums;
- tastatūras navigācija un redzams fokuss;
- JavaScript sintakse un mobilās izvēlnes atvēršana/aizvēršana;
- HTTP 301 → HTTPS un HTTPS 200 produkcijā.

Ierobežojums:
- Safari pārbaude šajā vidē nebija pieejama.
```

Ziņojumā norāda tikai reāli veiktās pārbaudes. Nedrīkst apgalvot, ka tests ir
izturēts, ja tas nav palaists vai rezultāts nav apskatīts.

## Pabeigšanas kontrolsaraksts

Pirms uzdevuma nodošanas:

- [ ] izpildīti uzdevuma pieņemšanas kritēriji;
- [ ] HTML struktūra un saturs ir korekts;
- [ ] nav bojātu saišu vai trūkstošu aktīvu;
- [ ] izkārtojums pārbaudīts mobilajā un darbvirsmas platumā;
- [ ] galvenā plūsma darbojas ar tastatūru;
- [ ] nav jaunu pārlūka konsoles kļūdu;
- [ ] JavaScript sintakse ir derīga, ja JavaScript mainīts;
- [ ] nav nejauši publicētu noslēpumu vai atkļūdošanas datu;
- [ ] dokumentācija atjaunināta, ja mainījies projekta lēmums;
- [ ] produkcijas HTTPS pārbaude izturēta, ja izmaiņa publicēta;
- [ ] gala ziņojumā minētas tikai faktiski veiktās pārbaudes.
