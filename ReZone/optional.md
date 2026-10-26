# optional.json – popisy volitelných modů

Launcher bere volitelné mody ze tří míst a spojí je dohromady:

1. **Sekce `[====Optionals====]` v Mod Organizeru** (až po `== Custom addons HERE! ==`) – objeví se samy.
2. **Složky na Google Drive** (Addony, NPC Models, Zbraně, Ostatní, Textury) – dají se stáhnout. Každá kategorie může mít **libovolný počet odkazů** (Nastavení → Zdroje → + PŘIDAT ODKAZ): mody se načtou ze všech a odkazy slouží zároveň jako záložní zrcadla. Archivy můžou být i v podsložkách.
3. **`optional.json`** – přidá jim název, autora, popis, kategorii a číslo priority.

Stejně fungují **textury a sezóny** (stránka TEXTURY): mody pod separátorem `Jaro`, `Léto`, `Podzim`
nebo `Zima` v MO2 (na `=` a závorkách nezáleží, jde i `Spring`, `Summer`, `Autumn`, `Winter`),
mody ze složek sezón na Google Drive a mody s polem `season` v `optional.json`.
Sezóny nejsou součástí modpacku. Hráč vybere jednu sezónu: její mody se stáhnou (jen poprvé)
a zapnou, mody ostatních sezón se vypnou. Stažené sezóny zůstanou v MO2, takže přepnutí je
okamžité. Stahují se jen vybrané možnosti.

Jedna sezóna může mít víc možností na výběr – stačí modům dát stejné `group`:

```json
{ "name": "C Consciousness Grass and Trees Overhaul – Spring", "title": "C Consciousness – jarní tráva",
  "season": "Jaro", "group": "Tráva", "default": true, "priority": 10 },
{ "name": "Jiná jarní tráva", "season": "Jaro", "group": "Tráva", "priority": 11 },
{ "name": "Jarní počasí", "season": "Jaro", "priority": 20 }
```

Na stránce Jaro pak hráč vybere jednu ze dvou trav a jarní počasí si může zapnout nebo vypnout. Separátory sezón dej ideálně mimo sekci Optionals.

Záznam v `optional.json` není povinný. Mod bez záznamu se zobrazí taky, jen bez popisu.

## Pole

| Pole | Povinné | Co dělá |
|---|---|---|
| `name` | ano | Název modu. Číslo na začátku (`123- `), autor v závorce a velká/malá písmena se při porovnání ignorují, takže `Better HUD` najde i `123- Better HUD (Ncenka)`. U modu z Google Drive napiš název archivu bez `.7z`. |
| `title` | ne | Název v launcheru. Prázdný = název modu bez čísla a autora. |
| `author` | ne | Autor, zobrazí se v okně INFO. Prázdný = z názvu modu `Mod (Autor)` nebo `[Autor] Mod`. |
| `link` | ne | Odkaz na stránku modu (ModDB, GitHub…), v okně INFO. |
| `category` | ne | Kategorie = tlačítko filtru na stránce Volitelné (`Addony`, `Zbraně`, `NPC Models`, `Ostatní` nebo vlastní). U modů z Drive se doplní sama podle složky, u modů z MO2 podle podsekce. |
| `season` | ne | `Jaro`, `Léto`, `Podzim` nebo `Zima` – mod patří na stránku SEZÓNY místo Volitelné. Nemusíš vyplňovat, když je mod pod separátorem sezóny nebo ve složce sezóny na Drive. Po stažení se zařadí pod separátor své sezóny (podle `priority`). |
| `group` | ne | Jen u sezón: **skupina možností**, např. `Tráva` nebo `Počasí`. Z modů se stejnou sezónou a skupinou má hráč zapnutý vždy jen jeden (výběr kolečkem). Mody bez skupiny jdou zapnout/vypnout zaškrtnutím. |
| `default` | ne | Jen u sezón: `true` = doporučená možnost ve skupině, zapne se, dokud si hráč nevybere jinou. Bez `default` se vezme první mod ve skupině. |
| `bundle` | ne | **Balíček**: mody se stejným `bundle` se na stránce Volitelné ukážou jako jeden řádek (název = název balíčku), stahují se a zapínají/vypínají společně. Pořadí v load orderu určuje `priority` (bez ní pořadí záznamů v souboru). Popis stačí vyplnit u jednoho z modů. |
| `image` / `images` | ne | Obrázek / seznam obrázků do okna INFO (šipkami se přepíná). Přímý odkaz na obrázek (`.jpg`, `.png`, `.webp`), odkaz na soubor na Google Drive (`drive.google.com/file/d/…/view`, sdílený „kdokoli s odkazem“), Imgur (`imgur.com/ID`) nebo Dropbox. Funguje u volitelných modů i sezón. |
| `gallery` | ne | Odkaz na celou galerii (album Imgur, složka Drive…), v INFO jako odkaz „Galerie“. |
| `description` | ne | Text v okně INFO. Nový řádek = `\n`. |
| `priority` | ne | Číslo priority – podle něj se mod po stažení zařadí v sekci Optionals, stejně jako sloupec Priority v MO2: **větší číslo = v MO2 níž = vyšší priorita** (přepíše mody s menším číslem). Mod se dá hned pod poslední mod s menším nebo stejným číslem. Bez `priority` se použije číslo před názvem modu (`250- Addon`), a když ani to není, jde mod na konec sekce Optionals. |
| `url`, `version` | ne | Jen pro mody mimo Google Drive a repozitář: odkaz na archiv a verze (změna verze = nabídka aktualizace). |

Priorita se použije, když hráč mod stáhne přes launcher. Mody, které už má, launcher nepřesouvá.
Čísla nemusí jít po jedné – nech si mezi nimi mezery (100, 150, 200…), ať jde nový mod vložit mezi.

## Prázdná šablona záznamu

```json
{
  "name": "",
  "title": "",
  "author": "",
  "link": "",
  "category": "",
  "bundle": "",
  "image": "",
  "images": [],
  "gallery": "",
  "season": "",
  "group": "",
  "default": false,
  "description": "",
  "priority": 100
}
```

Celý soubor vypadá takto: `{ "mods": [ {…}, {…} ] }` – záznamy oddělené čárkou, za posledním čárka není.
Vzor s příklady je v `optional.example.json`.

## Balíček – příklad (3 mody, které musí jít spolu)

```json
{ "name": "[Party50] Modular Attachment System", "category": "Zbraně",
  "bundle": "Modular Attachment System", "priority": 271, "description": "Popis balíčku." },
{ "name": "[MsPizza727] Modular Attachment System BaS", "category": "Zbraně",
  "bundle": "Modular Attachment System", "priority": 272 },
{ "name": "[MsPizza727] Pizza's Ultimate Sight Selection for Anomaly", "category": "Zbraně",
  "bundle": "Modular Attachment System", "priority": 273 }
```

`name` musí odpovídat názvu archivu na Google Drive (bez `.7z`). Když se čísla priority v load
orderu změní, stačí je přepsat tady.

## Obrázky – příklad

```json
{ "name": "Jarní počasí", "season": "Jaro",
  "images": ["https://i.imgur.com/abc123.jpg", "https://drive.google.com/file/d/1AbC.../view"],
  "gallery": "https://imgur.com/a/xyz789" }
```

## Párování názvů

`name` nemusí přesně odpovídat názvu archivu na Drive: launcher najde archiv i bez ohledu na
číslo na začátku, autora, velikost písmen a HTML znaky (`Pizza&#39;s` = `Pizza's`). Když by
odpovídalo víc archivů, použije se jen přesná shoda.
