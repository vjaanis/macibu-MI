# Dizains

## Dizaina mērķis

Vietnei jāizskatās modernai, mierīgai un uzticamai, vienlaikus paliekot ātrai un
viegli uzturamai ar tīru HTML un CSS. Dizains ir minimālistisks: daudz brīvas
telpas, skaidra tipogrāfija, gaiši bēši pamata foni un atturīgi zaļi akcenti.
Vizuālā sistēma balstās uz nelielu dizaina tokenu kopu un atkārtoti
izmantojamiem UI elementiem, nevis katrai sadaļai atsevišķi rakstītiem stiliem.

Galvenie principi:

- **saturs pirmajā vietā** — katram vizuālajam elementam ir skaidrs uzdevums;
- **mazāk, bet precīzāk** — neizmanto liekas ēnas, gradientus un ornamentus;
- **mobile first** — pamata izkārtojums paredzēts mazam ekrānam;
- **konsekvence** — vienāda nozīme vienmēr izskatās un darbojas vienādi;
- **pieejamība** — krāsa nav vienīgais nozīmes signāls;
- **progresīva uzlabošana** — saturs ir lietojams arī bez JavaScript;
- **atkārtota izmantošana** — komponentus veido no kopīgiem tokeniem un klasēm.

## Vizuālais virziens

Mērķa dizains izmanto siltu bēšu fonu un ļoti gaišas zaļas virsmas. Tumši zaļš
teksts nodrošina mierīgu kontrastu, bet vidēji zaļš akcents norāda galvenās
darbības. Komponentus no fona galvenokārt atdala ar atstarpi un smalku apmali;
ēna ir tikai paceltiem vai pārklājošiem elementiem.

Vizuālais raksturs:

- silts, gaiši bēšs lapas fons;
- gaiši zaļas sadaļas un kartīšu akcenti;
- tumši zaļpelēks teksts ar skaidru kontrastu;
- piesātināts, bet kluss zaļš galvenajām darbībām;
- mēreni noapaļoti stūri un smalkas apmales;
- plašas atstarpes un skaidra tipogrāfiskā hierarhija.

No dizaina izslēdz stikla efektus, spilgtus gradientus, krāsainas gaismas,
smagas ēnas un nevajadzīgas dekoratīvas ikonas. Vienā skatā izmanto ne vairāk kā
vienu izteiktu akcenta krāsu.

## Dizaina tokeni

Visas pamatvērtības definē vienuviet kā CSS mainīgos. Komponentos nelieto
nejaušas krāsu vai atstarpju vērtības, ja to var izteikt ar esošu tokenu.

```css
:root {
  /* Krāsas */
  --color-bg: #f3f1e8;
  --color-surface: #faf8f2;
  --color-surface-soft: #e5eee3;
  --color-surface-raised: #ffffff;
  --color-text: #243127;
  --color-text-muted: #626d63;
  --color-border: #cbd4c8;
  --color-primary: #426a4b;
  --color-primary-hover: #35593e;
  --color-on-primary: #fffdf8;
  --color-secondary: #8a7657;
  --color-success: #377a4b;
  --color-warning: #9c6b19;
  --color-danger: #a8493d;

  /* Tipogrāfija */
  --font-sans: Inter, ui-sans-serif, system-ui, -apple-system,
    BlinkMacSystemFont, "Segoe UI", sans-serif;
  --font-mono: "SFMono-Regular", Consolas, "Liberation Mono", monospace;
  --text-xs: 0.75rem;
  --text-sm: 0.875rem;
  --text-base: 1rem;
  --text-lg: 1.125rem;
  --text-xl: 1.25rem;
  --text-2xl: clamp(1.75rem, 4vw, 2.5rem);
  --text-display: clamp(2.75rem, 9vw, 6rem);

  /* Atstarpes — 4 px solis */
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-6: 1.5rem;
  --space-8: 2rem;
  --space-12: 3rem;
  --space-16: 4rem;
  --space-24: 6rem;

  /* Forma un efekti */
  --radius-sm: 0.375rem;
  --radius-md: 0.625rem;
  --radius-lg: 1rem;
  --radius-pill: 999px;
  --shadow-sm: 0 2px 8px rgb(36 49 39 / 8%);
  --shadow-lg: 0 12px 30px rgb(36 49 39 / 12%);
  --focus-ring: 0 0 0 3px rgb(66 106 75 / 28%);
  --content-width: 72rem;
  --transition-fast: 160ms ease;
}
```

