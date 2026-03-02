# H6 - Salaus

Tässä tehtävässä suojaamme verkkosivumme HTTPS-yhteydellä.

## Käyttöympäristön tiedot
Tätä tehtävää suoritetaan käyttäen VirtualBoxia. Host-tietokoneena toimii pöytätietokone:

    Processor Intel(R) Core(TM) i7-6700K CPU @ 4.00GHz 4.00 GHz
    Installed RAM 16,0 GB
    Graphics Card NVIDIA GeForce RTX 3080 (10 GB)

## X - Let's Encrypt ja Apachen SSL/TLS-kofiguraatio
- Let's Encrypt voi antaa sivulle tarvittavan SSL/TLS-sertifikaatin.
- ACME-asiakas (*Automatic Certificate Management Environment*) todistaa sertifikaattiviranomaiselle, että palvelin hallitsee kyseistä domaini.
- Kun tämä on vahvistettu, asiakas voi pyytää sertifikaatin lähettämällä CSR-pyynnön, jonka viranomainen tarkistaa ja myöntää.

- Sertifikaatti otetaan käyttöön Apache-verkkopalvelimella konfiguraatiotiedostoilla ja direktiiveillä.
- HTTPS otetaan käyttöön, salaus vahvistetaan, sertifikaatin tila tarkistetus aktivoidaan (OCSP Stapling), ja pääsy rajoitetaan asiakassertifikaateilla.

## A - Sertifikaatin hankinta

- Ensitöiksemme otamme SSH-yhteyden palvelimeen, ja asennamme ACME-asiakkaan, Certbotin

```
ssh arima@81.27.96.169
sudo apt-get update
sudo apt-get install certbot
sudo apt-get install python3-certbot-apache
```

- Sitten hankimme ja asennamme sertifikaatin.

```
sudo certbot --apache -d arimattitoivonen.com -d www.arimattitoivonen.com
```

![sert-virhe](sert-virhe.png)

- Viestin mukaan sertifikaatti on hankittu oikein, mutta Apache-asennus epäonnistui.
- Avaamm HTTP-vhostin

```
sudo micro /etc/apache2/sites-available/arima.conf
```

![vhost-tarkistus](vhost-tarkistus.png)

- Täällä näemmekin, että näissä on väärä ServerName ja -Alias.
- Päivitämme sen:

![vhost-korjaus](vhost-korjaus.png)

- Testaamme vielä että sivu toimii:

```
sudo apache2ctl configtest
```

![configtest_onnistui](configtest_onnistui.png)

- "Syntax OK" eli onnistui.
- Sitten vielä käynnistämme serverin uudestaan ja asennamme sertifikaatin uudelleen.

```
sudo systemctl reload apache2
sudo certbot install --cert-name arimattitoivonen.com
```

# Lähteet
- https://certbot.eff.org/instruction
