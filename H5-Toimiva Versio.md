# Ympäristönä tuttu ja turvallinen kotikone: Windows OS, 16gb ram, x64-bittinen OS, Microsoft Windows 11 Home. Tehtävät tehdään Vagrantilla Windows Powershellin kautta SSH yhteydellä virtuaalikoneeseen.
## Tiivistä.
### Chacon and Straub 2014: https://git-scm.com/book/en/v2 ja https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
- Pro Git book, on gitin käytöstä kertova kirja, joka kertoo miten versionhallintajärjestelmää voi käyttää perusteista, palvelimen käyttöön ja hajautettuun työskentelyyn
- Gitin toiminta perustuu siihen, että jokaisesta projektin versiosta tallennetaan tehdyt muutokset aina kun niitä tehdään, vanhoja versioita voi tarkastella gitissä.
- Gitissä kaikki data takastetaan eheydentarkistuksella, joka mahdollistaa sen että tiedostoja ei voi muuttaa tai rikkoa huomaamatta.

### Git komennot: `Git add . && git commit; && git pull && git push`
- `Git add` - Komennolla lisätään muutoksia tulevaan committiin. Se lisää muutetut, sekä uudet tiedostot "staging"-alueelle.
- `Git commit` - Luo uuden commitin. Komennolla tallennetaan tiedostoja Gitin arkistoon.
- `Git pull` - Komennolla haetaan uusimmat muutokset tietystä reposta. Git pull:in avulla voidaan tuoda ystävän repo omaan komentoliittymään ja tekemään muutoksia sinne mikäli oikeudet sallivat.
- `Git push` - Komennolla pusketaan omat lokaalit commitit verkon yli git-repoon.

### Varaston terokarvinen/suolax/ historia, eli loki ja muutokset: https://github.com/terokarvinen/suolax/
- READ.ME - kansio sisältää tietoa Saltin käyttämisestä, viimeisimmät muutokset on tehty viime vuoden aikana, lokien mukaan Tero on parantanut käyttö-ohjeita tiedostolokien perusteella, joka muutokset aikana.
- https://github.com/terokarvinen/suolax/commits/main/ - Viimeisimmät commitit on tehty 10.4.2024. Ainakin kahdeksan committiä on tehty.

## A) Online. Uusi Varasto GitHubiin.
- Tein uuden repon nimeltä `Snow-repo`
- Kuvaus: `Snow`
- Varaston tiedostot: `README.md & GNU General Public License 3`
- Sitten tallensin uuden repon
- <img width="941" height="789" alt="image" src="https://github.com/user-attachments/assets/ad7a951a-7843-40e8-ac72-b77b92c464b4" />

## B) Dolly.
- Aloitetaan `sudo apt-get install git`, minulla kuitenkin oli jo gitti näköjään asennettuna.
- Kloonasin Snow-repon -> `git clone (REPON URL)`

- <img width="635" height="157" alt="image" src="https://github.com/user-attachments/assets/c449b341-0889-4217-8e3f-8634dae827f0" />

