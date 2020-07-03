![](fjärrstyr.gif)

---

- [1. Syfte](#1-syfte)
- [2. Funktioner](#2-funktioner)
- [3. Installation](#3-installation)
  - [3.1. Beroenden](#31-beroenden)
  - [3.2. Lokal installation](#32-lokal-installation)
  - [3.3. Global installation](#33-global-installation)
- [4. Användning](#4-användning)
- [5. Referens](#5-referens)

## 1. Syfte

__Vad är poängen med det här programmet?__

Programmet gör det något bekvämare att använda fjärranslutningar till andra datorer och servrar via SSH-protokollet`*` - dels genom att spara favoritanslutningar och dels genom att skifta färgtema på terminalfönstret. Färgskiftet gör det snabbt och enkelt att se vilka terminaler som är lokala och vilka som inte är det (vilket enligt en kompis kan minska risken att man göra dumma misstag).

>`*`SSH (Secure Shell) är ett protokoll som används för att säkert  och krypterat ansluta sig mot andra datorer över ett nätverk (både Internet och lokala sådana). SSH består av en serverdel, som vanligtvis lyssnar på port 22, och en klientdel. Den vanligaste implementationen är OpenSSH.

## 2. Funktioner

+ Alla talar svenska!
+ Lagra favorit-servrars anslutningsuppgifter.
+ Skiftar färg på terminalfönster vid anslutning. Återställer vid avslutning.
+ Testar innan uppkoppling om servern svarar på anrop på port 22.
+ ~~hashcat-integrering.~~
+ Bash-komplettering, d.v.s. automatisk ifyllning när man dubbelklickar på [TAB]-tangenten.



## 3. Installation

För att installera programmet krävs bara att du först ändrar dess rättigheter till körbar och sedan placerar den i en mapp som ligger i din __$PATH-variabel__`*`.

>`*`$PATH-variabeln berättar för skalet (i det här fallet Bash) vilka mappar som datorns program ligger i. Alla mappar som är definierade i $PATH laddas liksom alltid som en stor bonusmapp efter att mappen som du faktiskt är i har laddats så att programmen som ligger däri alltid är nåbara utan att definiera deras fulla sökväg.

### 3.1. Beroenden

För att allt ska funka måste du ha följande program installerade.
+ **ssh**
+ **netcat**
+ **konsole** - Bara om du vill ha skifte av färg vid anslutning.


### 3.2. Lokal installation

Följande kommandon installerar programmet för en specifik användare.

``` bash
# Se till att $HOME/bin ligger i $PATH.
echo $PATH

# Om du inte ser $HOME/bin måste du lägga till den genom att redigera $HOME/.bashrc.
nano $HOME/.bashrc

# Klistra nu in följande längst ned i filen:
export PATH="$HOME/bin:$PATH"

# Ladda ned programmet!
git clone https://github.com/albinhenriksson/fjarrstyr
cd fjarrstyr

# Gör programmet körbart.
chmod +x fjärrstyr

# Kopiera till program-mappen.
cp fjärrstyr $HOME/bin/
```

Klart! Om du också vill ha autoifyllnad när du klickar på [TAB] så behöver du bara skriva följande kommando.
``` bash
echo "source \"$(realpath _fjärrstyr)\"" >> ~/.bashrc
```

### 3.3. Global installation

Om du vill att programmet ska vara tillgängligt för alla användare på systemet, inklusive root-användaren gör du följande.

``` bash
# Ladda ned programmet!
git clone https://github.com/albinhenriksson/fjarrstyr
cd fjarrstyr

# Gör programmet körbart.
chmod +x fjärrstyr

# Kopiera till program-mappen.
cp fjärrstyr /usr/bin/
```

Klart! Om du också vill ha autoifyllnad när du klickar på [TAB] så behöver du bara skriva följande kommando.
``` bash
echo "source \"$(realpath _fjarrstyr)\"" | sudo tee --append /etc/profile
```


## 4. Användning

``` bash
$ fjärrstyr --help

Användning:
fjärrstyr [server]
kommer att ansluta användaren till servern "[server]".

fjärrstyr -l
skriver ut en lista på sparade anslutningar.

fjärrstyr -h
visar det här hjälpfönstret.

Beroenden:
ssh, netcat, (konsole).

Beskrivning:
Programmet ansluter användaren till en vald server m.h.a. Secure Shell-
protokollet (SSH). Vid anslutning byts även färgtemat i användarens terminal
ut för att göra det lättare att se skillnad på terminalfönster.

Om terminalemulatorn Konsole används ändras färgemat till "SSH" vid anslutning
och återställs till "Breeze" vid slutföring.

Konfiguration:
Programmet letar efter sparade anslutningar i filen "$HOME/.fjärrstyr".

Filen ska följa följande mönster:
NAMN ANVÄNDARE SERVERADRESS

Exempel:
jobb_server ulf mittjobb.se
botnet4 root 84.221.147.159
speldator cspro91 192.168.1.42
```


## 5. Referens
+ [SSH (Secure Shell)](https://sv.wikipedia.org/wiki/Secure_Shell)
+ [Bash-komplettering](https://www.gnu.org/software/bash/manual/bash.html#Programmable-Completion)
