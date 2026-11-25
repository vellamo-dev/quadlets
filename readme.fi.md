# Quadlets

[English](readme.md) | Suomi

![Quadlets](./docs/img/quadlets-building.webp)

Valmiita Quadleteja [Podmanille](https://podman.io/) ja [PodShiftille](https://github.com/vellamo-dev/podshift).

Quadlet on pieni reseptitiedosto, joka kuvaa sovelluksen, taltion, verkon tai levykuvan. Quadletit ovat [Podmanin ominaisuus](https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html): Podman tekee jokaisesta tiedostosta systemd-palvelun, joten sovellus käynnistyy koneen käynnistyessä, käynnistyy tarvittaessa uudelleen ja sitä hallitaan kuten mitä tahansa muuta järjestelmän palvelua.

## Mitä projektissa on

Kokoelma Quadleteja, jotka voit ladata ja ottaa käyttöön. Kukin on yksittäinen tiedosto tai tiedostokansio, kun sovellus tarvitsee useita osia, esimerkiksi verkkosovellus omalla tietokannallaan.

- `catalog/apps/`: yksi kansio sovellusta kohden, jossa on kaikki sen tiedostot ja lyhyt `readme.md`.
- `catalog/singles/`: yksittäiset Quadletit tyypeittäin (`container`, `volume`, `network`, `image`).

## Käyttö PodShiftin kanssa

1. Asenna [PodShift](https://github.com/vellamo-dev/podshift) palvelimellesi.
2. Asenna [PodShift UI](https://github.com/vellamo-dev/cockpit-podshift), PodShiftin sivu [Cockpitiin](https://cockpit-project.org/).
3. Lataa tästä projektista Quadlet-tiedosto tai sovelluskansion tiedostot.
4. Avaa Cockpitissa **PodShift**, siirry **Drop Quadlet** -välilehdelle ja pudota tiedosto sivulle.

PodShift tarkistaa tiedoston, asentaa sen ja käynnistää sovelluksen. Saman välilehden **Drop History** ja **Install log** näyttävät, miten asennus etenee.

PodShift UI ottaa vastaan yhden tiedoston kerrallaan, enintään 50 kt: `.container`, `.volume`, `.network`, `.image` tai `.zip`.

## Käyttö Podmanin kanssa

Quadletit, joissa ei ole PodShift-muuttujia (katso alla), toimivat myös pelkän Podmanin kanssa. Sijoita ne Quadlet-kansioon, esimerkiksi käyttäjälle `~/.config/containers/systemd/`, ja lataa systemd uudelleen. Lisätietoja on [Podmanin Quadlet-dokumentaatiossa](https://docs.podman.io/en/latest/markdown/podman-systemd.unit.5.html).

## PodShift-muuttujat

Osa tämän projektin Quadleteista on tehty PodShiftille. Ne käyttävät PodShift-muuttujia, joiden nimet alkavat `TSV_`, arvoille, jotka vaihtelevat palvelimittain, kuten ympäristö (`TSV_ENV`, esimerkiksi `dev`, `staging` tai `prd`) tai palvelimen IP-osoitteet (`TSV_NW1`–`TSV_NW8`). PodShift korvaa ne palvelimen todellisilla arvoilla, kun se asentaa Quadletin.

Pelkkä Podman ei tunne näitä muuttujia. Osan niistä voi antaa *ympäristötiedostolla*, mutta Podman ei korvaa muuttujia Quadletissa joka kohdassa, joten näiden Quadletien käyttö ilman PodShiftiä on rajallista. PodShiftin tarjoamat muuttujat on kuvattu [PodShiftin laajuudessa](https://github.com/vellamo-dev/podshift/blob/main/docs/scope.md).

## Liittyvät projektit

| Projekti | Mikä se on |
|---|---|
| [Podman](https://podman.io/) | Konttimoottori, joka ajaa Quadletit. |
| [PodShift](https://github.com/vellamo-dev/podshift) | Muuttaa pienen palvelimen sellaiseksi, joka asentaa itsensä, pitää itsensä turvassa ja päivittää sovelluksesi automaattisesti. |
| [PodShift UI](https://github.com/vellamo-dev/cockpit-podshift) | Valinnainen PodShiftin Cockpit-sivu, jolla näet palvelimesi ja voit asentaa sovelluksia pudottamalla Quadleteja. |

## Lisenssi

AGPL-3.0-or-later; katso `LICENSE`.
