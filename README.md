# Przekierowanie brzezińskifizjo.pl

Jedyne zadanie tego repozytorium: przekierować domenę z polskim znakiem
`brzezińskifizjo.pl` (w DNS: `xn--brzeziskifizjo-goc.pl`) na główną
domenę `brzezinskifizjo.pl`.

Właściwa strona żyje w repozytorium `mati-fizjo`.

## Dlaczego osobne repozytorium

GitHub Pages obsługuje jedną domenę własną na repozytorium, a wskazanie
drugiej domeny rekordami A na te same adresy daje 404, nie przekierowanie
(GitHub porównuje nagłówek `Host` z ustawioną domeną). Dlatego domena
z „ń" potrzebuje własnego Pages, które ją przywita i odeśle dalej.

## Jak to działa

`index.html` i `404.html` są identyczne. Skrypt w `<head>` przekierowuje
natychmiast, zachowując ścieżkę, parametry i kotwicę. `404.html` obsługuje
wszystkie pozostałe adresy, więc np. `/polityka-prywatnosci.html` trafi
pod właściwy adres na nowej domenie. `<meta http-equiv="refresh">` jest
zapasem dla wyłączonego JavaScriptu, a widoczny przycisk ostatnią deską
ratunku.

## Wymagane rekordy DNS

Domena `brzezińskifizjo.pl` musi wskazywać na GitHub Pages:

```
A     (host pusty)   185.199.108.153
A     (host pusty)   185.199.109.153
A     (host pusty)   185.199.110.153
A     (host pusty)   185.199.111.153
AAAA  (host pusty)   2606:50c0:8000::153
AAAA  (host pusty)   2606:50c0:8001::153
AAAA  (host pusty)   2606:50c0:8002::153
AAAA  (host pusty)   2606:50c0:8003::153
```
