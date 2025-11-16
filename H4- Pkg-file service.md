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

- 
