- Sitten luodaan SSH-avain.
    - `ssh-keygen` -> 3x ENTER-painallus -> Minulla oli jo näköjään luotu ssh-avain, mutta kirjoitin sen yli -> Suuntasin avaimen sijaintiin -> katsoin `cat id_rsa.pub` - julkisen avaimen koodi.
    - Avain pitää kopioida GitHubissa oikean ylänurkan profiilikuvan kautta -> Settings -> SSH and PGP-keys -> Add new key...
    - <img width="891" height="216" alt="image" src="https://github.com/user-attachments/assets/09c8443e-a1df-4ba5-af73-a837b5a9ad00" />
    
    - <img width="1007" height="300" alt="image" src="https://github.com/user-attachments/assets/42cd68fc-5306-4fa0-9518-221f5e2ad8fa" />

    - Sitten siirryin Snow-repoon -> `cd Snow-repo` -> Tein hieman hassusti seuraavaksi, sillä koodasin uuden repon kansion sisään vagrantissa -> `git clone git@github.com:tommiraja/Snow-repo.git` -> Siirryin Snow-repon sisään `cd:llä` ja tein muutoksia
    - <img width="808" height="554" alt="image" src="https://github.com/user-attachments/assets/b65f2b7a-a2e0-4bea-a927-ada5cd472004" />
    
    - <img width="971" height="168" alt="image" src="https://github.com/user-attachments/assets/17089632-f8f9-40dc-b13e-c36fede25e90" />
    - Muutokset onnistuivat.
 
 ## C) DOH! Huonojen muutoksien tuhoaminen Gitissä
 - Aluksi tein `echo "Tässä muutoksessa virhe!!!!" >> README.md -> `git add` -> `git status` -> katsoin, että muutokset ovat tulleet, mutta vaativat vain commitin. Sitten vain `git reset --hard`
- <img width="878" height="594" alt="image" src="https://github.com/user-attachments/assets/14b53084-eabd-41c8-b529-90091cbad508" />
   
- Viimeisin muutos on resetattu.

## D) Git lokin tarkastelu

- Sain git lokin näkyviin komennolla `git log --patch`

- <img width="866" height="966" alt="image" src="https://github.com/user-attachments/assets/52f12325-0fd5-494d-b7ba-301294246082" />

- Lokista nähdään tekijän tiedot, päivämäärä, ja commitit. Huomataan,  että README.md tiedostoa on muokattu ja onnistuneesti puskettu "Muutoksia tehty Vagrant koneelta." Snow-repoon, sekä lisätty viesti "+Muutoksia Vagrant koneesta".
- Loki näyttää myös Repositoryn GNU General Public Lisenssin tiedot.

## E) Suolattu. 

Alkuun loin kaksi kansiota salt ja top, Snow-repo polkuun -> Salt kansiossa `sudo nano init.sls` ja sama top kansion sisällä -> Määrittelin statet `file.managed` ja `Tree` -> Sitten tein top.sls tiedoston -> `sudo nano top.sls` -> Kokeilin statejen ajamista `sudo salt-call --local state.apply`
Sitten olikin aika vain puskea gittiin muutokset.
- `git add .`
- `git commit -m "Muutoksia"`
- `git push`

<img width="702" height="214" alt="image" src="https://github.com/user-attachments/assets/837a7698-9b6c-43ef-b91a-1cb4b687efd0" />

<img width="390" height="168" alt="image" src="https://github.com/user-attachments/assets/e5481886-0a61-4a58-b016-cedce74b3323" />

<img width="501" height="99" alt="image" src="https://github.com/user-attachments/assets/c1c45d86-7b97-416b-8189-fbd094c8b08f" />

<img width="726" height="515" alt="image" src="https://github.com/user-attachments/assets/48e36611-d132-4e5c-80ad-e307b2b4478e" />

<img width="603" height="271" alt="image" src="https://github.com/user-attachments/assets/6b537d82-ec9d-4e62-a436-545800fcfb19" />

<img width="664" height="284" alt="image" src="https://github.com/user-attachments/assets/f32902a7-a0b9-4745-b58e-c297f0677186" />

- Kansiot onnistuneesti Gitissä!

- Katsotaan vielä erilaisella komennolla `sudo salt-call --local --file-root=. state.apply salted` -> Tämä ajaa nyt file.managed tilan

<img width="873" height="444" alt="image" src="https://github.com/user-attachments/assets/75c5b5b6-8313-4690-b601-aae9eb9d96cd" />

- Perfect!

Tehtäviin meni 3h aikaa.

### Lähteet:

- Chacon and Straub 2014: https://git-scm.com/book/en/v2
- Karvinen (vinkit osio):  https://terokarvinen.com/palvelinten-hallinta/#h5-toimiva-versio
- Chacon and Straub 2014: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
- Suolax repository, Karvinen Tero: https://github.com/terokarvinen/suolax/
- Karvinenm Tero: https://github.com/terokarvinen/suolax/commits/main/
