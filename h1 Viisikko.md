# Tehtävä H1 Viisikko
## Lyhyet tiivistelmät artikkeleista.

### Install Salt On Debian 13 Trixie https://terokarvinen.com/install-salt-on-debian-13-trixie/
- Salt on konfiguraatiohallintaan tarkoitettu työkaly.
- Mahdollistaa lukuisien tietokoneiden yhteinäisen hallitsemisen ja sen avulla voi määritellä palvelimen tilan, sekä toteuttaa samoja muutoksia lukuisille tietokoneille.
- Salt-master ohjaa salt-minioneita -> Master antaa käskyt ja minionit toteuttaa, sekä antavat dataa takaisin.

### Run Salt Command Locally https://terokarvinen.com/2021/salt-run-command-locally/
- Salt komentoja voi ajaa paikallisesti ja tulokset näkee heti
- Tärkeimmät Saltin viisi tilafunktiota ovat `pkg`, `file`, `service`, `user` ja `cmd`
- Salttia käytetään normaalisti suurten tietokonejoukkojen ohjaamiseen internetin välityksellä

### Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/
- Orjakoneet voivat olla palomuurin tai NATin takana, taikka täysin tuntemattomassa osoitteessa ja silti niitä pystyy hallinnoimaan. Pelkästään Salt-masterin palvelimen töytyy olla julkinen ja tiedetty osoite.
- Mikäli salt-masterilla on palomuuri käytössä, tarvitsee se portit 4505/tcp ja 4506/tcp käyttöönsä, jos palomuuria ei ole sitä ei tarvitse huomioida.

### Raportin kirjoittaminen https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/
- Kirjoita raporttia koko ajan samalla kuin teet.
- Täsmällinen kertomus tekemästään, mitä tapahtui, miten ongelmat korjattiin...
- Lähdeviittaukset ovat todella tärkeitä, sekä raportin helppolukuisuus. Huolellinen kieliasu, väliotsikot!!!
  
### a) Debian 13-Trixie asennus. Hyödynsin tässä kohdassa seuraavaa youtube videota: https://www.youtube.com/watch?v=99yUVmLkqOk How To Install Debian 13-Trixie Through Virtual Box

<img width="320" height="493" alt="image" src="https://github.com/user-attachments/assets/cc5a5882-5dcc-4e3e-ae46-0b6a8e18762b" />

- Minulla oli aluksi ongelma, sillä en voinut suorittaa sudo komentoja terminaalissa, käyttäjäni ei ollut sudo kansiossa -> `su -` -> `usermod -aG sudo tommi` -> `su - tommi`. Nyt pystyin alkaa käyttämään sudoa.

**- !Huomiona! Joudun kuitenki aina kirjautumaan uudelleen `su - "käyttäjänimi"` eli aloittamaan uuden istunnon, jos suljen aikaisemman istunnon tai suljen virtuaalikoneen. Tämä jää selvitykseen.**

<img width="301" height="37" alt="image" src="https://github.com/user-attachments/assets/8f9081b5-92c7-40a3-9249-c070f2e12e09" />

- Ennen b) kohtaa suoritin terminaalissa `sudo apt update` `sudo apt upgrade` komennot. Aina ennen uutta ohjelmistoa asentaessa on tärkeää varmistaa uusimman pakettiversion käyttö.

### b) Salt (salt-minion) asentaminen Linuxille virtuaalikoneelle. https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html

<img width="400" height="220" alt="image" src="https://github.com/user-attachments/assets/9ef15f77-1f0a-4ad0-a9a8-ce5dafdb96c3" />

- Alkuun `sudo apt-get update` ja `sudo apt-get install wget`. Tämä mahdollistaa tiedostojen lataamisen verkosta.
- Sitten olikin aika ladata Salt Linuxille. Seurasin kyseisen sivun Salt install guidea, joka on linkattuna alaotsikossa.
- Loin keyrings hakemiston avaimille `mkdir -p /etc/apt/keyrings`, tämän jälkeen latasin julkisen avaimen pitkällä curl -fsSL komennolla. Kyseinen komento hakee tiedoston avaimen URL-osoitteesta ja tallentaa sen salt-archive-keyring.pgp tiedostoon root-oikeuksin.
<img width="600" height="270" alt="image" src="https://github.com/user-attachments/assets/97e053f9-fbf5-4904-ae3c-57c657118875" />


- Sitten lisäsin apt repon Saltille toisella pitkällä curl koodilla
<img width="450" height="311" alt="image" src="https://github.com/user-attachments/assets/ef3dfbfd-b0a8-4068-9caa-980d61a46654" />

- Ennen Salt mininonin asennusta ajoin komennon `sudo apt update` päivittääkseni metadatan
- <img width="923" height="148" alt="image" src="https://github.com/user-attachments/assets/75b7e347-b562-4a3e-81a6-9274e682e1a9" />
- Salt minionin asennus tapahtui `sudo apt-get install salt-minion`
<img width="1000" height="724" alt="image" src="https://github.com/user-attachments/assets/e1def32f-618a-4244-a6c0-499d46cdee3a" />
- Lopuksi tarkistin, että salt-minionin asennus oli onnistunut
- <img width="868" height="239" alt="image" src="https://github.com/user-attachments/assets/1158dafc-a4f9-4083-86f0-5a3290d19877" />
- Näyttää vihreältä, hyvä :)

### c) Viisi tärkeintä Saltin tilafunktiota


### d) Idempotentti?

## Raportissa hyödynnettyjä Lähteitä:
Sudo-oikeuksien ratkaisussa hyödynsin seuraavaa youtube videota: https://www.youtube.com/watch?v=nwNC8NF70WQ&pp=0gcJCQYKAYcqIYzv

Debian 13-Trixien asentaminen: https://www.debian.org/download

Tero Karvinen, Install Salt On Debian 13 Trixie: https://terokarvinen.com/install-salt-on-debian-13-trixie/

Tero Karvinen, Run Salt Command Locally: https://terokarvinen.com/2021/salt-run-command-locally/

Tero Karvinen, Salt Quickstart - SaltStack Master and Slave On Ubuntu Linux: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

Tero Karvinen, Raportin Kirjoittaminen: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

