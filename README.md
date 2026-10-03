# Hello World

Vienkārša statiska mājaslapa, kuru nginx publicē adresē
`https://vjaanis.gleeze.com` ar HTTP pāradresāciju uz HTTPS.

## Versija

Pašreizējās versijas numurs atrodas failā `VERSION`. Git tags `v<versija>`
norāda uz atbilstošo komitu. Versiju palielināšanas kārtība aprakstīta
`docs/development.md`.

## Projekta konteksts

Darba noteikumi ir `AGENTS.md` un `CLAUDE.md`. Paplašinātais konteksts ir sadalīts
mapē `docs/`: arhitektūra, dizains, saturs, izstrāde un pārbaudes.

## Publicēšana

Avota fails atrodas `index.html`. Domēna publiskā kopija tiek izvietota
`/var/www/vjaanis.gleeze.com/index.html`.

Pēc izmaiņām lapu var pārpublicēt ar:

```bash
sudo install -o kursants -g kursants -m 0644 index.html /var/www/vjaanis.gleeze.com/index.html
```
