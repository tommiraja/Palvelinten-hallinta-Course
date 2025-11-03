# H2 - Infraa koodina

## Nopea ympäristön kuvaus
- Windows 10 Home, 64-bit os
- 16 gb ram
- Virtuaalikone via VirtualBox:
<img width="517" height="609" alt="image" src="https://github.com/user-attachments/assets/ff67d67e-d8f1-4bf1-a5ba-a680a82ba455" />

## Tiivistelmät

### Karvinen 2014: https://terokarvinen.com/2024/hello-salt-infra-as-code/
- Saltissa orja koneille jaetaan tiedostokansiot, joihin määritellään infra koodina
- Saltin tiedostopäätteet ovat .sls - päätteisiä, joihin määritetään koodi, minkä mukaisesti orjakoneet toimivat
- Käyttäjän on oltava tietyn kansion sisällä, johon .sls tidosto tullaan luomaan
### Salt contributors: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml
#### Rules of YAML
- YAML on merkintäkieli, jonka tehtävänä on kääntää YAML-datarakenne Python datarakenteeksi Saltin käytettäväksi
- YAML merkintäkielessä käytetään vain välilyöntejä, tabulaattorin käyttö ei ole sallittua, kommentit kirjoitetaan "#" merkillä, mappingsit käyttävät kaksoispistettä ja yhtä välilyöntiä esim. nimi: "Book Worm", missä "nimi" toimii avaimena -> ja "Book Worm" arvona.
#### YAML simple structure
- Kolme eri elementtiä: Avaimet, listat ja hakemistot.
- Listoissa arvot kirjoitetaan viivan "-" jälkeen, sanakirjat voivat sisältää avain-pareja, sekä listoja.
- YAML erottaa isot ja pienet kirjaimet toisistaan, esim `Key,` `key,` `KEY` ovat erillisiä avaimia.
#### Lists and dictionaries - YAML block structures
- YAML-kieli on järjestetty lohkotyyppisiin rakenteisiin.
- Sisennys tapahtuu vakiona kahdella välilyönnillä.
- Luettelomerkinnät luodaan yhdysviivalla "-" ja yhdellä välilyönnillä.
### Salt contributors: https://docs.saltproject.io/en/latest/ref/states/top.html
#### Introduction
- Useimmat infrastruktuurit koostuvat koneiden ryhmistä, joissa jokaisella koneella on oma roolinsa.
- Ylläpitäjä määrittelee roolit ryhmille ja hallitsee niitä.
- Saltissa `Top file` toimii pää-asiallisena määrittelijänä konfiguraatioille, joiden mukaan kukin ryhmä toimii.
#### A basic example
- `Top file` muodostuu kolmesta osasta: enviroment, target ja state file.
- Enviroment eli ympäristö sisältää target-ryhmät, jossa taas targetit sisältävät state-tiedostot.
- Esimerkkinä tilanne, jossa orjakoneiden ID:t sisältävät "web" tunnisteen, tarkoittaa se sitä että ne saavat apache.sls-konfiguraatiot.

## A) Hei infrakoodi!
- Tarkoituksena oli tehdä sls-tiedosto, joka luo uuden tiedoston haluttuun polkuun
- Homma alkoi hakemiston luonnilla `sudo mkdir -p /srv/salt/moisalt/` -> Tämän jälkeen loin sls-tiedoston kansion sisälle `sudo nano init.sls` -> nano editoriin funktiot `/tmp/SaltinTekemä:`(polku), `file.managed` (statement) -> tallennus ja eikun kokeilemaan.
- `sudo salt-call --local state.apply moisalt`

- <img width="321" height="24" alt="image" src="https://github.com/user-attachments/assets/ce776bbd-09f1-474e-a8ab-b1fbe14c1cae" />

- <img width="222" height="76" alt="image" src="https://github.com/user-attachments/assets/c6cdb54d-850c-4a5e-a26a-f8cf6926cafd" />

- <img width="669" height="435" alt="image" src="https://github.com/user-attachments/assets/bd0d0aed-5d4c-4439-b4c4-f7d3bd3fb061" />
## B) Topping.
- Tarkoituksena luoda top-file, jonka avulla voidaan ajaa kaikki viisi tilafunktiota yhdellä `sudo salt-call --local` funktiolla.
- Alkuun loin polun top-filelle `sudo mkdir /srv/salt/top.sls` -> nano editorilla muokkaus `sudo nano top.sls` -> nanoon kirjoitin viiden tilafunktion id:t.
  
