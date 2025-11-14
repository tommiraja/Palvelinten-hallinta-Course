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

- Lisätään portti 22 kuuntelemaan sshd_config tiedostoon -> `sudo nano /etc/ssh/sshd_config` -> : <img width="116" height="51" alt="image" src="https://github.com/user-attachments/assets/1026b747-588c-48e7-ae24-4e3d937a5150" />

- Tallennus ja restartaan ssh `sudo systemctl restart ssh`

<img width="609" height="69" alt="image" src="https://github.com/user-attachments/assets/a7a84a5f-eb07-4188-81d4-dcf801d96885" />
Ongelmatilanne!
- Täytyy antaa orjalle masterin osoite komennolla `master: 192.168.12.3` tottakai, sitten hyväksyä orjan avain masterilla.
<img width="357" height="182" alt="image" src="https://github.com/user-attachments/assets/7e9c3b2c-9dd3-41ab-98ab-1fa653285647" />








