# Izstrāde

## Mērķis

Šis dokuments apraksta, kā cilvēks un MI aģents kopā izstrādā nelielu statisku
HTML/CSS/JavaScript vietni. Process paredzēts īsiem uzdevumiem, kuros aģents var
izlasīt projekta kontekstu, veikt ierobežotas izmaiņas, tās pārbaudīt un skaidri
nodot rezultātu.

MI aģents ir izstrādes palīgs, nevis projekta prasību avots. Lietotāja uzdevums
un projekta dokumentācija nosaka vēlamo rezultātu. Aģentam nav jāizdomā jaunas
produkta funkcijas, ārējas atkarības vai servera servisi bez pamatotas vajadzības.

## Projekta darba vide

```text
Avota projekts:  /home/kursants/workspace/hello-world
Produkcijas mape: /var/www/vjaanis.gleeze.com
Publiskā adrese:  https://vjaanis.gleeze.com
Web serveris:     nginx
Tehnoloģijas:     HTML, CSS, JavaScript
Būvēšanas solis:  nav
```

Avota projekts ir vienīgā vieta, kur pastāvīgi rediģē kodu. Produkcijas mapē
failus tikai publicē. Izmaiņas, kas veiktas tikai `/var/www/` mapē, nākamajā
publicēšanas reizē var pazust.

## Konteksta faili

Pirms darba MI aģents izlasa `AGENTS.md` un tikai uzdevumam vajadzīgos konteksta
failus:

| Fails | Kad to lasīt |
| --- | --- |
| `AGENTS.md` | vienmēr pirms projekta izmaiņām |
| `CLAUDE.md` | ja darbu veic Claude vai rīks, kas ievēro šo failu |
| `docs/architecture.md` | mainot failu struktūru, JavaScript vai tehnisko risinājumu |
| `docs/design.md` | mainot krāsas, izkārtojumu vai UI komponentus |
| `docs/content.md` | mainot tekstus, valodu vai informācijas hierarhiju |
| `docs/testing.md` | pirms un pēc izmaiņu pārbaudes |

Dokumentācija apraksta ieceri, bet dzīvais kods un servera stāvoklis parāda
faktisko situāciju. Ja tie atšķiras, aģents vispirms noskaidro atšķirības iemeslu,
nevis akli pārraksta kodu pēc dokumenta.

## Laba uzdevuma formulējums MI aģentam

Uzdevumā vēlams norādīt četras lietas:

1. **rezultāts** — kas pēc darba būs redzams vai darbosies;
2. **tvērums** — kura lapa, sadaļa vai komponents jāmaina;
3. **ierobežojumi** — kas jāsaglabā un ko nedrīkst pievienot;
4. **pieņemšanas kritēriji** — kā noteikt, ka darbs pabeigts.

Labs piemērs:

> Sākumlapai pievieno trīs pakalpojumu kartītes. Izmanto `design.md` gaiši zaļo
> un bēšo paleti, saglabā tīru HTML/CSS bez bibliotēkām, un panāc vienu kolonnu
> telefonā un trīs kolonnas no 64rem. Publicē tikai pēc responsīvās un HTTPS
> pārbaudes.

Pārāk neskaidrs piemērs:

> Uztaisi lapu modernāku.

Ja trūkst nebūtiska lēmuma, aģents izvēlas vienkāršāko risinājumu, kas atbilst
esošajai dokumentācijai. Ja izvēle būtiski mainītu produkta saturu, datu apstrādi
vai publisko uzvedību, aģents lūdz precizējumu.

## Darba plūsma

### 1. Izpēte

Pirms rediģēšanas aģents:

- izlasa projekta noteikumus un atbilstošo dokumentāciju;
- apskata esošo failu struktūru un maināmos failus;
- pārbauda, vai darba mapē nav nesaistītu lietotāja izmaiņu;
- ja uzdevums skar produkciju, pārbauda dzīvo lapu un nginx stāvokli;
- nosaka mazāko failu kopu, kas jāmaina.

Izpēte ir lasoša darbība. Tā nedrīkst mainīt failus, instalēt pakotnes vai
pārstartēt servisus.

### 2. Īss īstenošanas nodoms

