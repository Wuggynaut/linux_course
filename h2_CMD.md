# H2 Komentaja Pingviini

Tätä tehtävää suoritetaan käyttäen VirtualBoxia.
Host-tietokoneena toimii pöytätietokone:
  Processor	Intel(R) Core(TM) i7-6700K CPU @ 4.00GHz   4.00 GHz
  Installed RAM	16,0 GB
  Graphics Card	NVIDIA GeForce RTX 3080 (10 GB)

## A - Micro
Tehtävänä on asentaa Micro tekstieditori.

- Terminaalissa kirjoitetaan komento
```sudo apt-get install micro```
- Tämä asensi Micron koneelle:

(micro-asennus)[micro-asennus.png]

- Testatakseni, että Micro on asentunut, käynnistän sen kirjoittamalla komennon

```micro```

- Micro lähtee käyntiin odotetusti:

(micro)[micro.png]

## B - Apt
Tehtävänä on asentaa kolme itselleni uutta komentoriviohjelmaa, ja kokeilla niitä.
Valitsemani ohjelmat on Crawl (tai dungeon-crawl-stone-soup, komentorivipohjainen-roguelike peli), htop (visuaalinen prosessienhallinta) ja ranger (tiedostonhallinta esikatseluilla).

- 18.35 Koetan asentaa nämä yhdellä komennolla:

```
sudo apt-get -y install crawl htop ranger
```

- Kaikesta päätellen asennus on onnistunut:

[kolmoisasennus](kolmoisasennus.png)

- 18.36 Koetan avata htopin komennolla

```htop```

- Ohjelma avautuu normaalisti ja näyttää meneillään olevat prosessit
- **Ongelma:** Ohjelman sulkukomento F10 avaakin terminaalin File-valikon:

[menu-ongelma](menu-ongelma.png)

- Lähdin etsimään ratkaisua oikotienäppäimistä. Erotiun F10 näppäimen terminaalin oikotienäppäimistä menemällä Edit -> Preferences -> Shortcut ja poistamalla näppäimen kohdasta 'Show Menubar Temporarily'. Tämä ei ole toiminto jolle nään muutenkaan hyötyä.

[shortcut-siivous](shortcut-siivous.png)

- Jostain syystä tämä ei lopettanut menun avaamista f10. Etsin vastausta xfce dokumentaatiosta, ja löysin toisen asetuksen, joka liittyy valikon oikotiehen. Tämä löytyy Edit -> Preferences -> Disable menu shortcut key.

[advanced-shortcut](advanced-shortcut.png)

- Tämä irroitti f10 toiminnot terminaaliohjelman hallusta, ja se toimi. Syy sille, miksi pelkkä oikotiennäppäimen poisto ei toiminut, tai sille, miksi tämä asetus löytyy käytännössä kahdesta eri paikasta, on minulle mysteeri.

- 19.00 Tästä selviydyttyäni kokeilen muita asentamiani ohjelmia. Seuraavaksi vuorossa on ranger. Avaan sen komennolla:

```ranger```

- Ranger avautui odotetusti, joskin tallennettuja tiedostoja ei kotihakemistossa tällä hetkellä ole:

[ranger](ranger.png)

- Rangerilla pääsen kuitenkin selaamaan vaikka /etc/ tiedostoja:

[ranger-etc](ranger-etc.png)

- 19.06 Viimeiseksi kokeilen crawlin toimivuutta:

```crawl```

- Tämä avaa odotetusti DCCS :n päävalikon:

[dccs-menu](dccs-menu.png)

- Peli käynnistyy normaalisti, ja aloitan uuden pelin luomalla Merfolk Transmuterin, nimeltään Teuvo:

[teuvo](teuvo.png)

# Lähteet

https://docs.xfce.org/apps/xfce4-terminal/preferences
https://terokarvinen.com/2020/command-line-basics-revisited
