# Re:Zone – soubory pro launcher

Repozitář, ze kterého Re:Zone Launcher čte changelog, popisy volitelných modů,
výchozí nastavení a průběžné aktualizace skriptů a configů.

Výchozí nastavení launcheru: vlastník `AlzHighMr`, repozitář `ReZone`, větev `main`.
Cesty jdou změnit v launcheru: Nastavení → Zdroje stahování → Zobrazit.

```
ReZone/
├─ changelog.md               okno CHANGELOG na stránce Domů
├─ optional.json              popisy volitelných modů (tlačítko INFO)
├─ optional.example.json      vzor – NEnahrávat jako optional.json
├─ optional.md                návod k polím v optional.json
├─ moddb.json                 kompatibilní addony z ModDB (stránka je zatím skrytá)
├─ defaults/
│  ├─ user.ltx                hlavní nastavení hry      → Anomaly\appdata\user.ltx
│  ├─ Rookie/axr_options.ltx  MCM pro profil Rookie     → mods\…Rookie Preset\gamedata\configs\
│  └─ Veteran/axr_options.ltx MCM pro profil Veteran    → mods\…Veteran Preset\gamedata\configs\
└─ mods/
   └─ <Přesný název modu v MO2>/gamedata/…   průběžné aktualizace modů
```

## Jak to funguje

| Soubor | Co launcher dělá |
|---|---|
| `changelog.md` | Zobrazí ho tak, jak je. Nejnovější verzi piš nahoru. |
| `optional.json` | Mody uvedené tady jsou **volitelné** (nenainstalují se samy) a dostanou název, autora, popis, kategorii a číslo priority. Návod v `optional.md`. |
| `defaults/…` | Při nové instalaci se použijí automaticky. Když soubor změníš, hráč dostane nabídku aktualizace s možností ponechat si své nastavení. V Nastavení jsou tlačítka pro obnovení. |
| `mods/<mod>/…` | Nainstalované mody se aktualizují soubor po souboru (jen změněné). Nová složka = nový mod, nainstaluje se a zapne. Soubory smazané tady se smažou i u hráčů. |

## Důležité

* Název složky v `mods/` musí **přesně** odpovídat názvu modu v Mod Organizeru.
* `axr_options.ltx` v presetech (`… Preset`) se přes `mods/` neaktualizuje – na to je `defaults/`.
* Velké soubory (textury, modely, zvuky) patří do patchů na Google Drive, ne sem.
  GitHub u velkého repozitáře nevrátí celý seznam souborů a launcher repozitář přeskočí.
* Repozitář musí být **veřejný** (jinak potřebuje token v nastavení launcheru).

## Archivy modpacku (Google Drive / GitHub Releases)

Nejsou v tomto repozitáři. Struktura hlavní složky na Google Drive:

```
Hlavní složka\        (Anomaly se stahuje jen z ModDB)
└─ ReZone\   ReZone.7z.001, .002, …
Patche\            <Přesný název modu>.7z
Volitelné mody\    <Název modu>.7z
NPC modely\        <Název modu>.7z
Zbraně\            <Název modu>.7z
Ostatní\           <Název modu>.7z
Jaro\ Léto\ Podzim\ Zima\   <Název modu>.7z   (mody sezón; odkazy v Nastavení → Zdroje)
```

Pro GitHub Releases použij samostatný repozitář (např. `ReZone-Files`), soubory < 2 GiB,
názvy stejné jako na Google Drive.
