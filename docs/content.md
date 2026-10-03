# Saturs

## Valoda un tonis

Vietnes pamatvaloda ir latviešu. Tekstam jābūt īsam, skaidram un saprotamam bez
tehniskām priekšzināšanām. Tonis ir draudzīgs un nedaudz rotaļīgs, bet ne
bērnišķīgs. Joki un metaforas palīdz mācīties, nevis novērš uzmanību.
Pirmajā lietojumā paskaidro: vaicājums ir uzdevums vai jautājums, ko dod MI.

## Pašreizējais stāvoklis un nākamās versijas tvērums

Pašreizējais `index.html` ir sākotnējā Hello World lapa. Tajā ir virsraksts
“Hello, World!” un paziņojums par darbību ar HTTPS. Šis paziņojums apliecina
savienojuma veidu produkcijā, nevis visas vietnes drošību; HTTPS pārbauda pēc
`testing.md` norādēm.

Šis dokuments nosaka nākamās versijas satura specifikāciju: viena statiska
MI mācību lapa ar pieciem posmiem un noslēguma izaicinājumu. Aprakstītā mācību
taka vēl nav īstenota. Dokumentācijas precizēšana pati par sevi nenozīmē lapas
ieviešanu vai publicēšanu.

Pirmā mācību versija izmanto iepriekš sagatavotus mācību piemērus. Tā neveic
pieprasījumus MI pakalpojumiem un neprasa ārēja rīka kontu. Piemērus apzīmē kā
“sagatavots mācību piemērs”, nevis kā šobrīd ģenerētu MI atbildi. Lietotājs
vingrinās formulēt uzdevumus un izvērtēt atbildes; īstas MI sarunas integrācija
nav šīs versijas daļa.

Vietne neprasa reģistrāciju, kontaktinformāciju vai maksājumu. Tā nenosūta
lietotāja atbildes serverim. Tehniskais risinājums ievēro `architecture.md`,
noformējums — `design.md`, pārbaudes — `testing.md`.

## Mērķis un auditorija

Vietne ir neliela pašmācības taka iesācējiem bez programmēšanas priekšzināšanām.
Tās mērķis ir palīdzēt uzrakstīt skaidru MI uzdevumu, izvēlēties atbilstošu
pārbaudes darbību un atpazīt datus, kurus nedrīkst ievadīt.

## Galvenais vēstījums un navigācija

- **Virsraksts:** “Hei, MI — iepazīsimies!”
- **Apakšvirsraksts:** “Īsa un praktiska mācību taka ar sagatavotiem piemēriem.
  Mācies veidot skaidrus vaicājumus un pārbaudīt atbildes.”
- **Galvenā saite:** “Sākt piedzīvojumu” → `#iepazisanas`.
- **Papildu saite:** “Kā tas darbojas?” → `#ka-tas-darbojas`.

Sadaļā `#ka-tas-darbojas` parāda tekstu:

> Izpildi piecus īsus uzdevumus sev vēlamā secībā. Šeit izmantoti sagatavoti
> mācību piemēri; vietne neveido jaunas MI atbildes. Izlasi skaidrojumus,
> pārbaudi savu darbu un atzīmē apgūtos posmus. Noslēgumā izveido savu vaicājumu.

Lapas sākumā piedāvā saites uz visiem pieciem posmiem un noslēgumu. Tās ir
parastas fragmentu saites, kas darbojas arī bez JavaScript.

## Ievads un sasniedzamie rezultāti

Iedomājies MI kā centīgu palīgu, kurš spēj piedāvāt tekstus un idejas, bet
reizēm atbild ar pārliecību arī tad, kad kļūdās. Tavs uzdevums ir dot skaidras
norādes, uzdot papildjautājumus un pārbaudīt svarīgos faktus.

Pēc takas lietotājs var pašvērtējumā pārbaudīt, vai viņš spēj:

- atšķirt ideju vai melnrakstu no pārbaudīta fakta;
- papildināt vaicājumu ar mērķi, kontekstu un vēlamo formātu;
- izvēlēties, kā pārbaudīt apgalvojumu vai iegūt trūkstošo informāciju;
- salīdzināt variantus pēc konkrētiem nosacījumiem;
- aizstāt privātus datus ar izdomātiem piemēriem.

