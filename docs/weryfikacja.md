# Weryfikacja lokalna

Sprawdzono kod w Chromium, serwując katalog repozytorium przez `python3 -m http.server 8000 --bind 127.0.0.1`.

## Wyniki

- HTML5: parser `html5lib` w trybie ścisłym nie zgłosił błędów składni. Nie jest to pełny audyt zgodności HTML ani WCAG.
- Widoki: 1440 × 900, 1366 × 768, 768 × 1024, 390 × 844, 320 × 568 i 844 × 390.
- Brak przewijania poziomego we wszystkich sprawdzonych widokach. Komputer i laptop mieszczą stronę w jednym widoku; niski ekran poziomy przewija się pionowo.
- Dodatkowo sprawdzono brak poziomego przepełnienia po podwojeniu bazowego rozmiaru tekstu na komputerze.
- Nawigacja: dokładnie dwa wskazane adresy; dwa kolejne naciśnięcia Tab przenoszą focus na blog i Goodreads. Focus ma widoczny obrys. Pola linków mają wysokość 44 px.
- `prefers-reduced-motion: reduce` wyłącza przejście kolorów.
- Kontrast względem `#0b0b0d`: tekst główny 14,99:1, drugorzędny 8,05:1, stopka 5,99:1. Spełniają wymaganie 4,5:1 dla zwykłego tekstu.
- Tytuł, język polski, canonical, CNAME oraz `.nojekyll` sprawdzone. HTML, CSS i oryginalne logo są dostępne lokalnie.
- Nie wystąpiły błędy wykonania JavaScriptu; strona nie zawiera skryptów.

## Logo — ponowna weryfikacja

Pobrano `MD-logo.jpg` ze zdalnego commitu `859f473826f363f4cb08ab1671c722029b449e03` gałęzi `main`. Oryginał ma 940 × 1136 px i 69 159 bajtów. Zawartość pliku jest identyczna z wersją w Git; nie zmieniono proporcji, kadrowania ani obrazu.

Zaktualizowano ścieżkę obrazu w HTML oraz metadane Open Graph. Żądanie `MD-logo.jpg` zwraca HTTP 200; we wszystkich sześciu widokach `naturalWidth > 0`. Ponowione kontrole nie wykazały błędnych odpowiedzi HTTP dla zasobów strony ani błędów wykonania JavaScriptu. Obejrzano zrzuty ekranu komputera i telefonu: logo jest widoczne, zachowuje proporcje, a jego czarne tło integruje się z tłem strony. Poprzedni błąd 404 został usunięty. Opcjonalny favicon pominięto ze względu na szczegółowy, pionowy charakter obrazu.

Nie wykonano publikacji, zmian DNS, testów certyfikatu HTTPS ani dostępności zewnętrznych serwisów bloga i Goodreads. Zweryfikowano ich adresy w kodzie, nie działanie usług zewnętrznych. Automatyczne kontrole nie stanowią pełnego audytu WCAG 2.2 AA.
