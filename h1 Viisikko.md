# Tehtävä H1 Viisikko
## Lyhyet tiivistelmät artikkeleista.

### Install Salt On Debian 13 Trixie. https://terokarvinen.com/install-salt-on-debian-13-trixie/
- Salt on konfiguraatiohallintaan tarkoitettu työkaly.
- Mahdollistaa lukuisien tietokoneiden yhteinäisen hallitsemisen ja sen avulla voi määritellä palvelimen tilan, sekä toteuttaa samoja muutoksia lukuisille tietokoneille.
- Salt-master ohjaa salt-minioneita -> Master antaa käskyt ja minionit toteuttaa, sekä antavat dataa takaisin.

### Run Salt Command Locally. https://terokarvinen.com/2021/salt-run-command-locally/
- Salt komentoja voi ajaa paikallisesti ja tulokset näkee heti
- Tärkeimmät Saltin viisi tilafunktiota ovat `pkg`, `file`, `service`, `user` ja `cmd`
- Salttia käytetään normaalisti suurten tietokonejoukkojen ohjaamiseen internetin välityksellä

### Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux. https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/
- Orjakoneet voivat olla palomuurin tai NATin takana, taikka täysin tuntemattomassa osoitteessa ja silti niitä pystyy hallinnoimaan. Pelkästään Salt-masterin palvelimen töytyy olla julkinen ja tiedetty osoite.
- Mikäli salt-masterilla on palomuuri käytössä, tarvitsee se portit 4505/tcp ja 4506/tcp käyttöönsä, jos palomuuria ei ole sitä ei tarvitse huomioida.

### Raportin kirjoittaminen. https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/
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
<img width="868" height="239" alt="image" src="https://github.com/user-attachments/assets/1158dafc-a4f9-4083-86f0-5a3290d19877" />
- Näyttää vihreältä, hyvä :)

### c) Viisi tärkeintä Saltin tilafunktiota.
#### 1. PKG. 
<img width="601" height="438" alt="image" src="https://github.com/user-attachments/assets/784ac9ca-934b-4207-9841-0cc21c37877c" />

- Ajoin komennon `sudo salt-call --local -l info state.single pkg.installed tree`, joka asensi tree paketin koneeseeni.
- Kyseinen tuloste kertoo, että paketti asennettiin onnistuneesti, ilman virheitä.
- `ID` = Mitä asennettiin, `Function` = pkg.installed eli paketti asennettiin, `Result` kuvaa asennuksen onnistumista, `Comment` kuvailee mitä muutoksia tapahtunut, `Started` ja `Duration` kuvaa asennuksen ajankohtaa ja -kulkua, sekä kuinka kauan asennuksessa kesti, `Changes` kuvailee muutoksia, kuvasta voidaan päätellä, että tree - pakettia ei ollut aiemmin asennettu, asennettu versio on 2.2.1-1, kesto 4,454 sekunttia, asennus sujui ilman virheitä.

<img width="526" height="417" alt="image" src="https://github.com/user-attachments/assets/7a3f8e76-1168-48ba-af82-71366506b174" />

- Komento `sudo salt-call --local -l info state.single pkg.removed tree`, poistaa Tree - paketin onnistuneesti ja kertoo samat tiedot.
- Huomataan, että versionumero siirtyy kohtaan `Old`, joka kuvaa aiemmin asennettua pakettia ja `Function` kohta kertoo, että paketti poistettiin.

#### 2. File.
<img width="454" height="387" alt="image" src="https://github.com/user-attachments/assets/ab078bd1-0860-41d9-84d9-366a1a052124" />

- Komento `sudo salt-call --local -l info state.single file.managed /tmp/hellotommi` varmistaa, kyseisen tiedoston olemassa olon tai luo tiedoston paikallisesti koneeseen "hellotommi" `/tmp` kansiopolkuun. Komento toimii ikään kuin `touch`-komento.
- `Changes` kohdasta huomataan, että juuri uusi kyseinen tiedosto on luotu ja `Comment` kenttä kertoo, että luotu tiedosto on tyhjä.
- Tulostuksesta huomataan kaikki samat asiat, kuin `PKG` kohdasta.

<img width="959" height="504" alt="image" src="https://github.com/user-attachments/assets/d1a69056-448d-4c0e-ad05-f370b622295f" />

