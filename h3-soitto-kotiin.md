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

## A) Hello Vagrant!

<img width="291" height="193" alt="image" src="https://github.com/user-attachments/assets/481928b8-a43e-4304-a799-816b878cb356" />