Pirms rīku izmantošanas aģents lietotājam īsi pasaka:

- ko tas pārbaudīs;
- kurus failus paredzēts mainīt;
- kā tiks pārbaudīts rezultāts.

Nelielam uzdevumam nav vajadzīgs garš plāns. Sarežģītāku uzdevumu sadala
pārbaudāmos posmos, lai kļūda vienā posmā nesabojātu pārējo darbu.

### 3. Īstenošana

Aģents veic mazākās nepieciešamās izmaiņas:

- saglabā esošo failu kodējumu, stilu un lietotāja izmaiņas;
- neievieš bibliotēku, ja uzdevumu var skaidri atrisināt ar pārlūka iespējām;
- nepārraksta visu failu nelielas izmaiņas dēļ;
- neizveido abstrakciju vienreiz lietotam elementam;
- atkārtoti lietojamu UI veido saskaņā ar `design.md`;
- ja mainās projekta lēmumi, atjaunina atbilstošo `docs/` failu.

MI ģenerēto kodu nedrīkst uzskatīt par pareizu tikai tāpēc, ka tas izskatās
pārliecinoši. Katru mainīto ceļu pārbauda ar reālu komandu vai pārlūka darbību.

### 4. Pārbaude

Pārbaudes izvēlas pēc izmaiņas veida:

| Izmaiņa | Minimālā pārbaude |
| --- | --- |
| tikai teksts | HTML saturs, valoda un publiskā atbilde |
| HTML struktūra | semantika, saites, tastatūras secība |
| CSS | telefona un datora platums, kontrasts, fokuss |
| JavaScript | `node --check`, darbība un kļūdas pārlūka konsolē |
| aktīvi | faila ceļš, izmērs, formāts un `404` neesamība |
| nginx | `sudo nginx -t` pirms pārlādes |

Pilnais kontrolsaraksts ir `docs/testing.md`. Ja pārbaude neizdodas, aģents
vispirms nosaka cēloni, izlabo to un atkārto tieši saistītās pārbaudes.

### 5. Publicēšana

Publicē tikai tad, ja lietotāja uzdevums to paredz. Pirms publicēšanas:

1. avota faili ir saglabāti projekta mapē;
2. lokālās pārbaudes ir sekmīgas;
3. precīzi zināms, kuri faili tiks kopēti;
4. netiek pārrakstīti nesaistīti produkcijas faili.

Pēc publicēšanas pārbauda tieši publisko HTTPS adresi, nevis tikai avota failus.

### 6. Nodošana

Gala atbildē aģents īsi norāda:

- kas mainīts un kāpēc;
- kuri galvenie faili mainīti;
- kā darbs pārbaudīts;
- vai izmaiņas publicētas;
- zināmus ierobežojumus, ja tādi palikuši.

Aģents neuzskaita katru izmantoto komandu. Nodošanas mērķis ir ļaut cilvēkam
novērtēt rezultātu un turpināt darbu.

## Failu struktūra un pienākumi

Plānotā koda struktūra:

```text
index.html
assets/
├── css/
│   └── styles.css
├── js/
│   └── main.js
└── images/
docs/
```

- `index.html` satur semantisko struktūru un tekstu;
- `assets/css/styles.css` satur tokenus, izkārtojumus un komponentus;
- `assets/js/main.js` satur tikai nepieciešamo interaktivitāti;
- `assets/images/` satur optimizētus vietnes attēlus;
- `docs/` glabā projekta lēmumus, nevis dublē kodu.

Sākotnējā Hello World lapā stili vēl atrodas `index.html`. Tos pārvieto uz
atsevišķu failu tad, kad sākas plašāka vietnes izstrāde vai stili jākoplieto.

## HTML izstrādes noteikumi

- Dokumentam ir `<!doctype html>` un `lang="lv"`.
- Katrā lapā ir unikāls, saturam atbilstošs `<title>` un meta apraksts.
- Izmanto semantiskus elementus pirms vispārīgiem `div`.
- Lapā ir viens galvenais `h1`; nākamie virsraksti veido loģisku secību.
- Navigācijai lieto saiti, darbībai — pogu.
- Formas laukam ir redzams `label` un atbilstošs `autocomplete`.
- Attēlam norāda izmērus un saturam atbilstošu `alt`.
- Dekoratīvam attēlam lieto tukšu `alt=""`.
- ID ir unikāli, un fragmentu saites norāda uz eksistējošiem elementiem.