- <img width="282" height="185" alt="image" src="https://github.com/user-attachments/assets/cc178687-1f05-4d08-984d-b263ce380a47" />

- <img width="297" height="28" alt="image" src="https://github.com/user-attachments/assets/7fe5809a-d39e-4830-a486-908df462f3a1" />

- Sitten loin kaikkien tilojen omat SLS-tiedostot suoraan saltin polkuun ja `YAML` koodilla statementtien konfiguroinnit, `sudo tee /srv/salt/hellopkg.sls` jne...
- Nyt `pkg:n` pitäisi asentaa cowsay paketti, `file` luo hello.txt tiedoston `/tmp` polkuun, `service` varmistaa cronin päällä olon, `user` luo käyttäjän hello ja `cmd` suorittaa komennon `echo "Moi T: Salt" | tee /tmp/hello_cmd.out`

- <img width="943" height="726" alt="image" src="https://github.com/user-attachments/assets/1e36e904-3e02-4105-9da9-5f0a05bff564" />

- Kokeillaan nyt ajaa `sudo salt-call --local state.apply`

- <img width="838" height="724" alt="image" src="https://github.com/user-attachments/assets/18a802eb-2236-403d-958a-fe1373b1f511" />

- <img width="1267" height="725" alt="image" src="https://github.com/user-attachments/assets/4bfda4b4-83c1-4ad8-9d68-c17509061cf7" />

- <img width="676" height="447" alt="image" src="https://github.com/user-attachments/assets/6abfbe86-927f-4d31-9904-d9bcba034cbf" />

- <img width="786" height="740" alt="image" src="https://github.com/user-attachments/assets/b670d30a-8b60-4275-811b-fa18cce24906" />

- Kuvien perusteella voidaan päätellä, että kaikki sujui onnistuneesti!

## C) Viisikko tiedostossa.
- Aloitetaan `pkg` tilafunktiosta.
- Alkuun loin tarvittavat hakemistost jokaiselle viidelle tilafunktiolle yhdellä komennolla -> `mkdir -p /srv/salt/{hellopkg,moiuser,moifile,moicmd,moiservice}` -> Tämän jälkeen loin init.sls tiedostot jokaisen uuden hakemiston sisään sudoeditorilla `sudo nano init.sls`. Tämä kohta tehtiin jokaisen tilafunktion kohdalla erikseen. Huomioitavana se, että on oikean directoryn sisällä.
### 1.PKG

- <img width="240" height="76" alt="image" src="https://github.com/user-attachments/assets/272b5de4-d115-42c9-9abc-60444738b1d3" />

- Kirjoitin nano editoriin komennon, joka asentaa pkg:n -> `pkg.installed` -> tallennus!
- Testaus:
-   <img width="538" height="200" alt="image" src="https://github.com/user-attachments/assets/47432096-1288-40a6-865f-4df330cf40b8" />

- Vihreää, näyttää toimivan!
### 2. User

- Suuntasin `moiuser` hakemistoon, loin init.sls-tiedoston joihin kirjoitin komennon `user.present:`, joka varmistaa tietyn käyttäjän olemassaolon tai luo sen, mikäli sitä ei vielä ole. Tämän alle määrittelin käyttäjän nimen, sekä kotihakemiston.
- <img width="349" height="120" alt="image" src="https://github.com/user-attachments/assets/98ccd338-24e6-4920-9744-e7db67edfa56" />
- Moiuserin ajaminen pitäisi nyt luoda "Tommi2" niminen käyttäjä, sekä sille oman kotihakemiston `/home/viisikkotestit`
- Lets see!
- <img width="792" height="688" alt="image" src="https://github.com/user-attachments/assets/82713bfa-74ea-4a1a-8e94-cfca6f4dc31f" />
- Näyttää pelittävän! 
### 3. File
- Suunnataan `moifile`hakemistoon -> sudo nano init.sls -> `/tmp/moi.txt`, `file.managed`, `- contents: "Moi Tiedosto :)` -> Nyt kun file staten ajaa, pitäisi uuden "moi.txt"-tiedoston ilmestyä /tmp/moi.txt polkuun, sisältäen "Moi Tiedosto :)" tekstin.

