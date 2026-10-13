> # NIEUŻYWANE, można usunąć
>
> **Stan na 13 października 2026.** To repozytorium nie obsługuje już żadnego
> ruchu i można je skasować bez konsekwencji.
>
> Przekierowanie `brzezińskifizjo.pl` na `brzezinskifizjo.pl` przejęła usługa
> **redirect.pizza**. Domena wskazuje teraz rekordem A na `89.106.200.1`,
> a nie na GitHub Pages, więc nic tutaj nie jest już odpytywane.
>
> Powód zmiany: GitHub Pages zawsze odpowiada kodem `200`, nawet dla strony,
> która wyłącznie przekierowuje. Google potraktowało adres z polskim znakiem
> jako zwykłą istniejącą stronę i go zaindeksowało. Potrzebne było prawdziwe
> serwerowe `301`, czego GitHub Pages nie potrafi — jedno repozytorium może
> mieć jedną domenę własną i zawsze serwuje treść, nie przekierowanie.
>
> Stan docelowy jest zweryfikowany: `301` po HTTP i HTTPS, ważny certyfikat
> Let's Encrypt, obsłużony również wariant `www`.
>
> Właściwa strona żyje w repozytorium **mati-fizjo**.
>
> Usunięcie wymaga zakresu `delete_repo` w tokenie `gh` albo zrobienia tego
> ręcznie w *Settings → General → Danger Zone*.

---

# Przekierowanie brzezińskifizjo.pl

Jedyne zadanie tego repozytorium: przekierować domenę z polskim znakiem
`brzezińskifizjo.pl` (w DNS: `xn--brzeziskifizjo-goc.pl`) na główną
domenę `brzezinskifizjo.pl`.

Właściwa strona żyje w repozytorium `mati-fizjo`.

## Dlaczego osobne repozytorium

GitHub Pages obsługuje jedną domenę własną na repozytorium, a wskazanie
drugiej domeny rekordami A na te same adresy daje 404, nie przekierowanie
(GitHub porównuje nagłówek `Host` z ustawioną domeną). Dlatego domena
z „ń" potrzebowała własnego Pages, które ją przywita i odeśle dalej.

## Jak to działało

`index.html` i `404.html` były identyczne. Skrypt w `<head>` przekierowywał
natychmiast, zachowując ścieżkę, parametry i kotwicę. `404.html` obsługiwał
wszystkie pozostałe adresy. `<meta http-equiv="refresh">` był zapasem dla
wyłączonego JavaScriptu, a widoczny przycisk ostatnią deską ratunku.

Słabością tego podejścia było to, że przekierowanie działo się w przeglądarce,
a serwer nadal zwracał `200`. Dla użytkownika różnicy nie było, dla Google
owszem — i to ona ostatecznie zdecydowała o przejściu na redirect.pizza.

## Wymagane wtedy rekordy DNS

Domena `brzezińskifizjo.pl` musiała wskazywać na GitHub Pages:

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
