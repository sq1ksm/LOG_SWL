# 📻 Broadcast DX Logger

Lokalny dziennik nasłuchów radiowych dla pasm **LW / MW / SW / FM** — działa w całości w przeglądarce, bez serwera i bez bazy danych. Wystarczy otworzyć plik HTML.

![Wersja](https://img.shields.io/badge/wersja-1.4-blue)
![Licencja](https://img.shields.io/badge/licencja-MIT-green)
![Bez zależności](https://img.shields.io/badge/zależności-brak-success)

---

## Funkcje

- Dodawanie wpisów z formularza (częstotliwość, stacja, QTH nadajnika, QTH odbiorcy, język, SINPO, odbiornik, antena, uwagi)
- Automatyczny **czas i data UTC** przy dodawaniu wpisu
- **Zapamiętywanie sprzętu i lokalizacji** (Odbiornik, Antena, QTH odbioru) w `localStorage` — nie musisz wpisywać ich przy każdym nasłuchu
- **Edytowanie wpisów bezpośrednio w tabeli** (klik → zmiana → Enter)
- Walidacja na bieżąco: SINPO (5 cyfr 1–5), częstotliwość, data, czas
- Status **QSL**: 🔴 brak / 🟡 wysłana / 🟢 otrzymana
- **Generowanie i drukowanie karty QSL** (w języku angielskim, format 14x9 cm)
- **Drukowanie naklejek QSL** (format 9x5 cm, bez zbędnych elementów)
- **Eksport / import CSV** (UTF-8 z BOM — otwiera się poprawnie w Excelu)
- Inteligentny import CSV z **łączeniem i deduplikacją** danych
- Wyszukiwanie na żywo we wszystkich polach
- Licznik wpisów i zegar UTC w nagłówku
- Responsywny layout (grid + auto-fit)
- Zero zależności — jeden plik HTML

---

## Szybki start

1. Pobierz plik `index.html` (oraz `help.html`, jeśli chcesz korzystać z przycisku *Pomoc*).
2. Otwórz `index.html` w dowolnej nowoczesnej przeglądarce (Chrome, Firefox, Edge, Safari).
3. Wypełnij formularz i kliknij **„Dodaj wpis”**.
4. Po sesji nasłuchowej kliknij **„Eksport CSV”** — to Twoja kopia zapasowa.

> 💡 Nie musisz nic instalować ani uruchamiać serwera — aplikacja działa w całości po stronie klienta.

---

## Opis interfejsu

### Formularz wpisu

| Pole | Opis |
|------|------|
| **Częstotliwość (kHz)** | Cyfry, opcjonalnie kropka lub przecinek (np. `6120`, `100.7`). **Wymagane.** |
| **Stacja** | Nazwa / identyfikator stacji. **Wymagane.** |
| **Miejsce nadawania (QTH nad.)** | Miejsce położenia masztu nadajnika (opcjonalne). |
| **Język** | Język audycji (opcjonalne). |
| **SINPO** | Dokładnie 5 cyfr od 1 do 5 (np. `45444`). **Wymagane.** |
| **Odbiornik** | Model odbiornika (opcjonalne, zapamiętywane). |
| **Antena** | Rodzaj / model anteny (opcjonalne, zapamiętywane). |
| **QTH odbioru** | Miejsce, z którego prowadzisz nasłuch (opcjonalne, zapamiętywane). |
| **Uwagi** | Opis odbioru, fading, zakłócenia, program, godziny (opcjonalne). |

Data i czas UTC dodawane są **automatycznie** w chwili dodania wpisu.

### Tabela wpisów

- Wpisy sortowane są **od najnowszego**.
- Kliknięcie komórki umożliwia edycję — zmiana zapisuje się po `Enter` lub kliknięciu poza pole.
- Błędne dane (np. litera w SINPO, zły format daty) zostaną odrzucone, a poprzednia poprawna wartość przywrócona.
- Przycisk **Info** otwiera podgląd wpisu, kartę QSL oraz opcje drukowania.

### Status QSL i Drukowanie

| Ikona | Znaczenie |
|-------|-----------|
| 🔴 | brak / nie wysłano |
| 🟡 | wysłana |
| 🟢 | otrzymana |

Po kliknięciu przycisku **Info** w tabeli, otwiera się okno ze szczegółami. Znajdziesz tam podgląd karty QSL oraz trzy przyciski drukujące:
1. **Drukuj samą QSL** – generuje standardową kartę 14x9 cm (w całości po angielsku, ze stopką "Report by SQ1KSM").
2. **Drukuj z uwagami** – drukuje kartę QSL, a pod nią Twoje prywatne notatki.
3. **Drukuj naklejkę** – generuje mniejszą wersję (9x5 cm) pozbawioną nagłówka i stopki, gotową do naklejenia na kopertę.

---

## Skala SINPO

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

## Format pliku CSV

Kolumny (w tej kolejności):
DataUTC, CzasUTC, Czestotliwosc, Stacja, QTH_Nadajnika, QTH_Odbiorcy, Jezyk, SINPO, QSL, Odbiornik, Antena, Uwagi

- Separator: przecinek
- Kodowanie: **UTF-8 z BOM** (poprawnie otwiera się w Excelu)
- Dozwolone wartości kolumny **QSL**: `(puste)`, `Wysłana`, `Otrzymana`
- Znaki `"` w polach tekstowych są podwajane (`""`) zgodnie ze standardem CSV
- Pierwszy wiersz to nagłówek — przy imporcie jest pomijany

✅ **Import łączy dane (nie nadpisuje).** Każdy wpis jest porównywany z istniejącymi (klucz: Data + Czas + Częstotliwość + Stacja). Nowe wpisy są dodawane, istniejące aktualizowane, a duplikaty pomijane. Obsługiwane są również starsze pliki 11-kolumnowe.

---

## Przechowywanie danych

Wszystkie dane przechowywane są w **`localStorage`** przeglądarki pod dwoma kluczami:
- `broadcastDXLog` – przechowuje wpisy z dziennika.
- `broadcastDXUstawienia` – przechowuje Odbiornik, Antenę i QTH odbioru (aby nie wpisywać ich za każdym razem).

**Konsekwencje:**

- Jedna przeglądarka = jeden log.
- Brak synchronizacji między urządzeniami.
- Wyczyszczenie danych przeglądarki, tryb prywatny lub zmiana urządzenia → **utrata logu**.
- **Regularnie eksportuj CSV** — to jedyna kopia zapasowa poza przeglądarką.

---

## Zalecenia praktyczne

1. **Eksportuj CSV** po każdej sesji nasłuchowej.
2. Przed importem CSV warto **zrobić kopię** aktualnego logu. Import co prawda domyślnie łączy dane, ale kopia chroni przed skutkami pomyłki (np. gdy plik CSV zawiera błędne dane).
3. Używaj spójnego formatu czasu UTC — ułatwia porównywanie wpisów z harmonogramami stacji.
4. W polu **Uwagi** zapisuj godziny rozpoczęcia i zakończenia audycji — pomaga przy weryfikacji QSL.

---

## Struktura projektu
.
├── index.html # główna aplikacja (cała logika + style + dane)
├── help.html # strona pomocy (otwierana przyciskiem „Pomoc”)
└── README.md # ten plik

Wszystko zawarte jest w pojedynczych plikach HTML — brak zależności, brak `node_modules`, brak build-stepu.

---

## Wsparcie przeglądarek

Aplikacja korzysta z:

- `localStorage`
- `Blob` / `URL.createObjectURL` (eksport)
- `FileReader` (import)
- `contenteditable` (edycja w tabeli)
- ES6+ (arrow functions, template literals, `padStart`, `forEach`)
- CSS Grid / Flexbox / `@media print`

Działa we wszystkich aktualnych wersjach Chrome, Firefox, Edge i Safari.

---

## Znane ograniczenia

- Dane trzymane są wyłącznie w `localStorage` — brak synchronizacji chmurowej.
- Brak automatycznej kopii zapasowej — tylko ręczny eksport CSV.

---

## Licencja

Projekt udostępniany na licencji **MIT** — możesz go swobodnie używać, modyfikować i rozpowszechniać.

Copyright © Sławek Kuchowicz (SQ1KSM)
