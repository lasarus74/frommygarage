# frommygarage.co.uk — dokumentacja projektu

Prywatna strona sprzedaży garażowej (UK, Dorking, Surrey RH4). Czysty statyczny
HTML + CSS + odrobina JS. Bez frameworków, bez backendu, bez bazy danych.
Wrzucasz pliki na serwer pod domeną i działa.

---

## STAŁE DANE (te same na każdej stronie — nie zmieniać bez powodu)

- **WhatsApp / telefon:** 07947 985 521  -> w linkach jako `447947985521`
- **Email:** martin@frommygarage.co.uk
- **Lokalizacja:** Dorking, Surrey, RH4
- **Domena:** https://frommygarage.co.uk
- **Język strony:** angielski (lang="en-GB"). Klient jest w UK.
- **Waluta:** funty (GBP). Wszystko w funtach.
- **Charakter sprzedaży:** PRYWATNA, "sold as seen". NIE firma, NIE sklep,
  bez regulaminów, bez danych Ltd. Każda strona ma na dole formułę
  "Private sale — used item sold as seen".

Te elementy są celowo identyczne na wszystkich podstronach (spójność marki):
sposób wyświetlania ceny (pulsująca, monospace, kolor --gold), przyciski
WhatsApp (zielony) i Email, paleta kolorów, font szeryfowy, galeria + lightbox.

---