Ja mainās vizuālais virziens, vispirms maina tokenus. Jauns tokens ir pamatots,
ja viena vērtība tiek izmantota vairākās vietās vai tai ir noteikta semantiska
nozīme.

## Tipogrāfija

Pamatā izmanto sistēmas fontus, lai vietne ielādētos ātri un nebūtu atkarīga no
ārēja fontu servisa.

- `h1` lapā ir tikai viens un raksturo galveno tēmu;
- virsrakstu līmeņus neizlaiž vizuāla izmēra dēļ;
- pamatteksta izmērs ir vismaz `1rem`;
- pamatteksta rindstarpa ir `1.6–1.75`;
- teksta rindas garums nepārsniedz aptuveni `65ch`;
- sekundārais teksts drīkst būt klusāks, bet tam saglabā pietiekamu kontrastu;
- tehniskiem fragmentiem izmanto monospace fontu.

```css
body {
  color: var(--color-text);
  background: var(--color-bg);
  font: 400 var(--text-base) / 1.7 var(--font-sans);
}

h1,
h2,
h3 {
  margin: 0;
  line-height: 1.1;
  text-wrap: balance;
}

p {
  max-width: 65ch;
}
```

## Lapas režģis

Saturs atrodas kopīgā `.container` elementā. Tas ierobežo maksimālo platumu un
nodrošina drošu atkāpi no ekrāna malām.

```css
.container {
  width: min(100% - 2rem, var(--content-width));
  margin-inline: auto;
}

.section {
  padding-block: clamp(var(--space-16), 9vw, var(--space-24));
}

.stack {
  display: flex;
  flex-direction: column;
  gap: var(--stack-space, var(--space-6));
}

.cluster {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: var(--cluster-space, var(--space-3));
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 17rem), 1fr));
  gap: var(--space-6);
}
```

`.stack`, `.cluster` un `.grid` ir izkārtojuma palīgklases. Tās risina elementu
attiecības un neuzliek krāsu, apmali vai tipogrāfiju.

## Responsīvais dizains

Pamata CSS paredzēts 320 pikseļu platam ekrānam. Platāka ekrāna noteikumi tiek
pievienoti ar `min-width`, kad saturs konkrētajā komponentā sāk izskatīties
saspiests. Izmērus izvēlas pēc satura, nevis konkrētu ierīču modeļiem.

Ieteicamie orientieri:

| Platums | Lietojums |
| --- | --- |
| līdz `39.99rem` | viena kolonna, mobilā navigācija |
| no `40rem` | divu kolonnu kartītes, plašākas atkāpes |
| no `64rem` | pilna navigācija, sarežģītāki vairāku kolonnu izkārtojumi |

```css
@media (min-width: 40rem) {
  .hero {
    grid-template-columns: 1.15fr 0.85fr;
  }
}

@media (min-width: 64rem) {
  .site-nav__menu {
    display: flex;
  }
}
```

Interaktīva elementa skāriena laukums ir vismaz `44 × 44` pikseļi. Horizontāla
ritināšana pamatlapā nav pieļaujama. Attēliem izmanto `max-width: 100%` un
vajadzības gadījumā `aspect-ratio`, lai ielādes laikā nemainītos izkārtojums.

## Komponentu nosaukumi

Atkārtoti izmantojams UI elements saņem patstāvīgu komponenta klasi. Variantiem
izmanto modifikatoru, bet iekšējiem elementiem — komponenta prefiksu.

```text
.button
.button--primary
.button--secondary
.button--danger
.card
.card__title
.card__content
.card--featured
```

Komponenta izskatu nepiesaista lapas atrašanās vietai, piemēram,
`.homepage .sidebar button`. Komponentam jādarbojas jebkurā lapas sadaļā bez
specifiskāka selektora.

## Atkārtoti izmantojamie UI elementi

### Pogas

Pogu izmanto darbībai, bet saiti — navigācijai. Abām var būt kopīgs vizuālais
stils, taču HTML elements saglabā pareizo semantiku.

```html
<a class="button button--primary" href="#saturs">Sākt</a>
<button class="button button--secondary" type="button">Saglabāt</button>
```

