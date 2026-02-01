# H3 - Hello Web Server

## Käyttöympäristön tiedot
Tätä tehtävää suoritetaan käyttäen VirtualBoxia. Host-tietokoneena toimii pöytätietokone:

    Processor Intel(R) Core(TM) i7-6700K CPU @ 4.00GHz 4.00 GHz
    Installed RAM 16,0 GB
    Graphics Card NVIDIA GeForce RTX 3080 (10 GB)

## A - Webbipalvelimen vastaus
Webbipalvelin asennettiin tunnin aikana. Tunnilla asensimme Apache2:n ja asetimme uuden etusivun käyttäjähakemistoon. Tässä tehtävässä testaan, että tunnilla asennettu web palvelin toimii ja vastaa localhost -osoitteeseen.

![localhost](localhost.png)

- Palvelin vastaa onnistuneesti, ja näyttää muutetun etusivun.

## B - Loki
Seuraavaksi tarkastelen lokeja, jotka syntyvät kun sivun lataa. Tämän saa tehtyä helposti seuraavalla komennolla:

    sudo tail -f /var/log/apache2/arima_access.log

- arima_access.log on sivulleni konfiguroitu lokitiedosto, joka esittää kaikki HTTP-pyynnöt
- -f -lippu mahdollistaa sen, että uudet rivit tulostuvat heti kun ne syntyvät (kun uusia HTTP-pyyntöjä tehdään palvelimelle)

![webhost_logs](webhost_logs.png)

Tästä voidaan ottaa ensimäinen rivi, joka kertoo sivun latauksesta tapahtuneesta lokitapahtumasta:

    127.0.0.1 - - [01/Feb/2026:13:18:13 +0200] "GET / HTTP/1.1" 200 293 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0"

- 127.0.0.1 - Asiakkaan IP-osoite
- [01/Feb/2026:13:18:13 +0200] - Aikaleima ja aikavyöhyke (UTC+2, eli Suomen talviaika)
- "GET / HTTP/1.1" - HTTP-pyyntö, GET-metodi, juuripolkuun/etusivuun
-  200 - HTTP-tilakoodi. 200 tarkoittaa, että pyyntö onnistui.
-  293 - Vastauksen koko tavuina
-  "Mozilla/5.0..." - Kertoo käyttäjän selaimen ja käyttöjärjestelmän.

On huomioitava, että lokeissa näkyvä Favicon-pyynto sai 404 virheen. Tässä selain yrittää hakea sivukuvaketta, mutta sitä ei ole olemassa.
Lokeissa näkyvä 304 vastaus tarkoittaa, että selain kysyy onko sivu muuttunut, ja palvelin vastasi "ei ole", jolloin selain käyttää välimuistiaan sivun esittämisessä.

## C - Uusi virtuaalihosti
Tässä tehtävässä otan vanhan virtuaalihostin pois käytöstä, ja teen uuden tilalle. Uusi sivu on hattu.example.com, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p).

- Ensin tehdään uusi sivu komennolla:

    sudoedit /etc/apache2/sites-available/hattu.example.com.conf