## CSS izstrādes noteikumi

- Sāk ar mobile-first pamata stiliem un pievieno `min-width` vaicājumus.
- Izmanto `design.md` tokenus, nevis nejaušas krāsas un atstarpes.
- Komponenta klase darbojas neatkarīgi no konkrētas lapas sadaļas.
- Selektoru specifiskumu saglabā zemu; izvairās no `!important`.
- Fokusa stāvokli nenoņem bez līdzvērtīga aizstājēja.
- Izkārtojumam izmanto Flexbox vai Grid, nevis absolūtu pozicionēšanu.
- Animācijām ievēro `prefers-reduced-motion`.
- Pārbauda, ka nav horizontālas ritināšanas pie 320 pikseļu platuma.

CSS secība vienā failā:

1. tokeni un pamata atiestatīšana;
2. globālā tipogrāfija;
3. izkārtojuma palīgklases;
4. komponenti;
5. lapai specifiskas sadaļas;
6. responsīvie vaicājumi;
7. samazinātas kustības noteikumi.

## JavaScript izstrādes noteikumi

- JavaScript pievieno tikai funkcijai, ko nevar pietiekami atrisināt ar HTML/CSS.
- Skriptu ielādē ar `defer`.
- Lieto `const` pēc noklusējuma un `let` tikai mainīgai atsaucei.
- Pirms notikuma piesaistes pārbauda, vai DOM elements eksistē.
- Tekstu ievieto ar `textContent`, nevis `innerHTML`.
- Funkcija veic vienu skaidru uzdevumu un saņem nepieciešamos datus parametros.
- UI stāvokli atspoguļo arī pieejamības atribūtos, piemēram, `aria-expanded`.
- Kļūda vienā izvēles komponentā nedrīkst apturēt pārējo lapas skriptu.
- Konsolē neatstāj atkļūdošanas ziņas.

Pamata sintakses pārbaude:

```bash
node --check assets/js/main.js
```

Ja JavaScript faila vēl nav, šī pārbaude nav jāizpilda.

## Darbs ar MI aģentu

### Ko aģents drīkst izlemt pats

Aģents drīkst patstāvīgi izvēlēties:

- semantiskā HTML elementa precīzu lietojumu;
- vienkārša responsīva režģa tehnisko realizāciju;
- funkciju un klašu saprotamus nosaukumus;
- pārbaudes, kas tieši izriet no izmaiņas;
- nelielus pieejamības labojumus, kas nemaina produkta ieceri.

### Kad vajadzīgs lietotāja lēmums

Aģents prasa virzienu, ja nepieciešams:

- izvēlēties starp būtiski atšķirīgu saturu vai lietotāja ceļiem;
- vākt vai sūtīt personas datus;
- pievienot ārēju servisu, analītiku vai trešās puses skriptu;
- ieviest kontus, maksājumus vai servera pusi;
- mainīt domēnu vai dzēst būtiskus lietotāja datus;
- publicēt, ja uzdevums attiecās tikai uz lokālu sagatavošanu.

### Ko aģents nedara pēc noklusējuma

- neinstalē ietvarus un pakotnes;
- neveic Git commit vai push;
- nemaina nginx, DNS vai sertifikātus;
- neievieto slepenas vērtības kodā vai dokumentācijā;
- nedzēš nesaistītus failus;
- nepārraksta lietotāja nepabeigtās izmaiņas;
- nepublicē eksperimentālu vai nepārbaudītu versiju.

## Darbs ar versiju kontroli

Ja projekts atrodas Git repozitorijā, pirms izmaiņām aģents pārbauda statusu un
saglabā visas nesaistītās izmaiņas. Tas nepārvieto, neatceļ un neformatē svešas
izmaiņas tikai tāpēc, lai darba koks būtu tīrs.

Commit veic tikai pēc lietotāja lūguma. Ieteicamais commit saturs ir viens
loģisks, pārbaudīts uzdevums. Commit ziņa īsi apraksta rezultātu, piemēram:

```text
feat: add responsive services section
fix: preserve keyboard focus in mobile menu
docs: define reusable UI development workflow
```

## Drošība un privātums

- Projektā neglabā tokenus, paroles, privātās atslēgas vai OAuth saturu.
- Slepenas vērtības, ja tādas vēlāk rodas, glabā tikai aizsargātā `.env` failā,
  ko statiskā vietne un pārlūks nesaņem.
- Publiskajā JavaScript nevar droši glabāt noslēpumu.
- Lietotāja ievadi neievieto HTML bez drošas apstrādes.
- Pirms ārēja attēla, fonta vai skripta pievienošanas izvērtē privātumu un licenci.
- MI aģenta izvades tekstā nedrīkst nonākt slepenas konfigurācijas vērtības.

## Lokālā apskate

Vienkāršu lapu var atvērt tieši pārlūkā. Ja nepieciešams korekts HTTP konteksts,
izmanto īslaicīgu lokālu serveri, kas klausās tikai uz `127.0.0.1`:

```bash
python3 -m http.server 8080 --bind 127.0.0.1
```

Pēc apskates serveri aptur. Lokālo izstrādes portu nepublicē internetā un tam
neveido nginx vhost.

## Publicēšana

### Tikai pašreizējā `index.html`

```bash
sudo install -o kursants -g kursants -m 0644 \
  index.html /var/www/vjaanis.gleeze.com/index.html
```

### Kad projektam ir `assets/` mape

Izveido mērķa apakšmapes un publicē precīzi zināmos failus. Neizmanto plašu
rekursīvu kopēšanu, kas varētu pārrakstīt vai nodzēst nesaistītu saturu.

```bash
sudo install -d -o kursants -g kursants \
  /var/www/vjaanis.gleeze.com/assets/css \
  /var/www/vjaanis.gleeze.com/assets/js \
  /var/www/vjaanis.gleeze.com/assets/images

sudo install -o kursants -g kursants -m 0644 \
  index.html /var/www/vjaanis.gleeze.com/index.html

sudo install -o kursants -g kursants -m 0644 \
  assets/css/styles.css /var/www/vjaanis.gleeze.com/assets/css/styles.css

sudo install -o kursants -g kursants -m 0644 \
  assets/js/main.js /var/www/vjaanis.gleeze.com/assets/js/main.js
```

Attēlus publicē atsevišķi, saglabājot failu nosaukumus un apakšmapes. Produkcijas
mapes īpašnieku un tiesības nemaina plašāk par nepieciešamajiem failiem.

Statisku failu izmaiņām nginx pārstartēšana nav vajadzīga. Ja mainās nginx
konfigurācija, pirms pārlādes obligāti izpilda:

```bash
sudo nginx -t
```

## Pārbaude pēc publicēšanas

```bash
curl -fsSI http://vjaanis.gleeze.com/
curl -fsSI https://vjaanis.gleeze.com/
curl -fsS https://vjaanis.gleeze.com/ | grep '<title>'
```

Sagaidāmais rezultāts:

- HTTP atbild ar `301` un norāda HTTPS adresi;
- HTTPS atbild ar `200` bez `-k` sertifikāta apiešanas;
- publicētajā HTML ir jaunais saturs;
- katrs jaunais CSS, JavaScript un attēla URL atbild ar `200`;
- nginx žurnālā nav jaunu kļūdu, kas saistītas ar izmaiņu.

## Pabeigta darba kritēriji

Uzdevums ir pabeigts, ja:

- lietotāja pieprasītais rezultāts ir īstenots pilnā norādītajā tvērumā;
- kods atbilst `architecture.md`, `design.md` un `content.md`;
- nav pievienota nevajadzīga atkarība vai servera sarežģītība;
- izpildītas izmaiņai atbilstošās pārbaudes;
- dokumentācija atjaunināta, ja mainījies projekta lēmums;
- publicēšana veikta tikai tad, ja tā bija uzdevuma daļa;
- gala atbildē ir rezultāts, pārbaudes un būtiski ierobežojumi.

Ja kādu kritēriju nevar izpildīt, aģents skaidri norāda, kas trūkst un kāpēc,
nevis pasniedz daļēju darbu kā pabeigtu.