```css
.button {
  min-height: 2.75rem;
  padding: var(--space-3) var(--space-6);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  border: 1px solid transparent;
  border-radius: var(--radius-md);
  font-weight: 700;
  text-decoration: none;
  cursor: pointer;
  transition: background-color var(--transition-fast),
    border-color var(--transition-fast), transform var(--transition-fast);
}

.button--primary {
  background: var(--color-primary);
  color: var(--color-on-primary);
}

.button--primary:hover:not(:disabled) {
  background: var(--color-primary-hover);
}

.button--secondary {
  border-color: var(--color-border);
  background: transparent;
  color: var(--color-text);
}

.button:hover:not(:disabled) {
  transform: translateY(-1px);
}

.button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

Galvenajai pogai vienā skatā jābūt vienai. Sekundārā poga ir mazāk izcelta.
Bīstamai neatgriezeniskai darbībai izmanto atsevišķu danger variantu un skaidru
tekstu, piemēram, “Dzēst projektu”, nevis tikai “Apstiprināt”.

### Kartītes

Kartīte grupē saistītu informāciju. Visa kartīte nav klikšķināma, ja tajā ir
vairāki neatkarīgi interaktīvi elementi.

```html
<article class="card stack">
  <p class="eyebrow">Jaunums</p>
  <h2 class="card__title">Kartītes virsraksts</h2>
  <p class="card__content">Īss un saprotams apraksts.</p>
  <a class="text-link" href="/vairak.html">Lasīt vairāk</a>
</article>
```

```css
.card {
  padding: var(--space-6);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  background: var(--color-surface);
}
```

Kartītei pēc noklusējuma nav ēnas. `box-shadow: var(--shadow-sm)` pievieno tikai
tad, ja kartīte vizuāli atrodas virs cita satura vai tai jāizceļas kā aktīvam
elementam. Izceltam, mierīgam variantam izmanto `.card--soft` ar
`background: var(--color-surface-soft)`.

### Navigācija

Galvenā navigācija atrodas `header` elementā un lieto `nav` ar saprotamu
`aria-label`. Aktīvā saite tiek norādīta ne tikai ar krāsu, bet arī ar formu,
pasvītrojumu vai `aria-current="page"`.

Mazā ekrānā navigācijas poga:

- ir īsts `button` elements;
- satur `aria-expanded` un `aria-controls`;
- saglabā redzamu tastatūras fokusu;
- aizver izvēlni pēc saites izvēles;
- JavaScript neesamības gadījumā neatstāj galvenās saites nepieejamas.

### Formas lauki

Katram laukam ir redzams `label`. Palīgteksts un kļūdas ziņa ir piesaistīta ar
`aria-describedby`. Vietturis nav etiķetes aizstājējs.

```html
<div class="field">
  <label class="field__label" for="email">E-pasts</label>
  <input class="field__input" id="email" name="email" type="email"
    autocomplete="email" aria-describedby="email-hint">
  <p class="field__hint" id="email-hint">Piemērs: vards@example.com</p>
</div>
```

Laukiem definē vismaz `default`, `hover`, `focus`, `disabled`, `invalid` un
`valid` stāvokļus. Kļūdu parāda ar tekstu un ikonu vai apmali, nevis tikai ar
sarkanu krāsu.

### Žetoni un statusi

`.badge` ir īsam statusam vai kategorijai, nevis darbībai. Statusu varianti ir
semantiski: `.badge--success`, `.badge--warning`, `.badge--danger` un
`.badge--neutral`.

Statusa tekstam jābūt saprotamam arī bez krāsas, piemēram, “Publicēts”,
“Jāpārbauda” vai “Kļūda”.

### Paziņojumi

`.alert` informē par rezultātu vai svarīgu nosacījumu. Tā struktūrā ir statuss,
virsraksts un īss skaidrojums. Dinamiskam paziņojumam izmanto atbilstošu
`role="status"` vai `role="alert"`, ņemot vērā ziņas steidzamību.

### Akordeons

Vienkāršam jautājumu sarakstam priekšroka ir vietējam HTML:

```html
<details class="accordion">
  <summary>Jautājums</summary>
  <div class="accordion__content">Atbilde</div>
