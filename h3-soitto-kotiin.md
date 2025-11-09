# H3. Soitto kotiin.
## Tiivistelmät
### Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/
- Vagrantilla voi luoda automaattisesti VirtualBox virtuaalikoneita
- Automatisoi SSH-sisäänkirjauksen
- Onnistuu ilman graafista käyttöliittymää
### Karvinen 2018: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux
- Orjan tiedettävä, missä Master kone on, jotta tämä voi vastaanottaa tehtäviä
- Minionin potkaisu tärkeä osa yhteyden muodostamisessa
- Masterin on hyväksyttävä orjan avain
### Karvinen 2023: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file
- Minionin toivottu lopputila kirjoitetaan SLS-tiedostoon YAML-kielellä
- "'*'" ajaa tilan kaikille minioneille
- Top-file määrittää mitä tiolja ajetaan millekkin orjalle

## Tehtävät tehdään Windows 11 Os koneella, 16gb-ram, 64-bit os. Komentokehotteen kautta.

### A) Hello Vagrant!

<img width="291" height="193" alt="image" src="https://github.com/user-attachments/assets/481928b8-a43e-4304-a799-816b878cb356" />

<img width="367" height="62" alt="image" src="https://github.com/user-attachments/assets/f13843d6-fa2b-4769-910c-4f838fdaa6cc" />


### B) Linux Vagrant. Uusi Linux-virtuaalikone Vagrantilla.

Aluksi loin komentokehotteella uuden kansion, johon Vagrant-file luodaan. `mkdir vagrantit`-> `cd vagrantit` -> `vagrant init debian/bookworm64`. Sitten kun vagrant-tiedosto oltiin asetettu uuteen paikkaan oli aika käynnistää virtuaalikone `vagrant up` komennolla.

<img width="954" height="565" alt="image" src="https://github.com/user-attachments/assets/0eaa96f3-57cf-4cdf-8a5f-201646861dd4" />

Virtuaalikoneen käynnistämisessä kului noin 3. minuuttia. Tarkkaillessani VirtualBoxia, huomasin että sinne ilmestyi luomani kone.

<img width="384" height="56" alt="image" src="https://github.com/user-attachments/assets/4fa8ecf0-aaf8-4e6b-91dd-d7924a213a3a" />

Sitten oli aika muodostaa ssh-yhteys virtuaalikoneeseen `vagrant ssh` - komennolla.

<img width="815" height="195" alt="image" src="https://github.com/user-attachments/assets/d3599f27-88ff-4778-bc2c-5caa4f001287" />

<img width="350" height="101" alt="image" src="https://github.com/user-attachments/assets/b375c5f4-e7e2-4e35-808b-0e8f79af0072" />

Kokeilin vielä paria `whoami` komentoa varmistaakseni toimimisen. Lopulta tuhosin luomani koneen `vagrant destroy`

<img width="666" height="152" alt="image" src="https://github.com/user-attachments/assets/f544fa53-1018-4a64-9e99-60ddd7380a89" />

### C) Kaksin kaunihimpi.

Käydään muokkaamassa aluksi vagrant-tiedostoa vscoden avulla. Lisäsin tiedoston konfiguraatioihin komennot, joka luo minulle kaksi virtuaalikonetta t001 ja t002. Valmiit konfigit saatu Tero Karvisen nettisivulta : https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

Huom! Muokkasin myös kohdan "bullseye64" -> bookworm64. Sitten tallensin tiedoston ja kokeilin `vagrant up`

<img width="708" height="474" alt="image" src="https://github.com/user-attachments/assets/f0d0025e-e3e0-4dba-af90-99bc8871afeb" />

<img width="686" height="385" alt="image" src="https://github.com/user-attachments/assets/b9aa2de4-79ad-4532-a710-64e717b43de1" />

VIRHETILANNE -> Korjataan konfigurointi tiedostoa vscodessa. Poistin tiedostosta toisen `vagrant.do` lohkon, sekä ylimääräisen `end` lohkon. Kokeillaan nyt uudestaan `vagrant up`. Nyt alkoi toimia!

<img width="852" height="216" alt="image" src="https://github.com/user-attachments/assets/8ad3b684-d221-4d7b-8a6d-8877ed71f5a0" />

Nyt asennus oli nopeampi. Kokeillaan heti SSH-yhteyttä koneeseen `t001` -> vagrant ssh `t001` -> sitten pingataan t002 osoitetta, joka asetettiin konfiguraatio tiedostoon vagrant-fileen -> `ping 192.168.88.102`

<img width="588" height="194" alt="image" src="https://github.com/user-attachments/assets/56084b86-813e-43ec-a488-06f87938db63" />

Näyttää toimivan. Kokeillaan sitten kirjautua ssh-yhteydellä t002 virtuaalikoneelle ja tehdään sama pingaus sillä, mutta t001 osoitteeseen -> `exit` -> `vagrant ssh t002` -> `ping 192.168.88.101`

<img width="877" height="488" alt="image" src="https://github.com/user-attachments/assets/3f73adeb-6944-4e72-ab21-7cfb1eb92616" />

