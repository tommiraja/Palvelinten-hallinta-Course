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














