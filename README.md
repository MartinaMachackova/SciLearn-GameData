# SciLearn GameData

Tento repozitář obsahuje texty a pokyny pro jednotlivé hry v aplikaci **Fast ForWord**.  
Doplněk **SciLearn Helper** je automaticky načítá – stačí zde upravit soubor `data.json`
a při příštím otevření panelu se změny projeví.

---

## Co je `data.json`?

Soubor `data.json` je seznam her. Každá hra obsahuje:

| Pole | Co to je |
|---|---|
| `name` | Název hry (zobrazí se v panelu) |
| `description` | Krátký popis hry |
| `vocabulary` | Seznam pojmů a jejich vysvětlení |
| `explanation` | Kroky – jak hra funguje (zobrazí se jako číslovaný seznam) |
| `tips` | Tipy pro žáka (každý tip na nový řádek) |

---

## Jak přidat nebo upravit hru

### Krok 1 – Otevři soubor `data.json`

Klikni na soubor **`data.json`** v seznamu souborů výše.

![Otevření data.json](https://i.imgur.com/placeholder.png)

---

### Krok 2 – Spusť editaci

Klikni na ikonu **tužky** (✏️) vpravo nahoře v souboru.

---

### Krok 3 – Uprav nebo přidej hru

Najdi správný modul (klíč jako `"reading"`) a v jeho části `"games"` přidej novou hru.

**Šablona pro novou hru:**

```json
"KLIC_HRY": {
  "name": "Název hry",
  "description": "Krátký popis, co hra trénuje.",
  "vocabulary": [
    { "word": "Pojem (anglicky)", "def": "Vysvětlení pojmu česky." },
    { "word": "Další pojem", "def": "Jeho vysvětlení." }
  ],
  "explanation": [
    "První krok – co žák udělá jako první.",
    "Druhý krok – co se stane dál.",
    "Třetí krok – jak hra reaguje na odpovědi."
  ],
  "tips": [
    "🎧 Tip číslo jedna.",
    "⏳ Tip číslo dva.",
    "💡 Tip číslo tři."
  ]
}
```

> **Co je `KLIC_HRY`?**  
> Je to kód hry z URL adresy. Když je hra otevřena, v adresním řádku prohlížeče
> uvidíš část jako `demo_exercise=GYMNE` – klíč je to slovo za `=` (zde `GYMNE`).

---

### Krok 4 – Ulož změny (Commit)

Po upravení souboru:

1. Sroluj dolů na stránce.
2. Uvidíš sekci **„Commit changes"**.
3. Do pole pro zprávu napiš stručně, co jsi změnil/a – například:  
   `Přidána hra SpeedRead do modulu reading`
4. Klikni na zelené tlačítko **„Commit changes"**.

> **Co je commit?**  
> Commit je jako „uložení + popis změny". GitHub si pamatuje historii
> všech změn, takže se vždy dá vrátit k dřívější verzi.
> Je to podobné, jako když Word nabízí „Sledování změn".

---

## Jak přidat celý nový modul

Moduly jsou skupiny her (např. „Čtení", „Fonika"). Aktuálně existuje modul `reading`.

Nový modul přidáš do části `"modules"` ve stejném stylu:

```json
"fonika": {
  "name": "Fonika a zvuky",
  "icon": "🔊",
  "games": {
    "PHNCS": {
      "name": "Phonics Hero",
      ...
    }
  }
}
```

---

## Struktura celého souboru (přehled)

```
data.json
├── modules
│   └── reading              ← název modulu (klíč)
│       ├── name             ← zobrazovaný název modulu
│       ├── icon             ← emoji ikona
│       └── games
│           ├── GYMNE        ← kód hry (= URL parametr demo_exercise)
│           └── PTTRN
└── default                  ← hra zobrazená, pokud kód hry není nalezen
```

---

## Časté otázky

**Kdy se změny projeví v doplňku?**  
Ihned po commitu. Doplněk načítá data vždy při otevření panelu (ne při načtení stránky).

**Co když udělám chybu v JSON?**  
Panel se nezobrazí a v konzoli prohlížeče bude chybová hláška. JSON je citlivý na
závorky a čárky – každý řádek kromě posledního v seznamu musí končit čárkou `,`.
Použij [jsonlint.com](https://jsonlint.com) pro ověření správnosti.

**Jak zjistím kód hry?**  
Otevři hru ve Fast ForWord, podívej se do adresního řádku a najdi část
`demo_exercise=XXXXX` – kód je `XXXXX`.
