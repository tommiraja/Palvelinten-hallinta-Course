# Ympäristönä toimii sama kotikone, kuin viime tehtävissä. Tehtävä tullaan toteuttamaan Vagrantin avulla Windows OS komentokehotteen kautta.

## Tiivistelmä : Karvinen 2018 - https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh
- Konfiguraatio hallinnointi järjestelmällä voi ohjata useita eri demoneja
- Mikäli konfiguraatio asetuksia muutetaan, tulee demoni potkaista käyntiin asetuksien käyttöönottamiseksi
- Komennolla `sudo salt '*' state.apply (daemon) ajetaan halutut demonien tilat`

## a) SSHouto.
- Laitetaan vm:ät käyntiin PowerShellissä `Vagrant up` komennolla. Virtuaalikoneet sisältävät samat konfiguraatiot, kuin H4-Soitto kotiin tehtävässä, eli tarkoituksena käyttää samoja aikaisempia virtuaalikoneita.
- Koneet avautuivat nopeasti, sitten otetaan yhteys `tmaster`-koneeseen -> `vagrant ssh tmaster` -> Asennetaan Salt uudestaan, sillä edellisen tehtävän jälkeen tuhosin virtuaalikoneet (Myös Curl `sudo apt install curl`).
- Kerrataan vielä saltin asennus H3-tehtävästä.
  
<img width="771" height="190" alt="image" src="https://github.com/user-attachments/assets/2a9b2290-7d78-4e11-8340-122ef3e4588e" />

<img width="696" height="70" alt="image" src="https://github.com/user-attachments/assets/c06f0936-94f0-4783-9080-784096de082a" />

- Salt-master toiminnassa, nyt tehdään sama toiselle koneelle (t001) ja asennetaan sille Salt-minion. Asennus toimii samalla tavalla, mutta avainten jälkeen asennetaan `sudo apt install salt-minion`

<img width="704" height="72" alt="image" src="https://github.com/user-attachments/assets/179131d5-4304-440e-89e5-648734e047bd" />

Annetaan vielä masterin osoite minionille -> `sudoedit etc/salt/minion`

<img width="174" height="47" alt="image" src="https://github.com/user-attachments/assets/a737d152-65ff-4723-8799-1120260dd67c" />

Hyväksytään orjan avain master-koneella `sudo salt-key -A`

<img width="377" height="245" alt="image" src="https://github.com/user-attachments/assets/313b5baa-459a-4317-a6ca-7957fa5ee2ed" />

Sitten voidaankin aloittaa varsinainen tehtävä. Lisätään aluksi portti 22 ja 1234 kuuntelemaan `ssh_config` tiedostoon -> `sudo nano ssh_config`

<img width="303" height="60" alt="image" src="https://github.com/user-attachments/assets/536692cd-9fb5-4517-9a08-4eaad0c46d2b" />

Sitten loin uuden hakemiston, johon teen ssh:n sls-tiedoston `sudo mkdir -p /srv/salt/ssh` -> `sudo nano init.sls` -> johon kirjoitin Teron sivuilta saadut konffaukset "Create SSH-state": https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh

<img width="385" height="201" alt="image" src="https://github.com/user-attachments/assets/7c1fffef-efff-4176-ac17-fcfa641ce290" />

Testataan:

<img width="740" height="561" alt="image" src="https://github.com/user-attachments/assets/e84559e6-357a-4072-bb05-dca7a4ecbb1c" />

- Virhetilanne, Salt ei löydä sshd_config tiedostoa masterilta. Korjataan ->

- <img width="765" height="19" alt="image" src="https://github.com/user-attachments/assets/9b741039-f52d-4541-8051-d807d80f2153" />

- <img width="325" height="39" alt="image" src="https://github.com/user-attachments/assets/9a8b08d0-afa6-4983-857a-67e6b541ffcc" />

- Okei virtuaalikoneeni t001 hajosi, en saa enään muodostettua ssh yhteyttä, joten aion tuhota koneen `vagrant destroy t001` komennolla ja sitten aloitan tehtävän alusta. Jatketaan hetken kuluttua, kun saan saltin uudestaan asennettua.

Okei nyt ollaan tääs samassa kohtaa kuin viimeksi. Liitin portit 22 ja 2200 `sudo nano /etc/ssh/sshd_config` ja niiden pitäisi toimia nyt.

<img width="711" height="108" alt="image" src="https://github.com/user-attachments/assets/47bdbca4-343c-4c34-b59c-5a7593cbf14f" />

Eli käsin tehty toimii, sitten kokeillaan automatisoida.

