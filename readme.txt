Update: vind je home automation vet? Check dan zeker mijn Kickstarter project: een spraakgestuurd huis! http://kck.st/1jsMmvq


Home Automation is een opkomend én gaaf verschijnsel, en om het leven van jullie Tweakers wat makkelijker te maken heb ik hier een tutorial hoe je bepaalde merken stekkerdozen draadloos kan schakelen met een Raspberry Pi!

Deze tutorial werkt met de volgende merken: KlikAanKlikUit, Action, Blokker en Elro. Wellicht met meer omdat vaak dezelfde chips worden gebruikt, dus zeker het proberen waard!
Benodigdheden
Raspberry Pi
Een 433MHz/434MHz transmitter (o.a. te koop op eBay of iPrototype)
Wat draadjes om de transmitter aan je Raspberry Pi te verbinden. Een oude floppy kabel is in theorie voldoende, maar ik geef de voorkeur aan female jumper wires
Ik ga er van uit dat je je Raspberry Pi al werkend hebt met een degelijke linux distro, en weet hoe je met een terminal overweg kan. Ik gebruik Raspbian.
Stappenplan
Stap 1 - Sluit alles aan
VCC van de transmitter op pin 4 van je Pi (VCC 5V)
GND van de transmitter op pin 6 van je Pi (GND)
ATAD of DATA van de transmitter op pin 8 van je Pi (TX)
Zo moet het er uitzien:
http://i.imgur.com/QW0UqfYl.jpg
Stap 2 - Installeer WiringPi
WiringPi is een prachtige library die veel arduino functionaliteit naar de Raspberry Pi port. Omdat ik de draadloze library van een Arduino naar de Pi heb geport, heb je deze library dus ook nodig.

Als je git nog niet hebt, installeer dat dan via:

code:
1
2
3
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git-core


Daarna gaan we WiringPi downloaden en builden:

code:
1
2
3
4
5
git clone git://git.drogon.net/wiringPi
cd wiringPi
git pull origin
cd wiringPi
./build


Als alles goed gaat, heb je nu WiringPi geinstalleerd en kun je mijn code downloaden!
Stap 3 - Installeer het tooltje
Voer deze code uit:

code:
1
2
3
4
cd examples
wget -O lights.zip https://www.dropbox.com/s/nxdrkuk94w9fpqo/lights.zip?dl=1
unzip lights.zip
cd lights


Compileer nu de versie die jij nodig hebt:

KlikAanKlikUit
code:
1
g++ -o kaku kaku.cpp -I/usr/local/include -L/usr/local/lib -lwiringPi


Action
code:
1
g++ -o action action.cpp -I/usr/local/include -L/usr/local/lib -lwiringPi


Blokker
code:
1
g++ -o blokker blokker.cpp -I/usr/local/include -L/usr/local/lib -lwiringPi


Elro
code:
1
g++ -o elro elro.cpp -I/usr/local/include -L/usr/local/lib -lwiringPi


Nu kun je het zojuist gecompileerde tooltje uitvoeren om je lampen te schakelen! Bijvoorbeeld:

code:
1
sudo ./action 18 C on


Voor de andere merken, voer sudo ./merk uit voor het juiste gebruik. (sudo is nodig omdat de GPIO pin low-level zijn)
Optionele stap 4 - Tweaken
Bereik optimaliseren
Als je moeite hebt met het schakelen, is waarschijnlijk het bereik te klein. Dit heeft meestal drie oorzaken:
De ontvanger zit in de buurt van veel electronica: verplaats deze naar een wat 'rustigere' plek
Maak de antenne van de transmitter langer
Boost het vermogen van de transmitter naar maximaal 12V door die twee pinnen op een externe adapter aan te sluiten
Ontvanger
Ook kun je met de broncode aan de slag om de functionaliteiten uit te bouwen. Voor de originele Arduino library klik hier. Een receiver aankoppelen zou niet al te moeilijk moeten zijn!
Webserver
Koppel dit tooltje aan bijvoorbeeld een PHP of Node.js server om via je browser of smartphone je lampen te schakelen met een mobiele website, NFC tags bij de deur, Wi-Fi detectie.. you name it! :D

Update: Lampen schakelen met je smartphone & een Raspberry Pi

Credits gaan vooral naar Randy Simons voor zijn library RemoteSwitch ;) 

Reacties vind ik heel leuk! O+