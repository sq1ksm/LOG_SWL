# 📻 Broadcast DX Logger

Lokalny dziennik nasłuchów radiowych dla pasm **LW / MW / SW / FM** — działa w całości w przeglądarce, bez serwera i bez bazy danych. Wystarczy otworzyć plik HTML.

![Wersja](https://img.shields.io/badge/wersja-0.9-blue)
![Licencja](https://img.shields.io/badge/licencja-MIT-green)
![Bez zależności](https://img.shields.io/badge/zależności-brak-success)

---

## ✨ Funkcje

- ➕ Dodawanie wpisów z formularza (częstotliwość, stacja, kraj, język, SINPO, odbiornik, antena, uwagi)
- 🕒 Automatyczny **czas i data UTC** przy dodawaniu wpisu
- 🔄 **Edytowanie wpisów bezpośrednio w tabeli** (klik → zmiana → Enter)
- ✅ Walidacja na bieżąco: SINPO (5 cyfr 1–5), częstotliwość, data, czas
- 📮 Status **QSL**: 🔴 brak / 🟡 wysłana / 🟢 otrzymana
- 🔍 Wyszukiwanie na żywo we wszystkich polach
- 💾 **Eksport / import CSV** (UTF-8 z BOM — otwiera się poprawnie w Excelu)
- 📊 Licznik wpisów i zegar UTC w nagłówku
- 📱 Responsywny layout (grid + auto-fit)
- 🌐 Zero zależności — jeden plik HTML

---

## 🚀 Szybki start

1. Pobierz plik `index.html` (oraz `help.html`, jeśli chcesz korzystać z przycisku *Pomoc*).
2. Otwórz `index.html` w dowolnej nowoczesnej przeglądarce (Chrome, Firefox, Edge, Safari).
3. Wypełnij formularz i kliknij **„Dodaj wpis”**.
4. Po sesji nasłuchowej kliknij **„Eksport CSV”** — to Twoja kopia zapasowa.

> 💡 Nie musisz nic instalować ani uruchamiać serwera — aplikacja działa w całości po stronie klienta.

---

## 🧭 Opis interfejsu

### Formularz wpisu

| Pole | Opis |
|------|------|
| **Częstotliwość (kHz)** | Cyfry, opcjonalnie kropka lub przecinek (np. `6120`, `100.7`). **Wymagane.** |
| **Stacja** | Nazwa / identyfikator stacji. **Wymagane.** |
| **Kraj** | Kraj nadawania (opcjonalne). |
| **Język** | Język audycji (opcjonalne). |
| **SINPO** | Dokładnie 5 cyfr od 1 do 5 (np. `45444`). **Wymagane.** |
| **Odbiornik** | Model odbiornika (opcjonalne). |
| **Antena** | Rodzaj / model anteny (opcjonalne). |
| **Uwagi** | Opis odbioru, fading, zakłócenia, program, godziny (opcjonalne). |

Data i czas UTC dodawane są **automatycznie** w chwili dodania wpisu.

### Tabela wpisów

- Wpisy sortowane są **od najnowszego**.
- Kliknięcie komórki umożliwia edycję — zmiana zapisuje się po `Enter` lub kliknięciu poza pole.
- Błędne dane (np. litera w SINPO, zły format daty) zostaną odrzucone, a poprzednia poprawna wartość przywrócona.

### Status QSL

| Ikona | Znaczenie |
|-------|-----------|
| 🔴 | brak / nie wysłano |
| 🟡 | wysłana |
| 🟢 | otrzymana |

---

## 📐 Skala SINPO

**SINPO** to standardowa skala oceny odbioru używana przez DX-owców — pięć cyfr od 1 do 5:

| Litera | Znaczenie | Ocena 1–5 |
|--------|-----------|-----------|
| **S** | Siła sygnału *(Signal strength)* | 1 = bardzo słaby … 5 = bardzo silny |
| **I** | Zakłócenia *(Interference)* | 1 = bardzo silne … 5 = brak zakłóceń |
| **N** | Szumy *(Noise)* | 1 = bardzo silne … 5 = brak szumów |
| **P** | Propagacja / fading *(Propagation)* | 1 = bardzo silny fading … 5 = brak fadingu |
| **O** | Ocena ogólna *(Overall merit)* | 1 = nieczytelny … 5 = doskonały odbiór |

**Przykład:** `45444` — dobra siła sygnału, minimalne zakłócenia i szumy, brak zniekształceń, ogólnie dobry odbiór.

---

## 📁 Format pliku CSV

Kolumny (w tej kolejności):

```
DataUTC, CzasUTC, Czestotliwosc, Stacja, Kraj, Jezyk, SINPO, QSL, Odbiornik, Antena, Uwagi
```

- Separator: przecinek
- Kodowanie: **UTF-8 z BOM** (poprawnie otwiera się w Excelu)
- Dozwolone wartości kolumny **QSL**: `(puste)`, `Wysłana`, `Otrzymana`
- Znaki `"` w polach tekstowych są podwajane (`""`) zgodnie ze standardem CSV
- Pierwszy wiersz to nagłówek — przy imporcie jest pomijany

⚠️ **Import nadpisuje cały dotychczasowy log.** Przed importem zrób eksport aktualnych danych.

---

## 💾 Przechowywanie danych

Wszystkie dane przechowywane są w **`localStorage`** przeglądarki pod kluczem `broadcastDXLog`.

**Konsekwencje:**

- Jedna przeglądarka = jeden log.
- Brak synchronizacji między urządzeniami.
- Wyczyszczenie danych przeglądarki, tryb prywatny lub zmiana urządzenia → **utrata logu**.
- **Regularnie eksportuj CSV** — to jedyna kopia zapasowa poza przeglądarką.

---

## 📋 Zalecenia praktyczne

1. **Eksportuj CSV** po każdej sesji nasłuchowej.
2. Przed importem CSV **zrób kopię** aktualnego logu.
3. Używaj spójnego formatu czasu UTC — ułatwia porównywanie wpisów z harmonogramami stacji.
4. W polu **Uwagi** zapisuj godziny rozpoczęcia i zakończenia audycji — pomaga przy weryfikacji QSL.

---

## 🗂️ Struktura projektu

```
.
├── index.html   # główna aplikacja (cała logika + style + dane)
├── help.html    # strona pomocy (otwierana przyciskiem „Pomoc”)
└── README.md    # ten plik
```

Wszystko zawarte jest w pojedynczych plikach HTML — brak zależności, brak `node_modules`, brak build-stepu.

---

## 🧪 Wsparcie przeglądarek

Aplikacja korzysta z:

- `localStorage`
- `Blob` / `URL.createObjectURL` (eksport)
- `FileReader` (import)
- `contenteditable` (edycja w tabeli)
- ES6+ (arrow functions, template literals, `padStart`, `forEach`)

Działa we wszystkich aktualnych wersjach Chrome, Firefox, Edge i Safari.

---

## ⚠️ Znane ograniczenia

- Dane trzymane są wyłącznie w `localStorage` — brak synchronizacji chmurowej.
- Brak automatycznej kopii zapasowej — tylko ręczny eksport CSV.
- Kolejność w tabeli zależy od daty i czasu UTC wpisanych w wierszu — ręczna zmiana tych pól zmienia sortowanie.

---

## 📜 Licencja

Projekt udostępniany na licencji **MIT** — możesz go swobodnie używać, modyfikować i rozpowszechniać.

Copyright © Sławek Kuchowicz