- Seuraavaksi kokeilin komentoa `sudo salt-call --local -l info state.single file.managed /tmp/moitommi contents="foo"`, joka varmistaa tiedoston olemassa olon tai luo sen, mikäli se ei ole olemassa.
- `Contents="foo"` luo tiedostoon sisällön "foo".
- `Diff`kohta näyttää nyt "New File", joka kertoo että uusi tiedosto luotiin.

<img width="405" height="361" alt="image" src="https://github.com/user-attachments/assets/b562f819-aa67-4ccc-8dea-4d91084f49bc" />

- Lopuksi kokeilin tiedoston "hellotommI" poistamista `absent` komennon avulla, `sudo salt-call --local -l info state.single file.absent /tmp/hellotommi`
- `Changes`kohta kertoo, että tiedosto poistettiin.

#### 3. Service.
<img width="911" height="528" alt="image" src="https://github.com/user-attachments/assets/75e4f73b-d462-4ece-8b2d-56bfaa8b6692" />

- `sudo salt-call --local -l info state.single service.running apache2 enable=True` komento kertoo, että apache2 ohjelmisto on päällä ja varmistaa sen toiminnan.
- Huomataan, että palvelu oli jo käytössä Debianissani, sekä `Changes` kohta näyttää tyhjää = mitään muutosta ei tapahtunut.

- Seuraavaksi kokeilin apache2 ohjelmiston pysäyttämistä = `state.single service.dead apache2 enable=False.

<img width="587" height="390" alt="image" src="https://github.com/user-attachments/assets/5ff8ef00-87f4-44cc-9f9d-50ca9ec9d884" />

- Tulostuksesta huomataan, että Salt varmistaa apachen pysäyttämisen, sekä nyt `Changes`kohta on "True", mistä voidaan päätellä että muutoksia tehtiin onnistuneesti.

#### 4. Cmd.
Komento: `sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"`

<img width="1026" height="559" alt="image" src="https://github.com/user-attachments/assets/03ad3709-20a2-4cd1-b8ec-9e4f6ebf722f" />

- Tässä kohdassa Salt suorittaa `touch` - komennon ja luo tyhjän kansion, mikäli sitä ei ole olemassa.
- Tyhjän kansion luominen onnistui ilman virheitä.

#### 5. User.
- Käyttäjän luominen Saltin avulla.

<img width="548" height="666" alt="image" src="https://github.com/user-attachments/assets/479b7efa-8270-4ae1-9e76-06a788db27db" />

- Huomataan, että `user.present` komento luo halutun käyttäjän, kotihakemiston ja ryhmän.
- Passwd: x = Salasana on piilossa, tai tässä tilanteessa en määrittänyt käyttäjälle salasanaa.

- Lopulta poistin käyttäjän `user.absent` komennon avulla
- `sudo salt-call --local -l info state.single user.absent tomppa32`

<img width="429" height="400" alt="image" src="https://github.com/user-attachments/assets/713a3e00-caec-4a9a-b38f-f912ce92d146" />

- Huomataan, että käyttäjäkohtainen ryhmä ja käyttäjä poistettiin onnistuneesti.

### d) Idempotentti?
- Kuvailee ohjelmiston ominaisuutta, missä samat ja useasti suoritetut komennot / toimenpiteet eivät tee muutosta.
- Otetaan esimerkiksi tree pkg.installed tilanne.
<img width="603" height="386" alt="image" src="https://github.com/user-attachments/assets/5aa4d815-9f16-4932-be5e-109079bfabf3" />

- Tree - asennettu, changes = 1. Sitten suoritetaan sama asennus komento uusiksi.

<img width="530" height="335" alt="image" src="https://github.com/user-attachments/assets/8edacd44-647b-44b3-a72a-0021818f2c77" />

- Huomataan, että kommentti kentässä "All specified... already installed. Changes = 0, muutoksia ei siis tapahtunut.

## Raportissa hyödynnettyjä Lähteitä:
Sudo-oikeuksien ratkaisussa hyödynsin seuraavaa youtube videota: https://www.youtube.com/watch?v=nwNC8NF70WQ&pp=0gcJCQYKAYcqIYzv

Debian 13-Trixien asentaminen: https://www.debian.org/download

Tero Karvinen, Install Salt On Debian 13 Trixie: https://terokarvinen.com/install-salt-on-debian-13-trixie/

Tero Karvinen, Run Salt Command Locally: https://terokarvinen.com/2021/salt-run-command-locally/

Tero Karvinen, Salt Quickstart - SaltStack Master and Slave On Ubuntu Linux: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

Tero Karvinen, Raportin Kirjoittaminen: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

