# Maria Dunkel

Minimalistyczna, statyczna wizytówka literacka dla domeny **mariadunkel.art**. HTML i CSS, systemowe fonty, bez JavaScriptu, bibliotek, trackerów i procesu budowania.

Oryginalne logo `MD-logo.jpg` zostało pobrane z gałęzi `main` i podłączone bez zmiany zawartości ani proporcji. Publikacja i zmiany DNS nie zostały wykonane.

## Pliki

```text
index.html                  treść, linki i metadane
assets/css/style.css        wygląd i responsywność
MD-logo.jpg                 oryginalne logo autorskie
CNAME                       domena docelowa
.nojekyll                   wyłączenie Jekylla
docs/weryfikacja.md          wyniki kontroli
```

## Podgląd lokalny

W katalogu repozytorium uruchom:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Otwórz stronę serwowaną przez ten proces w lokalnej przeglądarce. Zatrzymanie: Ctrl+C. Instalacja zależności nie jest potrzebna. Serwer Pythona służy wyłącznie do pracy lokalnej.

## Logo i favicon

Podmień `MD-logo.jpg`, zachowując nazwę, albo zmień `src` obrazu w `index.html`. Nie zmieniaj proporcji ani zawartości oryginału. Ustaw `width` i `height` zgodnie z rzeczywistymi wymiarami; obecny plik ma 940 × 1136 px. Przy zmianie nazwy lub wymiarów zaktualizuj również metadane `og:image`, `og:image:width` i `og:image:height`. CSS skaluje proporcjonalnie; `mix-blend-mode: lighten` integruje czerń obrazu z tłem bez edycji pliku. Po podmianie sprawdź efekt na ekranie telefonu i komputera.

Opcjonalny favicon przygotuj z oryginału bez kadrowania i rozciągania: dopasuj cały obraz do kwadratowego płótna z czarnym marginesem. Zapisz lokalny PNG i dodaj w `head` np. `<link rel="icon" type="image/png" href="assets/images/favicon.png">`. Przy małych rozmiarach sprawdź czytelność — można zrezygnować z faviconu. Obecnie favicon pominięto; logo jest szczegółowym, pionowym obrazem. Metadane Open Graph korzystają z oryginalnego logo.

## Linki

Adresy AKTUALNOŚCI i GOODREADS zmienisz w atrybutach `href` w `index.html`. Prowadzą obecnie bezpośrednio do bloga i profilu autorskiego wskazanych w wymaganiach. Otwierają się w tej samej karcie.

Aby dodać Patronite, wstaw do listy `author__links` kolejny element, podając prawdziwy adres profilu:

```html
<li><a href="TU_WSTAW_DOKŁADNY_ADRES_PROFILU">Patronite</a></li>
```

Separatory i układ są nadawane automatycznie przez CSS. Obecnie Patronite nie jest widoczny. Stopka ma celowo stały rok 2026; jej tekst można zmienić w HTML.

## Publikacja na GitHub Pages

1. Sprawdź stronę lokalnie. Zatwierdź pliki oraz wyślij je do gałęzi `main` repozytorium `landing-page` dopiero po decyzji o publikacji.
2. W repozytorium otwórz **Settings → Pages → Build and deployment**. Wybierz **Deploy from a branch**, gałąź `main` i katalog **/(root)**, następnie zapisz. Repozytorium publiczne obsługuje bezpłatny GitHub Pages; prywatne może wymagać odpowiedniego planu.
3. W **Custom domain** wpisz `mariadunkel.art`. Plik `CNAME` zawiera tę samą domenę. Sprawdź wynik wdrożenia w GitHub Actions/Pages.
4. Skonfiguruj DNS według instrukcji poniżej i włącz HTTPS po uzyskaniu certyfikatu.

To zwykłe repozytorium projektowe. Względne ścieżki `assets/...` działają także przy podglądzie pod `/landing-page/`. Canonical wskazuje celowo domenę produkcyjną. Domena i publiczny podgląd GitHub nie będą działać, dopóki samodzielnie nie opublikujesz strony i nie skonfigurujesz DNS.

## Domena w WordPress.com — zachowaj Bloggera

**Nie zmieniaj serwerów nazw. Nie usuwaj wszystkich rekordów. Nie modyfikuj rekordów `blog.mariadunkel.art` ani rekordów weryfikacji Bloggera.**

1. W WordPress.com przejdź do zarządzania domenami, wybierz `mariadunkel.art`, następnie rekordy DNS (nazwy pozycji panelu mogą się zmieniać). Najpierw zapisz kopię wszystkich rekordów.
2. Sprawdź istniejące rekordy dla domeny głównej (`@`, czasem pole puste). Usuń lub zastąp tylko kolidujące rekordy A/AAAA/ALIAS/ANAME domeny głównej i ewentualne przekierowanie tej domeny. Zachowaj MX, TXT, rekordy pocztowe, weryfikacyjne oraz wszystkie rekordy Bloggera. Nie dodawaj CNAME na poziomie `@`.
3. Ustaw cztery rekordy **A** dla `@`:

   | Typ | Nazwa | Wartość |
   | --- | --- | --- |
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |

4. IPv6 jest opcjonalne. Jeśli chcesz je obsługiwać, ustaw cztery **AAAA** dla `@`: `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`. Nie pozostawiaj starych AAAA wskazujących inny hosting, ponieważ część odwiedzających trafi na niewłaściwy serwer.
5. Opcjonalnie dla `www` dodaj CNAME wskazujący na `cerralke.github.io` — **bez** `/landing-page`. Zrób to wyłącznie po sprawdzeniu istniejącego rekordu `www`. Nie zmieniaj `blog`.
6. Zalecane: zweryfikuj własność domeny w ustawieniach GitHub Pages konta. Dodaj dokładnie wygenerowany przez GitHub rekord TXT `_github-pages-challenge-…`; nie wymyślaj jego wartości. Pozostaw go po weryfikacji. Unikaj wildcardów DNS.
7. Poczekaj na propagację DNS (może potrwać do 24 godzin). W **Settings → Pages** sprawdź **DNS check** i po wystawieniu certyfikatu zaznacz **Enforce HTTPS**. Jeśli certyfikat nie powstaje, sprawdź kolidujące rekordy i ewentualne CAA; GitHub korzysta z Let's Encrypt. Nie usuwaj CAA w ciemno.
8. Sprawdź `https://mariadunkel.art/`, oba linki oraz osobno `https://blog.mariadunkel.art`. Blog musi nadal działać na Bloggerze.

Przed zmianami sprawdź aktualną dokumentację usług:

- [GitHub: domena niestandardowa](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
- [GitHub: HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)
- [WordPress.com: rekordy DNS](https://wordpress.com/support/domains/custom-dns/)

Żadne zmiany DNS ani publikacja nie są wykonywane przez ten projekt automatycznie.