Luodaan uusi hakemisto `Sudo mkdir -p /srv/salt` -> `sudo nano ssh_port.sls -> Luodaan sls-tiedosto

<img width="544" height="449" alt="image" src="https://github.com/user-attachments/assets/b51bee07-46b8-4d8b-a13c-8bcd1d7065ad" />

<img width="590" height="108" alt="image" src="https://github.com/user-attachments/assets/50c362a1-0271-4c9f-8aa1-1ea831da90d6" />

Ajetaan `sudo salt '*' state.apply ssh_port`

<img width="893" height="855" alt="image" src="https://github.com/user-attachments/assets/fd8db7f0-781f-44b5-9bfd-43209f516d65" />

SSH-yhteys tuhoutui uudestaan. Kokeilen seuraavaksi t002 konetta. Asensin Salt-minionin t002 koneeseen, määiritin hostin osoitteen minionille, potkaisin käyntiin, hyväksyin avaimen tmasterilla.

<img width="601" height="991" alt="image" src="https://github.com/user-attachments/assets/ab221b17-aaed-47bf-954d-c24f9eba43a1" />

Noniin säädön jälkeen jo parempaan päin, katsotaann että tila korjaa puutteet t002-koneella.

<img width="636" height="242" alt="image" src="https://github.com/user-attachments/assets/cdc67b00-9854-4a79-b601-6ccc7a89e4b1" />

- Eli poistetaan t002 koneelta ssh-server, sitten ajetaan tila uudestaan tmaster koneella, tämän nyt pitäisi asentaa ssh serveri takaisin minionille.

<img width="717" height="746" alt="image" src="https://github.com/user-attachments/assets/b6f4203f-edf2-4691-b233-f699cee8d357" />

- Toimii! Vikatilanne taisi ilmetä rikkinäisen `sshd_config` tai sls- tiedoston takia, sitten kun yritin ajaa staten salt restarttasi ssh-palvelun ja siinä oli väärät konfiguraatiot -> ssh-yhteys kaatui. Nyt raporttiani tutkineena olin myös unohtanut mainita, että kun konfiguraatioita muuttaa sshd_config tiedostossa, täytyy ssh sen jälkeen uudelleenkäynnistää.
- Selvitin ongelmaa tekoälyn (Chat-GPT) avulla, otin virheilmoituksesta kuvakaappauksen tekoälylle ja promptasin "Miten voisin selvittää kyseisen ongelman, niin että ssh-palvelu ei kaadu".
- Tekoäly ehdotti minulle turvallisemman sls-tiedoston luomista, joka sisältää `ssh_ports_block:` `file.blockreplace` ja `check_sshd_config:` konfiguraatiot

- <img width="519" height="515" alt="image" src="https://github.com/user-attachments/assets/6a2e8af1-7f1d-40c6-968f-47144d40e842" />

- `sudo systemctl restart ssh` ! Demonin potkaisu, kun konffeja muutetaan.

  (Tämän muutoksen jälkeen minulla alkoi toimimaan tilan ajo)

### Tässä vielä recap mitä tein eri tavalla t002-koneella

- <img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/eeef5e56-2fd0-4496-8c96-aac8487b22d2" />

  - Määritin portit minionille

- <img width="203" height="105" alt="image" src="https://github.com/user-attachments/assets/c269f392-48f6-4db4-8b83-ceae9a7b6ce0" />

  - Määritin minionille masterin osoitteen ja oman id:n

- <img width="256" height="69" alt="image" src="https://github.com/user-attachments/assets/a6e31d94-a5f8-4dfe-a297-733ebaed7f62" />

  - Tein polkuun `srv/salt/ssh_port_t002` sls.tiedoston ja määritin sen konffaukset tekoälyn ehdottamalla tavalla

- <img width="532" height="516" alt="image" src="https://github.com/user-attachments/assets/871adf3b-2895-4cd5-98a0-60a3fb7475da" />

Tämä tehtävä oli farssi, mutta jonkin näköseen lopputulokseen onneksi päästiin. Hermo oli koetuksella, sillä onnistuin tuhoamaan ssh yhteydet t001 koneeseen useaan otteeseen, kuitenkin juurisyynä tähän konfiguraatiovirhe sshd_config tiedostossa ja teorian perusteiden omaksuminen työskentelyyn. Aikaa kului ainakin 3h.

## Lähteet: 

Karvinen 2018: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh

ChatGPT 5.1: Kuvalähteenä virheilmoitus PowerShell terminaalista ja promptaus "Miten voisin selvittää kyseisen ongelman, niin että ssh-palvelu ei kaadu".


