Näyttää wörkkivän!

### D) Herra-orja verkossa

Aloitin tehtävän muokkaamalla vagrant-tiedoston konfiguraatio asetuksia ja lisäsin sinne komennot, jotka lataavat salt minionin ja salt masterin virtuaalikoneilleni. Komennot on saatu Tero Karvisen sivuilta "Salt Vagrant - Automatically provision one master and two slaves": https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file
Muokkasin myös kohdan "bullseye" bookwormiksi.

<img width="362" height="54" alt="image" src="https://github.com/user-attachments/assets/1074ec78-6237-4ac8-a8b9-6c7a7ea624f5" />


<img width="768" height="723" alt="image" src="https://github.com/user-attachments/assets/91e678c1-fd7d-4ded-8b95-b1999d8e2f6d" />

Tämän jälkeen loin uudet koneet `Vagrantit` kansiooni komennolla `init vagrant` -> `vagrant up`

<img width="387" height="170" alt="image" src="https://github.com/user-attachments/assets/218eaae1-80f8-4458-9edc-085b60f6b1dd" />

Noniin, VirtualBoxi näyttää jo koneita!

Muodostetaan ssh yhteys t002 koneeseen `vagrant ssh t002`, sitten hommataan curl komento käyttöön `sudo apt install curl` ja aloitetaan saltin asentaminen. Asennetaan salt-master t002 koneelle ja salt-minion t001 koneelle.
1. Loin avaimille kansion `mkdir etc/apt/keyrings`
2. Latasin avaimet: `curl -fsSL https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public | sudo tee /etc/apt/keyrings/salt-archive-keyring.pgp`, `curl -fsSL https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources | sudo tee /etc/apt/sources.list.d/salt.sources`
3. `sudo apt update` -> `sudo apt install salt-master`.
4. Tarkistetaan päällä olo `sudo systemctl status salt-master.service`
5. Otetaan master koneen osoite talteen `hostname -I`, tämä osoite laitetaan hetken päästä salt-minionin tiedostoihin.

<img width="959" height="1026" alt="image" src="https://github.com/user-attachments/assets/f3bca9f2-f20d-400d-8d7f-d44929d04f45" />

<img width="962" height="689" alt="image" src="https://github.com/user-attachments/assets/717b6408-6a5c-4c6d-a95f-5c8fa1f8292b" />

<img width="790" height="120" alt="image" src="https://github.com/user-attachments/assets/a40a116d-e9b6-4e92-b807-4ff76ba15691" />

<img width="480" height="36" alt="image" src="https://github.com/user-attachments/assets/f7b5204f-c638-4b98-a4a9-58aae542ce67" />

Noniin, nyt Salt-master pitäisi olla asennettuna

Hoidetaan seuraava kone t001 -> `exit` -> `vagrant ssh t001` -> samat saltin asennus-stepit kuin edellisessä -> `sudo apt install salt-minion`

<img width="736" height="90" alt="image" src="https://github.com/user-attachments/assets/4bb4b53f-397b-42cc-bf64-24abef863bf9" />

Nyt aika antaa master-koneen osoite minionille `sudoedit /etc/salt/minion` -> laitetaan nano fileen `master: 10.0.2.15` ja tunnisteeksi `id: orja`

<img width="182" height="85" alt="image" src="https://github.com/user-attachments/assets/fb4be38f-55e3-40be-a7aa-4b4669275979" />

Sitten potkaistaan daemoni käyntiin `sudo systemctl stop salt-minion` ja sitten `...start salt-minion`

Siirrytään nyt master-koneelle hyväksymään minionin avain -> `exit` -> `vagrant ssh t002` -> `sudo salt-key -L` katsotaan, että minionin avain näkyy ja hyväksytään se `sudo salt-key -A`.

<img width="396" height="211" alt="image" src="https://github.com/user-attachments/assets/f9a85180-8166-440a-8bc5-51b3b5ab6958" />

Kokeillaan, että herra komentaa orjakonetta. Kokeillaan vastaako orja `sudo salt '*' cmd.run whoami` komentoon.

<img width="366" height="65" alt="image" src="https://github.com/user-attachments/assets/9055d433-25d5-4c1a-8b3d-8150095d5091" />

Vastasi!

### E) Kaksi tilaa verkon yli.

Kokeillaan ensimmäisenä pkg-tilafunktiota komennoin `sudo salt '*' pkg.version bash`

<img width="404" height="94" alt="image" src="https://github.com/user-attachments/assets/5571e91f-b2aa-4317-8c47-b28827024c54" />

Jes. Kokeillaan vielä toista file-tilafunktiota `sudo salt '*' state.single file.managed name=/tmp/hello.txt`

<img width="612" height="354" alt="image" src="https://github.com/user-attachments/assets/d8b73239-4f7b-4deb-a63f-ae0883dd0b5c" />

Jee.

Tehtäviin meni noin 3-tuntia aikaa.

## Lähteet:

Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/

Karvinen 2018: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux

Karvinen 2023: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file


