- <img width="330" height="91" alt="image" src="https://github.com/user-attachments/assets/2014f35c-97dc-496d-aef1-24e3f70dd548" />

- Kokeillaan:

- <img width="718" height="379" alt="image" src="https://github.com/user-attachments/assets/1e72537d-8cd0-45cb-bfe0-ec97a6e5c376" />
  
- <img width="338" height="41" alt="image" src="https://github.com/user-attachments/assets/508f5662-89bd-41eb-848c-6a6976f3b15d" />

- Noniin! Uuden tiedoston luonti onnistui, `/tmp/moi.txt`polkuun.
### 4. Cmd
- Nyt cmd:n vuoro. Löydetään tie taas `moicmd` kansioon -> `sudo nano init.sls` -> :
- <img width="513" height="91" alt="image" src="https://github.com/user-attachments/assets/782745e9-19f3-4c84-9571-ca398e855a2e" />

Testi: 

- <img width="712" height="471" alt="image" src="https://github.com/user-attachments/assets/6b0537ba-7626-41e7-8ada-35e0e165d931" />

- <img width="400" height="38" alt="image" src="https://github.com/user-attachments/assets/9ce94049-4332-419b-8742-969af7547a74" />

- Jes. Näin saatiin cmd:n avulla luotua tiedosto haluamaani polkuun. Huomasin kuitenkin, ettei state-funktio `moicmd` ole idempotentti, mitenköhän korjaan? Kysyin tähän asiaan apua tekoälyltä ja soluutioksi sain `creates:` statementin käytön -> Vaihdoin init.sls:ään nano editorilla kohdan `creates: /var/local/moi1.txt`. Kyseisen staten merkitys on siinä, että `creates:...` estää komennon ajamisen, jos tiedosto on jo luotu tiettyyn polkuun ja siten se on idempotentti.

- Lopputulos:

- <img width="646" height="345" alt="image" src="https://github.com/user-attachments/assets/6517735f-bd05-4b23-bdc8-aca46459c2b5" />
### 5. Service
- Viides tilafunktio service, tehdään tämä tekemällä init.sls-tiedosto, jonka statementin ajo asentaa openssh-server paketin, sekä tarkistaa sen päällä olon. Sls-tiedosto asentaa ssh-pkg paketin, sallii openssh-serverin avautumisen kun virtuaalikone käynnistetään ja varmistaa sen päällä olon, mutta vaatii oikean paketin olemassa oloa.

- <img width="337" height="214" alt="image" src="https://github.com/user-attachments/assets/3ad3c0c4-29b9-4647-bb48-87a11ba45fc3" />

- <img width="800" height="507" alt="image" src="https://github.com/user-attachments/assets/41100373-be7c-4cac-8e4e-150500ae3dd8" />

- ...alreday installed. Nähdään, että service statement toimi, kuin myös sen että minulla oli openssh-server jo valmiiksi asennettuna.

## D) Useampi eri tilafunktio käytössä.
- Luodaan jokin sls-tiedosto, joka käyttää kolmea eri tilafunktiota samaan aikaan.
- Loin harjoitusta varten uuden hakemiston `state3` johon tein sls-tiedoston.

- <img width="395" height="318" alt="image" src="https://github.com/user-attachments/assets/5a653b84-49c3-45fa-a16f-32494c927dea" />

- Seuraavaksi päästään kokeilemaan.

- <img width="765" height="623" alt="image" src="https://github.com/user-attachments/assets/efe3da19-a083-4087-99b0-55eb9403bc93" />

- Jee! :)

## Lähteet:
- Karvinen 2014: https://terokarvinen.com/2024/hello-salt-infra-as-code/
- Salt Contributors: Starting or restarting of services and daemons: https://docs.saltproject.io/en/3007/ref/states/all/salt.states.service.html
- Salt contributors: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml
- Salt contributors: https://docs.saltproject.io/en/latest/ref/states/top.html


## Tehtäviin kulunut aika?
- Tiivistelmä noin puoli tuntia
- Tehtäväosiot noin 3h, oli hieman haastavempia tällä kertaa.