## Piecu posmu mācību taka

Katram posmam parāda mērķi, uzdevumu, skaidrojumu un pašvērtējuma nosacījumu.
Skaidrojumus var atvērt ar HTML `details` un `summary`, arī bez JavaScript.
Tie ir pieejami neatkarīgi no atbildes vai progresa.

### 1. Iepazīšanās pietura — `#iepazisanas`

**Mērķis:** saprast, kādām darbībām MI atbilde var būt sākumpunkts.

**Uzdevums:** salīdzini divus lūgumus: “Piedāvā trīs izdomātus stāsta
nosaukumus” un “Garantē, ka manā tekstā visi fakti ir pareizi”. Kurā gadījumā
pietiek izvērtēt idejas, un kurā vajadzīga neatkarīga faktu pārbaude?

**Skaidrojums:** izdomāta stāsta nosaukumus var izvēlēties pēc piemērotības.
Faktu pareizību nevar garantēt tikai ar pārliecinoši uzrakstītu atbildi —
apgalvojumi jāsalīdzina ar uzticamiem avotiem.

**Pašvērtējums:** vari paskaidrot, kāpēc idejas izvēle un fakta pārbaude ir
atšķirīgi uzdevumi.

### 2. Vaicājumu darbnīca — `#vaicajumi`

**Mērķis:** pārvērst miglainu lūgumu konkrētā uzdevumā.

**Miglainais vaicājums:** “Uzraksti tekstu par kosmosu.”

**Uzdevums:** uzraksti savu versiju, pievienojot auditoriju, teksta mērķi,
garumu un noskaņu. Teksta lauka etiķete: “Tavs uzlabotais vaicājums”.

**Sagatavots mācību piemērs:** “Uzraksti apmēram 100 vārdu ievadu par Marsa
izpēti 12 gadus veciem skolēniem. Mērķis ir radīt interesi par šo tēmu.
Izmanto aizraujošu valodu, norādi, kuri fakti jāpārbauda, un noslēgumā uzdod
vienu jautājumu pārdomām.”

**Skaidrojums:** auditorija ietekmē sarežģītību, mērķis — satura izvēli,
garums — apjomu, noskaņa — izteiksmi. Lūgums pārbaudīt faktus pats par sevi
nepierāda atbildes pareizību. Nav vienas obligātas vaicājuma versijas.

**Pašvērtējums:** tavā tekstā ir visas četras detaļas, un vari paskaidrot
vismaz vienas detaļas nozīmi. Vietne automātiski nevērtē brīvā teksta kvalitāti.

### 3. Faktu detektīvs — `#fakti`

**Mērķis:** izvēlēties pārbaudes darbību pēc apgalvojuma veida.

**Uzdevums:** katram sagatavotajam piemēram izvēlies vispiemērotāko nākamo soli:
“Pārbaudīt avotu”, “Precizēt kontekstu” vai “Izvērtēt kā ideju”.

| Sagatavots mācību piemērs | Paredzētā izvēle | Skaidrojums |
| --- | --- | --- |
| “Saskaņā ar pētījumu 87% skolēnu labāk mācās naktī.” Nav norādīts avots. | Pārbaudīt avotu | Precīzs skaitlis un atsauce uz nenosauktu pētījumu nav pierādījums. Atrodi pētījumu un pārbaudi, ko tas patiesībā secina; līdz tam apgalvojumu neizmanto kā faktu. |
| “Šis ir labākais maršruts.” Nav norādīts sākumpunkts, galamērķis vai pārvietošanās veids. | Precizēt kontekstu | Vispirms noskaidro trūkstošos nosacījumus. Pēc tam pārbaudi maršruta informāciju. |
| “Izdomāts stāsta nosaukums: Zvaigžņu pastnieks.” | Izvērtēt kā ideju | Šeit piedāvāta radoša ideja. Izvērtē, vai tā atbilst stāstam; tā nav pasniegta kā faktisks apgalvojums. |

**Skaidrojums:** skaitlis pirmajā piemērā ir izdomāts tikai vingrinājumam. To nepasniedz kā
īsta pētījuma rezultātu. Izvēles attiecas uz nākamo soli, nevis atbildes
patiesuma garantiju.

