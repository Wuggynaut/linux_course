# H7 - Maalisuora

## Käyttöympäristön tiedot
Tätä tehtävää suoritetaan käyttäen VirtualBoxia. Host-tietokoneena toimii pöytätietokone:

    Processor Intel(R) Core(TM) i7-6700K CPU @ 4.00GHz 4.00 GHz
    Installed RAM 16,0 GB
    Graphics Card NVIDIA GeForce RTX 3080 (10 GB)

## A - Hello World
Tässä tehtävässä kirjoitamme ja ajamme "Hello World" ohjelman kolmella eri ohjelmointikielellä. Valitsin ohjelmointikieliksi Python 3, Lua ja Bash.

### Python 3

- Ensin katsomme onko Python 3 asennettuna koneessa kokeilemalla komentoa

```
python3 --version
```

![python-version](python-version.png)

- Python on asennettuna koneeseen, joten voimme jatkaa kirjoittamaan ohjelmaa.
- Luomme uuden python tiedoston, ja kirjoitamme yksinkertaisen Hellow World ohjelman siihen.

```
micro helloworld.py
```

![python-code](python-code.png)

- Tallennuksen jälkeen ajetaan ohjelma:

```
python3 helloworld.py
```

![python-run](python-run.png)

### Lua

- Ensin asennamme Luan pakettimanagerista.

```
sudo apt-get install lua5.4
```

- Ja teemme lähes identtisen prosessin läpi:

```
micro helloworld.lua
```

![lua-code](lua-code.png)

```
lua helloworld.lua
```

![lua-run](lua-run.png)

### Bash

- Bashia ei luonnollisesti tarvitse erikseen asentaa.
- Käymme saman prosessin läpi.

```
micro helloworld.sh
```

![bash-code](bash-code.png)

```
bash helloworld.sh
```

![bash-run](bash-run.png)

## B - Tehtävien tarkastus
Tässä tehtävässä vain tarkastan kurssin aijemmat tehtävät, ja lisään mahdollisesti puuttuvat lähdeviitteet tms. Alla on linkki kaikkiin aijempiin raportteihin:

- [h1_oma_linux](h1_oma_linux.md)
- [h2_CMD](h2_CMD.md)
- [h3_hello_web_server](h3_Hello_Web_Server.md)
- [h4_pilvipalvelin](h4_pilvipalvelin.md)
- [h5_nimi](H5_nimi.md)
- [h6_salaus](h6_salaus.md)

## C - Shell skripti
Tässä tehtävässä luomme shell skriptin ja teemme siitä ajettavan kaikille käyttäjille.

- Luomme ensin skriptin

```
micro sysinfo.sh
```

![sysinfo-script](sysinfo-script.png)

**Selitykset skriptille**

```
#!/bin/bash
```

- Tämä on "Shebang" rivi. Se kertoo, että loppu skripti suoritetaan bashilla, ja osoitta missä se sijaitsee.

```
echo "=== System Info ==="
```

- Tämä printtaa vain tekstiä, koristelun vuoksi.

```
echo "Hostname: $(hostname)"
echo "User:     $(whoami)"
echo "Date:     $(date)"
echo "Uptime:   $(uptime -p)"
```

- Tässä skripti antaa erilaisia tietoja koneesta ajamalla erilaisia komentoja.
- Nämä komennot ovat "$(...)" syntaksin sisällä ja printtaavat komennon tulokset tuohon kohtaan tekstiä. Tätä kutsutaan nimellä "command substitution"
- Varsinaiset komennot ovat:
  - **hostname** - Printtaa koneen verkon hostnimen
  - **whoami** - Printtaa nykyisen käyttäjänimen
  - **date** - Printtaa päiväyksen
  - **uptime -p** - Printtaa kuinka kauan systeemi on ollut päällä. *-p* lippu tekee printistä luettavamman.

- Kun skriptin ajaa, palautus näyttää tältä:

```
bash sysinfo.sh
```

![script-output](script-output.png)

- Seuraavaksi teemme tästä ajettavan komennon.
- Teemme tämän kopioimalla sen /usr/local/bin/ kansioon ja asettamalla oikeudet.
- Poistamme myös .sh liitteen jottei sitä tarvitse kirjoittaa kun skriptiä ajetaan.

```
sudo cp sysinfo.sh /usr/local/bin/sysinfo
sudo chmod a+x /usr/local/bin/sysinfo
```

- Nyt testaamme, että kaikki toimii kirjoittamalla komennon terminaaliin.

```
sysinfo
```

![sysinfo](sysinfo.png)

## D - Laboratorio
Tässä tehtävässä teen jonkun aijemmista kurssin arvioitavista laboratorioista. Valitsin ict4tn021-3004 ti – alkukevät 2019 -kurssin laboratorion.

## Lähteet
- https://terokarvinen.com/linux-palvelimet/
- https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/
- https://terokarvinen.com/2007/12/04/shell-scripting-4/
- https://tldp.org/LDP/abs/html/index.html
- https://terokarvinen.com/2019/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-3004-ti-alkukevat-2019-5-op/?fromSearch=laboratorio
