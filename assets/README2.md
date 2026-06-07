# frommygarage.co.uk — jak to działa

Struktura katalogów (wrzucasz całość na serwer pod domeną):

```
/index.html               → STRONA GŁÓWNA (witryna z kafelkami wszystkich rzeczy)
/assets/
    favicon.svg           → ikonka (wspólna dla wszystkich)
    favicon.ico           → DOROBIĆ (zob. niżej)
    apple-touch-icon.png  → DOROBIĆ (opcjonalnie, 180×180)
/metabo/
    index.html            → ogłoszenie (otwiera się jako frommygarage.co.uk/metabo/)
    /photos/
        photo1.webp       → ZDJĘCIE GŁÓWNE (idzie też na podgląd FB/WhatsApp)
        photo2.webp ... photo6.webp
```

## Strona główna (index.html)

Jasna, z drewnianymi akcentami. Pokazuje kafelki wszystkich rzeczy.
Edytujesz TYLKO jedną listę `ITEMS` na dole pliku (oznaczona dużym komentarzem).
Każdy przedmiot to jeden blok:

```js
{
  link:  "metabo",                       // nazwa folderu → /metabo/
  name:  "Metabo KS 254 Plus",
  blurb: "Jedno zdanie opisu",
  price: "£180 ono",
  thumb: "metabo/photos/photo1.webp",    // zwykle photo1 danego przedmiotu
  sold:  false                           // ustaw true gdy sprzedane → wstążka SOLD
}
```

- Dodanie rzeczy: skopiuj jeden blok `{ ... }`, zmień wartości. Pilnuj przecinków między blokami.
- Sprzedane: zmień `sold:false` na `sold:true` — kafelek zszarzeje i dostanie wstążkę SOLD
  (zostawiasz go dla "social proof", albo usuwasz blok).
- Brak zdjęcia: zostaw `thumb:""` — pokaże się "photo coming".

Usuń blok "More coming soon" gdy będziesz mieć realne przedmioty.

## Dodanie kolejnej rzeczy (np. wiertarka)

1. Skopiuj cały folder `metabo` → `wiertarka`.
2. W `wiertarka/index.html` edytuj TYLKO blok na górze oznaczony
   `EDIT THIS BLOCK FOR EACH ITEM` (tytuł, cena, og: tagi, URL),
   a niżej podmień treść (specyfikacja, stan).
3. Wrzuć zdjęcia do `wiertarka/photos/` jako photo1.webp, photo2.webp...
4. Gotowe — `frommygarage.co.uk/wiertarka/`

## Zdjęcia

- Nazwij je photo1...photo6 (.webp). Brakujące same się ukryją (JS to ogarnia),
  więc jak masz 3 zdjęcia, zostaw photo1–3, resztę linijek możesz usunąć.
- photo1 to zdjęcie główne ORAZ to które pokaże się w podglądzie na Facebooku/
  WhatsAppie (og:image), więc niech będzie najlepsze.
- Optymalny rozmiar: dłuższy bok ~1600 px, webp. Lekkie i ostre.

## Favicon .ico

SVG favicon wystarcza w nowoczesnych przeglądarkach. Dla starszych dorób .ico:
- wejdź na dowolny konwerter SVG→ICO, albo z linii poleceń (ImageMagick):
  `convert -background none favicon.svg -define icon:auto-resize=64,32,16 favicon.ico`

## Uwaga prawna (UK, sprzedaż prywatna)

Na dole każdej strony jest formuła "Private sale — sold as seen". To jednoznacznie
ustawia transakcję jako prywatną. Trzymaj opisy uczciwe (zgodne ze stanem) i jesteś
kryty. Nie dawaj danych Ltd ani regulaminów — to NIE jest sprzedaż firmowa.