Pēc izvēles parāda paredzēto soli un skaidrojumu. Citas izvēles gadījumā
parāda: “Apskati skaidrojumu un mēģini vēlreiz.” Atkārtoti mēģinājumi ir atļauti.

**Pašvērtējums:** esi izvēlējies paredzēto soli visiem trim piemēriem un
izlasījis skaidrojumus. Bez JavaScript vari salīdzināt izvēles pats.

### 4. Ideju laboratorija — `#idejas`

**Mērķis:** izvēlēties piemērotu ideju pēc skaidriem ierobežojumiem.

**Uzdevums:** vajadzīga 15 minūšu aktivitāte klasē bez interneta un papildu
materiāliem. Salīdzini trīs sagatavotus variantus: tiešsaistes viktorīnu,
papīra plakātu darbnīcu un stāsta veidošanu mutiski pa vienam teikumam.
Izvēlies piemērotāko un pamato izvēli.

**Skaidrojums:** mutiska stāsta veidošana neprasa internetu vai materiālus,
un tai var noteikt 15 minūšu robežu. Tiešsaistes viktorīnai vajadzīgs internets;
plakātiem — papīrs un rakstāmpiederumi. Mainoties nosacījumiem, var mainīties
arī labākā izvēle.

**Pašvērtējums:** vari pamatot izvēli ar laiku, interneta pieejamību un
materiāliem, nevis tikai ar personīgu patiku.

### 5. Drošības finišs — `#drosiba`

**Mērķis:** atpazīt informāciju, kuru nevajag uzticēt MI rīkam.

**Uzdevums:** palīdzības pieprasījumā plānots ievietot “manu paroli”,
“klienta vārdu un personas kodu” un “izdomātu situāciju bez īstu cilvēku datiem”.
Kuru piemēru izvēlēsies? Kā pārveidosi pārējos?

**Skaidrojums:** izmanto izdomāto situāciju. Paroli izņem pilnībā; klienta
situāciju apraksti ar izdomātiem datiem, izņemot arī citas identificējošas un
konfidenciālas detaļas. Vārda aizstāšana vien vēl nenodrošina privātumu.
Vingrinājumā nelūdz ievadīt īstus sensitīvus datus.

**Pašvērtējums:** vari izvēlēties izdomāto piemēru un paskaidrot, kāpēc abus
pārējos nedrīkst ievadīt sākotnējā formā.

**Drošības mugursoma:**

- **Sargā datus** — neievadi paroles, personas kodus vai konfidenciālu informāciju.
- **Pārbaudi faktus** — svarīgus apgalvojumus salīdzini ar uzticamiem avotiem.
- **Tu esi kapteinis** — MI piedāvā variantus, gala lēmumu pieņem cilvēks.

## Progress un atkārtošana

Katra posma beigās ir poga “Atzīmēt posmu kā apgūtu”. Lietotājs to nospiež
pēc uzdevuma, skaidrojuma un pašvērtējuma. Tā ir paša lietotāja atzīme,
nevis automātisks zināšanu novērtējums. Atkārtota nospiešana nepievieno
papildu punktus. Pie apgūta posma piedāvā pogu “Noņemt atzīmi”.

Parāda statusu “Atzīmēti X no 5 posmiem” un īsu apstiprinājumu
“Posms atzīmēts kā apgūts.” Progress nekad nebloķē saturu.

Saglabā tikai piecu posmu atzīmes apmeklētāja `localStorage`; brīvā teksta
atbildes nesaglabā. Pirms pirmās atzīmes parāda:

> Posmu atzīmes saglabājas tikai šajā pārlūkā. Tavi ierakstītie teksti netiek
> saglabāti vai nosūtīti. Aizverot vai pārlādējot lapu, tie pazudīs.

Ja krātuve nav pieejama vai saglabātie dati ir bojāti, lapa turpina darboties.
Bojātas atzīmes ignorē; nesaglabājama progresa gadījumā parāda:
“Posmu atzīmes šoreiz saglabāsies tikai līdz lapas pārlādei.”

Poga “Notīrīt posmu atzīmes” dzēš tikai šīs takas progresu un atjauno “0 no 5”.
Tā nemaina atbildes laukus un neaizver skaidrojumus.

