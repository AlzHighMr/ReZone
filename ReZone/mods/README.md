# mods/

Každá podsložka = jeden mod. Název složky musí **přesně** odpovídat názvu modu v Mod Organizeru 2
(včetně velkých písmen, mezer a hranatých závorek). Uvnitř stejná struktura jako v MO2:

```
mods/
└─ [Autor] Název modu/
   └─ gamedata/
      ├─ configs/…
      └─ scripts/…
```

* Aktualizují se jen soubory s příponami ze seznamu v launcheru (výchozí = všechny přípony Anomaly).
* Tento README launcher ignoruje (soubory přímo v `mods/` se nečtou).