</details>
```

JavaScript akordeonu veido tikai tad, ja nepieciešama uzvedība, ko `details` un
`summary` nevar nodrošināt.

### Dialogs

Dialogam izmanto vietējo `dialog` elementu. Tam nepieciešams skaidrs virsraksts,
aizvēršanas poga, paredzama fokusa uzvedība un atgriešanās pie elementa, kas
dialogu atvēra. Dialogu neizmanto informācijai, ko var parādīt parastā lapas
sadaļā.

## Komponentu stāvokļi

Katram interaktīvam komponentam projektē visus nepieciešamos stāvokļus pirms tā
ieviešanas:

| Stāvoklis | Prasība |
| --- | --- |
| Noklusējuma | skaidri saprotama funkcija |
| Hover | viegla vizuāla atgriezeniskā saite |
| Focus-visible | izteikts fokusa gredzens |
| Active | redzama nospiešanas reakcija |
| Disabled | mazāks izcēlums un bloķēta darbība |
| Loading | saglabāts izmērs un norādīta gaidīšana |
| Error | tekstuāls kļūdas skaidrojums |
| Success | apstiprinājums, ko var uztvert bez krāsas |

```css
:where(a, button, input, select, textarea, summary):focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 3px;
  box-shadow: var(--focus-ring);
}
```

Fokusa indikatoru nedrīkst noņemt bez līdzvērtīga aizstājēja.

## Ikonas un attēli

Ikonām izmanto vienotu līniju biezumu un izmēru sistēmu: `16`, `20`, `24` vai
`32` pikseļi. Dekoratīvām ikonām pievieno `aria-hidden="true"`. Ikonai, kas viena
pati veic darbību, pogai nepieciešams saprotams pieejamais nosaukums.

Satura attēliem norāda `width`, `height` un atbilstošu `alt` tekstu. Dekoratīviem
attēliem izmanto tukšu `alt=""`. Tekstu neievieto attēlā, ja tas nav pieejams arī
HTML formā.

## Kustība

Animācijas ir īsas un izskaidro stāvokļa maiņu. Parastai pārejai izmanto
`120–240ms`; lielākai izkārtojuma pārejai ne vairāk par aptuveni `400ms`.

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    scroll-behavior: auto !important;
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

Automātiski kustīgs saturs, paralakses efekti un nepārtrauktas dekoratīvas
animācijas nav noklusējuma dizaina daļa.

## Krāsu režīms

Pamata dizains ir gaišs: bēšs lapas fons, balti vai gaiši zaļi satura laukumi un
tumši zaļpelēks teksts. Šī konsekventā palete ir daļa no minimālisma, tāpēc tumšā
režīma variants sākotnēji nav paredzēts.

Tumšo režīmu drīkst pievienot tikai kā pilnībā izstrādātu, lietotāja vadītu
funkciju ar atsevišķu semantisko tokenu kopu un pārbaudītu visu komponentu
kontrastu. Pārlūka `prefers-color-scheme` nedrīkst automātiski radīt daļēji
pārkrāsotu saskarni.

## Pieejamības minimums

- parasta teksta kontrasts pret fonu ir vismaz `4.5:1`;
- liela teksta un būtisku UI robežu kontrasts ir vismaz `3:1`;
- lapa ir pilnībā lietojama ar tastatūru;
- fokusa secība atbilst vizuālajai secībai;
- skāriena mērķi ir vismaz `44 × 44` pikseļi;
- saturs paliek saprotams pie `200%` teksta palielinājuma;
- nozīmi nenodod tikai ar krāsu, atrašanās vietu vai kustību.

## Dizaina kvalitātes kontrolsaraksts

Pirms jauna komponenta vai sadaļas publicēšanas pārbauda:

1. vai var izmantot jau esošu komponentu;
2. vai tiek lietoti esošie krāsu, atstarpju un formas tokeni;
3. vai komponents darbojas no 320 pikseļu platuma;
4. vai ir izstrādāti hover, focus, disabled un kļūdas stāvokļi;
5. vai komponents ir lietojams ar tastatūru;
6. vai teksts un funkcija ir saprotama bez dekoratīvām ikonām;
7. vai nav nevajadzīgas JavaScript vai ārējas bibliotēkas;
8. vai izmaiņa pārbaudīta vismaz vienā mobilā un vienā darbvirsmas platumā.

Ja komponents tiek izmantots atkārtoti, tā HTML paraugu, variantus un ierobežojumus
pievieno šim dokumentam, lai nākamās sadaļas saglabātu vienotu valodu.