Bez JavaScript progresa vadīklas nav redzamas; parāda norādi:
“Posmu atzīmēšanai vajadzīgs JavaScript. Visus uzdevumus un skaidrojumus vari
izmantot arī bez tā.”

## Noslēguma izaicinājums — `#noslegums`

**Uzdevums:** izvēlies ikdienas darbu un uzraksti savu MI vaicājumu.
Teksta lauka etiķete: “Tavs noslēguma vaicājums”. Izmanto izdomātus datus.

**Pašvērtējuma kontrolsaraksts:**

- ir skaidrs mērķis;
- ir uzdevumam nepieciešamais konteksts;
- ir vēlamais atbildes formāts;
- ir vismaz viens kvalitātes vai drošības nosacījums;
- nav privātu vai konfidenciālu datu;
- vari nosaukt vienu veidu, kā pārbaudīsi saņemto rezultātu.

**Noslēguma teksts:** “Tu esi izpildījis mācību takas uzdevumus. Pārbaudi savu
vaicājumu pēc kontrolsaraksta un izvēlies, ko vēl vēlies uzlabot.”

Šo tekstu rāda kā noslēguma norādi, nevis automātiski piešķirtu kvalifikāciju.
Noslēgums ir pieejams arī tad, ja neviens posms nav atzīmēts.

**Saite:** “Atkārtot vaicājumu darbnīcu” → `#vaicajumi`. Tā pāriet uz otro
posmu, saglabājot pašreizējās atzīmes un laukos ierakstīto tekstu.

## SEO un kopīgošanas teksti

Šos metadatus ievieš reizē ar mācību lapas saturu, nevis Hello World lapā:

- **Lapas `<title>`:** “Hei, MI — mācību taka iesācējiem”.
- **Meta apraksts:** “Īsa MI mācību taka ar sagatavotiem piemēriem. Mācies veidot
  vaicājumus, pārbaudīt atbildes un sargāt privātus datus.”
- **Kopīgošanas virsraksts:** “Vai proti sarunāties ar MI?”
- **Kopīgošanas apraksts:** “Pieci īsi uzdevumi ar sagatavotiem piemēriem, lai
  trenētu skaidrus vaicājumus un atbilžu izvērtēšanu.”

## Ieviešanas secība un pieņemšanas kritēriji

1. Izveido ievadu, darbības skaidrojumu, piecus posmus un noslēgumu HTML.
   Katram fragmenta saites mērķim jāeksistē; katram posmam jāietver visas četras
   daļas: mērķis, uzdevums, skaidrojums un pašvērtējums.
2. Pievieno `design.md` noformējumu un pārbaudi lasāmību mobilajā un datora skatā.
3. Pievieno izvēļu atgriezenisko saiti un progresa atzīmes. Dinamiskus statusus
   paziņo arī palīgtehnoloģijām; vadīklas ir lietojamas ar tastatūru.
4. Pārbaudi visas trīs detektīva izvēles, nepareizu atbildi un atkārtotu mēģinājumu.
   Brīvā teksta laukiem nedrīkst piešķirt automātisku pareizības vērtējumu.
5. Pārbaudi atzīmes pievienošanu, noņemšanu, pārlādi un notīrīšanu; arī bojātu
   datu un nepieejamas krātuves scenārijus. Brīvā teksta atbildes nedrīkst nonākt
   krātuvē vai tīkla pieprasījumos.
6. Atspējo JavaScript un pārliecinies, ka viss mācību saturs, skaidrojumi un
   fragmentu saites darbojas un nav šķietami aktīvu progresa vadīklu.
7. Pārbaudi valodu, vienu `h1`, virsrakstu secību un metadatu atbilstību saturam.
   Pabeidz atbilstošās `testing.md` pārbaudes, tostarp 320 px skatu un 200%
   palielinājumu. Publicē tikai tad, ja publicēšana ietilpst lietotāja uzdevumā.

Dokumentācijas pabeigšana nozīmē, ka ieviešanas prasības ir konkrētas un
savstarpēji saskanīgas. Mācību vietnes pabeigšana nozīmē, ka iepriekš minētie
kritēriji ir īstenoti un pārbaudīti; ar šo dokumentu vien nepietiek.
