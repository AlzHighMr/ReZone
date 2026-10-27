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
| `category` | ne | Kategorie = tlačítko filtru na stránce Volitelné (`Addony`, `Zbraně`, `NPC Models`, `Gameplay`, `Questy`, `Audio`, `Ostatní` nebo vlastní; `Work in Progress` je vždy poslední). Kategorie **`Textury`** = texture pack na stránce TEXTURY (např. IXR Texture Rework). Kategorie **`Terén`** = textury terénu v sekci TERÉN nad texture packy – terén má **vždy přednost** v load orderu před texture packy i sezonami (launcher ho sám posune). Pro výběr jen jednoho terénu dej všem stejnou `group`. U modů z Drive se doplní sama podle složky, u modů z MO2 podle podsekce. |
| `season` | ne | `Jaro`, `Léto`, `Podzim` nebo `Zima` – mod patří na stránku SEZÓNY místo Volitelné. Nemusíš vyplňovat, když je mod pod separátorem sezóny nebo ve složce sezóny na Drive. Po stažení se zařadí pod separátor své sezóny (podle `priority`). |
| `group` | ne | U sezón: skupina variant. U volitelných modů a texture packů: **mody se stejnou skupinou se vylučují** (zapnutí jednoho vypne ostatní, např. `NPC Models`). U sezón: **skupina možností**, např. `Tráva` nebo `Počasí`. Z modů se stejnou sezónou a skupinou má hráč zapnutý vždy jen jeden (výběr kolečkem). Mody bez skupiny jdou zapnout/vypnout zaškrtnutím. |
| `default` | ne | Jen u sezón: `true` = doporučená možnost ve skupině, zapne se, dokud si hráč nevybere jinou. Bez `default` se vezme první mod ve skupině. |
| `bundle` | ne | **Balíček**: mody se stejným `bundle` se na stránce Volitelné ukážou jako jeden řádek (název = název balíčku), stahují se a zapínají/vypínají společně. Pořadí v load orderu určuje `priority` (bez ní pořadí záznamů v souboru). Popis stačí vyplnit u jednoho z modů. |
| `image` / `images` | ne | Obrázek / seznam obrázků do okna INFO (šipkami se přepíná). Přímý odkaz na obrázek (`.jpg`, `.png`, `.webp`), odkaz na soubor na Google Drive (`drive.google.com/file/d/…/view`, sdílený „kdokoli s odkazem“), Imgur (`imgur.com/ID`) nebo Dropbox. Funguje u volitelných modů i sezón. |
| `disables` | ne | Seznam modů, které se při **zapnutí** tohoto modu vypnou a po jeho **vypnutí** (nebo odinstalaci) zase zapnou. Název bez ohledu na číslo (`["[Isthar] Old Dog Sleeves Hand Pack"]`) **nebo číslo modu** v load orderu (`[214]` = mod „214-…“). |
| `after` | ne | Umístění v MO2: mod se po stažení dá **hned pod** tento mod (přepíše ho), např. `"[Isthar] Old Dog Sleeves Hand Pack"`. Název bez ohledu na číslo. |
| `section` | ne | Umístění v MO2: na konec sekce pod tímto separátorem, např. `"== NPC Models HERE! =="` (použije se, když `after` v load orderu není). |
| `gallery` | ne | Odkaz na celou galerii (album Imgur, složka Drive…), v INFO jako odkaz „Galerie“. |
| `description` | ne | Text v okně INFO. Nový řádek = `\n`. |
| `priority` | ne | **Číslo modu v load orderu modpacku** (jako „216-…“ před názvem složky). Po stažení se mod v MO2 dá hned pod mod s tímto číslem (přepíše ho), **zapne se** a po odinstalaci (tlačítko ODINSTALOVAT v INFO) se z load orderu zase odebere. Platí i pro členy balíčku (`bundle`). Bez `priority`: sezóny 216, texture packy 217, terén 218, zima 219; ostatní podle čísla před názvem modu, jinak konec sekce Optionals. |
| `optional` | ne | Jen u modů sezóny: `true` = jen nabídka, ve výchozím stavu vypnutý – stáhne se, až si ho hráč v sezóně zaškrtne (např. Project INVERNO). |
| `requires` | ne | Mody (hlavně patche), které se stáhnou a zapnou spolu s tímto modem a v load orderu jdou hned pod něj (přepíšou ho), např. `["Vasgen CCon Patch"]`. Když žádný mod, který je vyžaduje, není zapnutý, vypnou se. Archiv patche stačí dát do složky na Drive (třeba do složky sezóny). |
| `hidden` | ne | `true` = mod se v launcheru neukazuje (patch, který se instaluje jen přes `requires`). |
| `fomod` | ne | Volby instalátoru FOMOD – seznam názvů možností (stačí část názvu), např. `["2K", "Rotten Summer"]`. Launcher instalátor FOMOD projde sám: bez `fomod` vybere povinné a doporučené volby a ve skupinách „vyber jednu“ první možnost. Když instalátor projít nejde, archiv dá do MO2 (Downloads). |
| `file`, `size` | ne | Jen u modů z ModDB: přesný název archivu na ModDB (např. `ATO_5.7z`) a velikost v bajtech. Když ModDB launcheru stažení nepovolí, hráč archiv stáhne v prohlížeči do Stažených souborů a launcher ho tam podle `file` najde (stejně jako Anomaly). |
| `url`, `version` | ne | Jen pro mody mimo Google Drive a repozitář: odkaz na archiv a verze (změna verze = nabídka aktualizace). `url` může být i **odkaz na GitHub** (repozitář nebo release – stáhne se archiv z nejnovějšího releasu, aktualizace podle releasu) nebo **stránka addonu na ModDB** – launcher stáhne aktuální soubor a verzi hlídá sám (`version` netřeba). Mody s instalátorem (**FOMOD**) launcher nainstaluje sám (viz `fomod`). |

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

## Mody bez záznamu (vlastní odkazy hráčů)

Mod, který launcher najde na Google Drive (třeba z odkazu, který si hráč přidal v Nastavení), ale
v `optional.json` nemá popis ani `priority`, se po stažení dá pod separátor
**`== Custom addons HERE! ==`**. Hráč tak může stahovat vlastní addony bez úprav na GitHubu.
