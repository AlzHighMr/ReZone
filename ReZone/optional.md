# optional.json – popisy volitelných modů

Launcher bere volitelné mody ze tří míst a spojí je dohromady:

1. **Sekce `[====Optionals====]` v Mod Organizeru** (až po `== Custom addons HERE! ==`) – objeví se samy.
2. **Složky na Google Drive** (Volitelné mody, NPC modely, Zbraně, Ostatní) – dají se stáhnout.
3. **`optional.json`** – přidá jim název, autora, popis, kategorii a číslo priority.

Záznam v `optional.json` není povinný. Mod bez záznamu se zobrazí taky, jen bez popisu.

## Pole

| Pole | Povinné | Co dělá |
|---|---|---|
| `name` | ano | Název modu. Číslo na začátku (`123- `), autor v závorce a velká/malá písmena se při porovnání ignorují, takže `Better HUD` najde i `123- Better HUD (Ncenka)`. U modu z Google Drive napiš název archivu bez `.7z`. |
| `title` | ne | Název v launcheru. Prázdný = název modu bez čísla a autora. |
| `author` | ne | Autor, zobrazí se v okně INFO. Prázdný = z názvu modu `Mod (Autor)` nebo `[Autor] Mod`. |
| `link` | ne | Odkaz na stránku modu (ModDB, GitHub…), v okně INFO. |
| `category` | ne | Kategorie = tlačítko filtru na stránce Volitelné (`Addony`, `Zbraně`, `NPC modely`, `Ostatní` nebo vlastní). U modů z Drive se doplní sama podle složky, u modů z MO2 podle podsekce. |
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
  "description": "",
  "priority": 100
}
```

Celý soubor vypadá takto: `{ "mods": [ {…}, {…} ] }` – záznamy oddělené čárkou, za posledním čárka není.
Vzor s příklady je v `optional.example.json`.