## STRUKTURA KATALOGÓW

    /index.html                  -> STRONA GŁÓWNA (kafelki wszystkich przedmiotów)
    /assets/
        favicon.svg              -> ikonka (wspólna)
        favicon.ico              -> DOROBIĆ (zob. niżej)
        apple-touch-icon.png     -> DOROBIĆ (opcjonalnie, 180x180)
        social.webp              -> domyślny obrazek podglądu social
        og-image.psd             -> źródło (Photoshop) obrazka social
        README.md                -> TEN PLIK
    /.well-known/                -> dla certyfikatu SSL (Let's Encrypt). Nie ruszać.
    /metabo/                     -> PRODUKT 1: piła ukosowa Metabo
        index.html
        /photos/  photo1.webp ... photo6.webp
    /pompa/                      -> PRODUKT 2: pompa Stuart Turner
        index.html
        /photos/  photo1.webp ... photo6.webp   <- WŁAŚCICIEL WRZUCA SAM
    /papier/                     -> PRODUKT 3: rolki papieru ściernego Klingspor
        index.html
        /photos/  photo1.webp ... photo5.webp   <- WŁAŚCICIEL WRZUCA SAM

Pliki index2.html...index6.html oraz index.html_old w /metabo/ to STARE
WERSJE ROBOCZE z budowy strony — można je skasować, nie są nigdzie używane.

---

## AKTUALNE PRODUKTY (status)

| Folder  | Przedmiot                                  | Cena     | Dostawa                  | Sprzedane? |
|---------|--------------------------------------------|----------|--------------------------|------------|
| metabo  | Metabo KS 254 Plus (piła ukosowa 254mm)    | £180 ono | odbiór osobisty (~18kg)  | nie        |
| pompa   | Stuart Turner Showermate ECO S1.5 Twin     | £50      | odbiór LUB wysyłka £5    | nie        |
| papier  | Klingspor PS 30 D, 115×10m, zestaw 5 rolek | £25      | odbiór LUB wysyłka £5    | nie        |

---

## STRONA GŁÓWNA (index.html)

Pokazuje kafelki wszystkich przedmiotów. Edytujesz TYLKO jedną listę ITEMS
na dole pliku (oznaczona dużym komentarzem). Każdy przedmiot to jeden blok:

    {
      link:  "pompa",                        // nazwa folderu -> /pompa/
      name:  "Stuart Turner Showermate...",  // tytuł na kafelku
      blurb: "Jedno zdanie opisu",
      price: "£50",                          // np. "£180 ono", "£50"
      thumb: "pompa/photos/photo1.webp",     // zwykle photo1 danego przedmiotu
      sold:  false                           // true gdy sprzedane -> wstążka SOLD
    }

- **Dodanie rzeczy:** skopiuj jeden blok { ... }, zmień wartości.
  PILNUJ PRZECINKÓW między blokami (ostatni blok bez przecinka na końcu).
- **Sprzedane:** zmień sold:false na sold:true — kafelek zszarzeje
  i dostanie wstążkę SOLD (zostawiasz dla "social proof" albo usuwasz blok).
- **Brak zdjęcia:** zostaw thumb:"" — pokaże się "photo coming".

---

## DODANIE KOLEJNEJ RZECZY (instrukcja krok po kroku)

1. Skopiuj cały folder istniejącego produktu jako wzór:
   - przedmiot do WYSYŁKI (mały, lekki)  -> kopiuj `pompa`
   - przedmiot tylko do ODBIORU (duży, ciężki) -> kopiuj `metabo`
   Nazwij nowy folder krótko, bez spacji i polskich znaków (np. `wiertarka`).

2. W nowym index.html edytuj BLOK NA GÓRZE oznaczony
   `EDIT THIS BLOCK FOR EACH ITEM` — tytuł strony (<title>), opis,
   tagi og: (tytuł, opis, og:image -> photo1, og:url -> folder).

3. Niżej podmień treść: nagłówek <h1>, subtitle, badge, CENĘ
   w bloku .action, sekcje .section (opis, specyfikacja, stan)
   oraz blok .collection (dostawa/płatność).

4. Linki kontaktowe (WhatsApp wa.me/447947985521?text=... i
   mailto:martin@frommygarage.co.uk?subject=...) — zmień TYLKO tekst po
   text= / subject= na nazwę nowego przedmiotu (zostaw numer i adres).

5. Wrzuć zdjęcia do nowyfolder/photos/ jako photo1.webp ... photo6.webp.

6. Dodaj blok do ITEMS w głównym /index.html (zob. wyżej).

7. Gotowe — frommygarage.co.uk/nowyfolder/

---

## RÓŻNICA: ODBIÓR vs WYSYŁKA (ważne)

Szablon `metabo` jest "collection only" (piła ~18 kg, nie do wysyłki).
Szablon `pompa` dodaje opcję WYSYŁKI £5 — bo przedmiot jest mały.

W stronie z wysyłką (pompa) różnią się od metabo:
- price-note pod ceną: "collection or postage £5"
- zielony box .ship-note w sekcji "Quick facts" (małe = łatwo wysłać)
- blok .collection ma nagłówek "Postage & collection" i opisuje proces:
  kupujący pisze -> podaje adres -> sprzedawca generuje link PayPal lub
  podaje konto do przelewu -> wysyłka po zaksięgowaniu.

BEZ PRZYCISKÓW PŁATNOŚCI. To sprzedaż prywatna — wszystko ustalane
bezpośrednio przez WhatsApp/email. Żadnego checkoutu, koszyka, formularzy.

---

## ZDJĘCIA

- Nazwij photo1.webp ... photo6.webp. Brakujące same się ukryją
  (JS to ogarnia), więc jak masz 3 zdjęcia — zostaw photo1–3.
- photo1 = zdjęcie główne ORAZ podgląd na Facebooku/WhatsAppie
  (og:image) -> niech będzie najlepsze.
- Dla pompy warto, by jedno zdjęcie pokazywało TABLICZKĘ ZNAMIONOWĄ
  (serial, dane) — buduje zaufanie kupującego.
- Optymalny rozmiar: dłuższy bok ~1600 px, format webp. Lekkie i ostre.

---

## FAVICON .ico

SVG favicon wystarcza w nowoczesnych przeglądarkach. Dla starszych dorób .ico:
`convert -background none favicon.svg -define icon:auto-resize=64,32,16 favicon.ico`
(ImageMagick) albo dowolny konwerter SVG->ICO online.

Favicon ma motyw piły (tarcza). Jest wspólny dla całej strony jako logo
"garażu", więc nie trzeba go zmieniać per-produkt.

---

## UWAGA PRAWNA (UK, sprzedaż prywatna)

Na dole każdej strony jest formuła "Private sale — sold as seen". To
jednoznacznie ustawia transakcję jako prywatną. Trzymaj opisy uczciwe
(zgodne ze stanem) i jesteś kryty. Nie dawaj danych Ltd ani regulaminów —
to NIE jest sprzedaż firmowa.

---

## HISTORIA / NOTATKI

- Produkt 1 (metabo): piła ukosowa, odbiór osobisty, £180 ono.
- Produkt 2 (pompa): Stuart Turner Showermate ECO S1.5 Twin, Part No. 46502,
  rok 2018, serial 1823022-078. Pompa Twin (hot+cold naraz), positive head,
  przyłącza 15mm. Z tabliczki: 1.7 A, 385 W, 1.5 bar. Specyfikacja producenta
  (zweryfikowana online): max 1.5 bar przy zamkniętym zaworze, 1.1 bar @ 9 l/min,
  0.6 bar @ 18 l/min, max przepływ 32 l/min, max inlet head 10 m, WRAS/CE.
  Cena £50, wysyłka £5. Zdjęcia wrzuca właściciel (5 szt., w tym tabliczka).
  Wycena rynkowa używanej: realnie £50–85 wg ofert eBay UK; nowa £120–180.
- Produkt 3 (papier): Klingspor PS 30 D, format 115 mm × 10 m, zestaw 5 rolek
  (ziarna 60 / 80 / 100 / 120 / 180). Nowe, nieużywane — surplus ze sklepu
  MatMax (etykieta MATMAXshop). Ziarno: tlenek glinu (aluminium oxide), spoiwo
  żywiczne, podłoże D-weight (wytrzymałe + elastyczne), powłoka półotwarta
  (semi-open, mniej się klei przy farbie/szpachli). Zastosowanie: drewno,
  farba, lakier, szpachla, gips, metal; ręcznie i maszynowo. Cena £25 za cały
  zestaw, wysyłka £5. Kąt sprzedażowy: pojedyncza rolka ~£13 w handlu; komplet
  5 rolek nowych ~£60–65; tu wszystko za £25. Zdjęcia wrzuca właściciel (5 szt.).
