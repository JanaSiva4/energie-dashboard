# ⚡ Energie Dashboard
**Přehled spotřeby energií | Verze 2.0 | Duben 2026**

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-janasiva4.github.io%2Fenergie--dashboard-222?logo=github)](https://janasiva4.github.io/energie-dashboard)
[![GitHub](https://img.shields.io/badge/GitHub-JanaSiva4%2Fenergie--dashboard-181717?logo=github)](https://github.com/JanaSiva4/energie-dashboard)

---

## 📋 O projektu

Energie Dashboard je webová aplikace na GitHub Pages pro sledování měsíční spotřeby a nákladů za energie skladu CZLC4 (WEST I – Alza, Chrástany). Data se načítají z Google Sheets přes Apps Script webhook.

---

## ✅ Funkce

### 📊 Záložka Přehled
- Karty s poslední měsíční spotřebou — elektřina (Innogy), FSX, plyn, voda
- Graf spotřeby elektřiny a nákladů po měsících
- **📈 Trendy — meziroční změna** — náklady (Kč) a spotřeba elektřiny (kWh) napříč roky
- **📈 Trendy — energetický benchmarking** — průměrná cena elektřiny Kč/kWh (Innogy) v čase

### 📉 Záložka Grafy
- Podrobné grafy spotřeby a nákladů pro každou kategorii energie
- Elektřina (Innogy + FSX), plyn, voda — spotřeba i náklady zvlášť

### 📋 Záložka Historie
- Tabulka všech měsíčních odečtů
- Sloupce: elektřina, FSX, plyn, voda, celkem, 📦 SJL

### 📈 Záložka Predikce
- **OTE cena** — ruční zadání spot ceny z [OTE-CR.cz](https://www.ote-cr.cz/cs/kratkodobe-trhy/elektrina/den-dopredu), ukládá se do localStorage
- **Alert** — červené upozornění při ceně nad 2 500 Kč/MWh
- **SJL kalkulačka** — koeficient 0,069 kWh/SJL (průměr 2025–2026, 13 měsíců), automatické předvyplnění z posledního měsíce
- **Predikce 2027** — odhad ročních nákladů s +5% nárůstem, graf skutečnost vs. predikce

### ✏️ Záložka Zadání dat
- Formulář pro ruční zadání měsíčních hodnot
- Uložení přímo do Google Sheets přes Apps Script

---

## 🏗️ Architektura

```
GitHub Pages (index.html)
        ↓
Apps Script webhook (doGet / doPost)
        ↓
Google Sheets — záložka CZLC4
```

---

## 🛠️ Technický stack

| Komponenta | Popis |
|-----------|-------|
| Hosting | GitHub Pages |
| Frontend | HTML + CSS + Chart.js 4.4.1 |
| Font | Epilogue (Google Fonts) |
| Data | Google Sheets Apps Script webhook |
| OTE cena | Ruční zadání + localStorage |

---

## 📁 Struktura repozitáře

```
energie-dashboard/
├── index.html      # Celá aplikace — jeden soubor
└── README.md       # Tato dokumentace
```

---

## 🔗 Integrace — Google Sheets

**Apps Script URL:**
```
https://script.google.com/macros/s/AKfycbzfRP2cvMrwjbsCgQPzfbQsVABB68OYdpTPajGRT4hbhBbVWoGPJIJJTfMy6PbbhfTwCQ/exec
```

**Struktura záložky CZLC4 (sloupce A–R):**

| Sloupec | Index | Hodnota |
|---------|-------|---------|
| A | 0 | Rok |
| B | 1 | Měsíc |
| C | 2 | Elektřina spotřeba kWh |
| D | 3 | Elektřina Ø cena Kč/kWh |
| E | 4 | Elektřina silová el. Kč |
| F | 5 | Elektřina distribuce Kč |
| G | 6 | Elektřina celkem Kč |
| H | 7 | FSX spotřeba kWh |
| I | 8 | FSX Ø cena Kč/kWh |
| J | 9 | FSX celkem Kč |
| K | 10 | Plyn spotřeba kWh |
| L | 11 | Plyn Ø cena Kč/kWh |
| M | 12 | Plyn celkem Kč |
| N | 13 | Voda spotřeba m³ |
| O | 14 | Voda Ø cena Kč/m³ |
| P | 15 | Voda celkem Kč |
| R | 17 | SJL (Store Job Lines) |

---

## ⚠️ Známá omezení

- OTE cena — zadávána ručně jednou týdně z [OTE-CR.cz](https://www.ote-cr.cz/cs/kratkodobe-trhy/elektrina/den-dopredu) (BASE LOAD × 25 = Kč/MWh)
- CORS blokuje přímé načítání OTE dat z GitHub Pages — řešení: ENTSO-E token (čeká se)
- Aplikace nemá přihlášení — přístup má kdokoli s odkazem

---

## 🗺️ Plánovaný rozvoj

- ENTSO-E API — automatické načítání live cen OTE
- Více skladů — LCÚ, LCZ, SKLC3 (Apps Script záložky)
- Exporty do PDF/Excel

---

*Energie Dashboard · Jana Sivačenko · Facility CZLC4 · Duben 2026*
