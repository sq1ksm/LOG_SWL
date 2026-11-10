# 📻 Broadcast DX Logger

Lokalny dziennik nasłuchów radiowych dla pasm **LW / MW / SW / FM** — działa w całości w przeglądarce, bez serwera i bez bazy danych.

> ⚠️ **Ważne:** wszystkie dane przechowywane są wyłącznie w pamięci lokalnej przeglądarki (`localStorage`). Wyczyszczenie danych przeglądarki, tryb prywatny lub zmiana komputera spowodują utratę logu. **Regularnie rób eksport do pliku CSV!**

---

## Spis treści

1. [Do czego służy program](#1-do-czego-służy-program)
2. [Opis interfejsu](#2-opis-interfejsu)
3. [Dodawanie nowego nasłuchu](#3-dodawanie-nowego-nasłuchu)
4. [Skala SINPO](#4-skala-sinpo)
5. [Edycja wpisów w tabeli](#5-edycja-wpisów-w-tabeli)
6. [Podgląd uwag](#6-podgląd-uwag)
7. [Wyszukiwanie wpisów](#7-wyszukiwanie-wpisów)
8. [Eksport i import CSV](#8-eksport-i-import-csv)
9. [Usuwanie wpisów](#9-usuwanie-wpisów)
10. [Wskazówki i uwagi końcowe](#10-wskazówki-i-uwagi-końcowe)

---

## 1. Do czego służy program

**Broadcast DX Logger** to prosty dziennik nasłuchów stacji radiowych nadających w pasmach:

- **LW** — Long Wave (fale długie)
- **MW** — Medium Wave (fale średnie)
- **SW** — Short Wave (fale krótkie)
- **FM** — UKF

Program pozwala zapisywać szczegóły każdego nasłuchu: datę i czas w UTC, częstotliwość, nazwę stacji, kraj, język, ocenę jakości odbioru w skali SINPO, użyty odbiornik, antenę oraz dowolne uwagi. Wpisy można edytować, przeszukiwać, eksportować do pliku CSV oraz importować z powrotem.

> 💡 Czas każdego wpisu zapisywany jest automatycznie w standardzie **UTC** (uniwersalny czas koordynowany) — jest to standard przyjęty w nasłuchach DX.

---

## 2. Opis interfejsu

- **Zegar UTC** w prawym górnym rogu — pokazuje aktualny czas uniwersalny.
- **Licznik nasłuchów** — pokazuje liczbę zapisanych wpisów.
- **Formularz** — pola do wpisania danych nowego nasłuchu.
- **Przyciski operacji** — dodawanie, eksport, import, czyszczenie logu.
- **Pole wyszukiwania** — filtruje tabelę wpisów.
- **Tabela wpisów** — lista wszystkich nasłuchów, edytowalna bezpośrednio w komórkach.

---

## 3. Dodawanie nowego nasłuchu

Wypełnij formularz i kliknij przycisk **➕ Dodaj wpis**.

### Opis pól formularza

| Pole | Opis |
|---|---|
| **Pasmo** | Wybór z listy: `SW`, `MW`, `LW`, `FM`. |
| **Częstotliwość (kHz)** | Cyfry, opcjonalnie kropka lub przecinek dziesiętny. **Wymagany wpis.** |
| **Stacja** | Nazwa stacji lub jej identyfikator. **Wymagany wpis.** |
| **Kraj** | Kraj nadawania (opcjonalne). |
| **Język** | Język audycji (opcjonalne). |
| **SINPO** | Dokładnie 5 cyfr od 1 do 5 (np. `45444`). **Wymagany wpis.** |
| **Odbiornik** | Model odbiornika (opcjonalne). |
| **Antena** | Rodzaj użytej anteny (opcjonalne). |
| **Uwagi** | Dowolny opis: warunki propagacyjne, fading, zakłócenia, treść programu itp. |

> 💡 Data i czas UTC są dopisywane automatycznie w momencie kliknięcia **Dodaj wpis**.

---

## 4. Skala SINPO

SINPO to standardowa skala oceny jakości odbioru radiowego, używana w nasłuchach DX. Każda z pięciu cyfr oznacza ocenę w skali 1–5 (5 = najlepiej).

| Litera | Znaczenie | Ocena 1–5 |
|---|---|---|
| **S** | Siła sygnału (Signal strength) | 1 = bardzo słaby · 2 = słaby · 3 = dostateczny · 4 = dobry · 5 = bardzo silny |
| **I** | Zakłócenia (Interference) | 1 = bardzo silne · 2 = silne · 3 = umiarkowane · 4 = niewielkie · 5 = brak zakłóceń |
| **N** | Szumy (Noise) | 1 = bardzo silne · 2 = silne · 3 = średnie · 4 = niewielkie · 5 = brak szumów |
| **P** | Propagacja / zanikanie (Propagation) | 1 = bardzo silny fading · 2 = silny · 3 = umiarkowany · 4 = niewielki · 5 = brak zauważalnego fadingu |
| **O** | Ocena ogólna (Overall merit) | 1 = nieczytelny odbiór · 2 = bardzo słaby · 3 = zadowalający · 4 = dobry · 5 = doskonały odbiór |

### Przykłady

- `55555` — odbiór doskonały, jak z lokalnej stacji.
- `45444` — odbiór bardzo dobry, drobne zakłócenia.
- `33333` — odbiór przeciętny, słyszalny ale z trudem.
- `25232` — odbiór słaby, wyraźne zakłócenia i szumy.
- `15111` — ledwo słyszalny sygnał w morzu szumu.

---

## 5. Edycja wpisów w tabeli

Wszystkie komórki tabeli (poza kolumną *Operacje*) są **edytowalne bezpośrednio**. Wystarczy kliknąć w komórkę, zmienić wartość i kliknąć poza nią lub nacisnąć `Enter`.

Program automatycznie waliduje poprawność danych:

- **Data** — musi być w formacie `RRRR-MM-DD` i być prawdziwą datą.
- **Czas** — musi być w formacie `GG:MM:SS` (24h).
- **Pasmo** — tylko `SW`, `MW`, `LW` lub `FM` (wielkość liter nie ma znaczenia).
- **Częstotliwość** — tylko cyfry, opcjonalnie kropka lub przecinek.
- **SINPO** — dokładnie 5 cyfr z zakresu 1–5.

> 💡 Jeśli wprowadzisz niepoprawną wartość, program wyświetli komunikat i przywróci poprzednią zawartość komórki.

---

## 6. Podgląd uwag

Uwagi do wpisu (oraz pełne dane: odbiornik, antena, SINPO, data, czas, pasmo, częstotliwość) można obejrzeć klikając przycisk **📝 Uwagi** w kolumnie *Operacje*. Otwiera się okno z podglądem, które zamykasz przyciskiem **Zamknij**.

---

## 7. Wyszukiwanie wpisów

Pole **Szukaj...** filtruje tabelę na bieżąco podczas pisania. Wyszukiwanie obejmuje **wszystkie pola** wpisu (stacja, kraj, język, uwagi, częstotliwość itp.), bez rozróżniania wielkości liter.

### Przykłady

- `polska` — wpisy dotyczące polskich stacji, języka polskiego lub uwag zawierających to słowo.
- `6000` — wpisy z częstotliwością zawierającą 6000.
- `45444` — wpisy z konkretną oceną SINPO.

---

## 8. Eksport i import CSV

### Eksport

Kliknij **💾 Eksport CSV**, aby pobrać cały log jako plik `Broadcast_DX_Log.csv`.

- Plik zawiera BOM UTF-8, więc poprawnie otwiera się w Excelu i LibreOffice.
- Separator kolumn: przecinek. Tekst w cudzysłowach.
- Kolejność kolumn: `DataUTC, CzasUTC, Pasmo, Czestotliwosc, Stacja, Kraj, Jezyk, SINPO, Odbiornik, Antena, Uwagi`.

> ✅ **Zalecenie:** po każdej sesji nasłuchowej wykonaj eksport CSV. To jedyna skuteczna kopia zapasowa Twojego logu.

### Import

Kliknij **📂 Import CSV** i wybierz wcześniej wyeksportowany plik.

- Import **nadpisuje** cały aktualny log.
- Pierwszy wiersz traktowany jest jako nagłówek i pomijany.
- Wymagany układ kolumn taki, jak w eksporcie.

> ⚠️ Import zastępuje wszystkie aktualnie zapisane wpisy. Przed importem wykonaj eksport obecnego logu, jeśli chcesz go zachować.

---

## 9. Usuwanie wpisów

- **🗑 Usuń** przy pojedynczym wpisie — usuwa tylko ten jeden wiersz (po potwierdzeniu).
- **🗑 Usuń cały log** — czyści wszystkie wpisy z pamięci przeglądarki (po potwierdzeniu).

> ⚠️ Usuniętych wpisów **nie da się odzyskać**. Jeśli log jest dla Ciebie cenny, zrób eksport CSV przed operacją czyszczenia.

---

## 10. Wskazówki i uwagi końcowe

### Format czasu

Wszystkie czasy w logu zapisywane są w **UTC**. Nigdy nie zapisuj czasu lokalnego — utrudnia to porównywanie nasłuchów z innymi słuchaczami na świecie.

### Gdzie przechowywane są dane

Dane trzymane są w `localStorage` przeglądarki pod kluczem `broadcastDXLog`. Są one widoczne tylko w tej przeglądarce i na tym urządzeniu. Oznacza to m.in., że:

- Otwarcie pliku HTML w innej przeglądarce → pusty log.
- Tryb prywatny / incognito → dane giną po zamknięciu okna.
- Czyszczenie danych przeglądarki → utrata logu.
- Zmiana komputera → log nie przenosi się automatycznie.

### Backup

Najprostsza strategia bezpieczeństwa:

1. Po każdej sesji nasłuchowej: **Eksport CSV**.
2. Plik CSV trzymaj w chmurze lub na dysku zewnętrznym.
3. Przy nowym komputerze / przeglądarce: **Import CSV**.

### Zgodność z innymi logami

Układ kolumn CSV jest zgodny z typowymi arkuszami DX-owymi, więc plik można otworzyć w Excelu / LibreOffice Calc i dalej obrabiać (sortowanie, filtry, wykresy).

### Zakres pasm (orientacyjnie)

| Pasmo | Zakres | Uwagi |
|---|---|---|
| **LW** | 148,5 – 285 kHz | Fale długie, głównie Europa (obecnie w zaniku). |
| **MW** | 526,5 – 1606,5 kHz | Fale średnie, silne stacje lokalne i regionalne. |
| **SW** | 2,3 – 26,1 MHz | Fale krótkie, stacje międzykontynentalne, propagacja zależna od godzin. |
| **FM** | 87,5 – 108 MHz | UKF, zasięg przeważnie do 100 km (poza tropo i sporadykami E). |

---

✅ Powodzenia w nasłuchach i **73 de Sławek**!

---

*Broadcast DX Logger v0.9 · Copyright © Sławek Kuchowicz*
