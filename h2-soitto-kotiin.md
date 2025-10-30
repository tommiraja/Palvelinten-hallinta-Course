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
<img width="321" height="24" alt="image" src="https://github.com/user-attachments/assets/ce776bbd-09f1-474e-a8ab-b1fbe14c1cae" />

<img width="222" height="76" alt="image" src="https://github.com/user-attachments/assets/c6cdb54d-850c-4a5e-a26a-f8cf6926cafd" />

<img width="669" height="435" alt="image" src="https://github.com/user-attachments/assets/bd0d0aed-5d4c-4439-b4c4-f7d3bd3fb061" />


## B) Topping.

<img width="282" height="185" alt="image" src="https://github.com/user-attachments/assets/cc178687-1f05-4d08-984d-b263ce380a47" />

<img width="297" height="28" alt="image" src="https://github.com/user-attachments/assets/7fe5809a-d39e-4830-a486-908df462f3a1" />

<img width="943" height="726" alt="image" src="https://github.com/user-attachments/assets/1e36e904-3e02-4105-9da9-5f0a05bff564" />

<img width="838" height="724" alt="image" src="https://github.com/user-attachments/assets/18a802eb-2236-403d-958a-fe1373b1f511" />

<img width="1267" height="725" alt="image" src="https://github.com/user-attachments/assets/4bfda4b4-83c1-4ad8-9d68-c17509061cf7" />

<img width="676" height="447" alt="image" src="https://github.com/user-attachments/assets/6abfbe86-927f-4d31-9904-d9bcba034cbf" />





## C) Viisikko tiedostossa.

## D)

## Lähteet

## Tehtäviin kulunut aika?
- Tiivistelmä noin puoli tuntia
- Tehtäväosiot ?
