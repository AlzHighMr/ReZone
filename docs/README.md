# Re:Zone – příručka a databáze

Web modpacku Re:Zone pro S.T.A.L.K.E.R. Anomaly.

| Soubor | Obsah |
|---|---|
| `index.html` | Příručka: Informace, Instalace, Příručka, Databáze, Výroba |
| `testy.html` | Test questů trilogie (zamčeno heslem) |
| `changelog.html` | Changelog oprav trilogie (zamčeno vlastním heslem) |
| `preklad.html`, `tr/` | Editace překladu |
| `.nojekyll` | GitHub Pages soubory nijak neupravuje |

## Zveřejnění na GitHub Pages

1. Na GitHubu vytvoř nový repozitář, třeba `rezone`. Může být veřejný.
2. Nahraj do něj všechny soubory z této složky (**Add file › Upload files**). Soubor `.nojekyll` je skrytý, tak zkontroluj, že se nahrál taky.
3. Otevři **Settings › Pages**. U **Source** vyber **Deploy from a branch**, větev `main` a složku `/ (root)`, a klikni na **Save**.
4. Za minutu až dvě poběží web na `https://<tvuj-ucet>.github.io/rezone/`.

Aktualizace: nahraj nové verze souborů přes stejné jméno a GitHub web sám obnoví.

## Stránky pro testery

- Obsah `testy.html` a `changelog.html` je zašifrovaný (AES-256-GCM, klíč z hesla přes PBKDF2). Bez hesla se nedá přečíst ani ze zdrojového kódu stránky.
- Heslo se po zadání pamatuje v otevřené kartě, takže mezi Testem questů a Changelogem ho nezadáváš znovu. Se zaškrtnutým „Pamatovat si heslo“ zůstane uložené i potom. Tlačítko **Odhlásit** ho smaže.
- Šifrování funguje jen přes `https` (GitHub Pages ho má) nebo z lokálního souboru.
- Značky a poznámky se ukládají v prohlížeči každého testera. Sdílí se přes zprávy: tlačítko **Sdílet / vložit chyby** › **Kopírovat můj seznam** zkopíruje čitelný seznam chyb a na konci kód `RZTEST1:…`. Kdo celou zprávu vloží u sebe do pole **Vložit od jiného testera**, uvidí u questů ✓/✗ a poznámky toho testera. Novější seznam od stejného jména nahradí starší a vložené testery jde zase odebrat.
- Kdo heslo zná, může ho předat dál. Jako zámek proti náhodným návštěvníkům to stačí, jako ochrana tajných dat ne.
