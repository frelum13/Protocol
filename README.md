# Protocol
### Protocol Pferdefiueranlage
### Version: 1.0.5

## Inhaltsangabe
1. Kommunikationsmanagment  
1.1 Zweck  
1.2 Protocol Daten  
2. Telegram  
2.1 Allgemeine Form der Telegramme  
2.2 Funktionen  
2.2.1 Wasser  
2.2.2 Neues Pferd hinzufügen    
2.2.3 Pferd löschen    
2.2.4 Info Pferd  
2.2.5 Pferd überarbeiten   
2.2.6 Stop  
2.2.7 Start  
2.2.8 Machine
2.2.9 Login
2.2.10 Version
3. Fehler  

## 1. Kommunikationsmanagment  
### 1.1 Zweck
Zweck dieses Protokolls ist es, dass eine Android App über TCP/IP mit einem Datenbankserver kommunizieren kann. Ein zweiter Client, kann auf den Datenbankserver zugreifen und die Daten abfragen, die auf der Datenbank abgelegt sind, um die Anlage zu starten. Der Server und die Clients bleiben im regelmäßigen Kontakt. Das Timeout beträgt bei dieser Verbindung 100ms, wird eine ausgelöst bleibt die Anlage sofort stehen.

### 1.2 Protocol Daten
Es ist ein Verbindungsorientiertes TCP/IP Protokoll was über das Ethernet funktioniert. Außerdem ist es ein Texorientiertes Zustandsloses Protokoll. Das Port über das dieses Protokoll komuniziert ist "1111".


C = Client  
S = Server

## 2. Telegram  

### 2.1 Allgemeine Form der Telegramme  

| Command  | Daten |
| ------------- |:-------------:|
|command | Daten | 

Dieser String wird dann in json zusammengesetzt und versendet
  
Beispiel:  

{"command":"water","water":true}
  


### 2.2 Funktionen  

#### 2.2.1 Wasser an/aus
| Anweisung  | Daten|
|-------------|:-----:|
|water| Wasser true/false |  

Antwort:

| Anweisung  | Daten|
|-------------|:-----:|
|water| true/false |  

Beispiel:

C: {"anweisung":"water","water":true}

S: {"anweisung":"water"}

Die Anweisung ist dafür da, um die Wassersprühanlage ein oder auszuschalten.  

#### 2.2.2 Neues Pferd hinzufügen

| Command  |name | time| trunaround| speed|
|-------------|:-----:|--:|--:|--:|
| new | Pferdname | Trainigszeit(s) | Anzahl der Drehrichtungsänderungen | Geschwindigkeit|

Antwort:  

| Command | 
|-------------|
|new | 

Beispiel:

C: {"command":"new","name":"Franz","time":"500","turnaround":"5","speed":"5"} 

S: {"command":"new"}

Sie ist dafür da, um ein neues Pferd in die Datenbank zu schreiben

#### 2.2.3  Pferd löschen

| command  | Name|
|-------------|:-----:|
| deletehorse | Name vom Pferd |  

Antwort:

| command |
|-------------|
| deletehorse |

Beispiel:

C: {"command":"deletehorse","name":"Franz"}

S: {"command":"deletehorse"} 

Die Anweisung ist dafür da, um alle Daten über das Pferd zu bekommen.  

#### 2.2.4  Info Pferd

| command  | Name|
|-------------|:-----:|
| infohorse | Name vom Pferd |  

Antwort:

| command | name| time | turnaround | speed |
|-------------|:-----:|:---:|:---:|:---:|
| infohorse | Name | Traingszeit(s) | Anzahl der Drehrichtungsänderung | Geschwindigkeit |  

Beispiel:

C: {"command":"infohorse","name":"Franz"}

S: {"command":"infohorse","name":"Franz","time":"500","turnaround":"5","speed":"5"} 

Die Anweisung ist dafür da, um alle Daten über das Pferd zu bekommen.  


#### 2.2.5 Pferd überarbeiten

| command  | name | time | turnaround | speed |
|-------------|:-----:|:---:|:---:|:---:|
| updatehorse |  Pferdname | Trainigszeit(s) | Anzahl der Drehrichtungsänderungen |  Geschwindigkeit|

Antwort:  

| command  |
|-----------|
|updatehorse|

Beispiel:

C: {"command":"updatehorse","name":"Franz","time":"500","turnaround":"5","speed":"5"} 

S: {"command":"updatehorse"} 

Server erhält neue Daten von einem Pferd, die in der Datenbank ausgetauscht werden.


#### 2.2.6 Stop

| command | stop |
|-------------|:-----:|
| stop | Art des stops |  

Antwort:  

| command |
|-------------|
|  stop  | 

Beispiel:

C: {"anweisung":"stop","stop":"stop"} 

S: {"anweisung":"stop"} 

Die Anweisung ist dafür, wie der Benutzer die Maschine stoppen kann (z.B. Notstop, pausieren).

Weitere Arten von Stopps:

    - stop
    - break

#### 2.2.7 Start

| command | name |
|-------------|:-----:|
| start | Pferdename |  

Antwort:  

| Anweisung  |
|-------------|
|start | 

Beispiel:

C: {"anweisung":"start","name":"Franz"} 

S: {"anweisung":"start"} 

Die Anweisung ist für den Anlagenstart da. Es wird der Name des schwächsten Pferdes übergeben. Die Parameter der Anlage werden auf dieses Pferd eingestellt und gestartet.  

#### 2.2.8 Machine

| command | errors|
|-------------|:-----:|
| get | Fehler |  

Antwort:  

| Anweisung  | stop | water |name | time | turnaround | speed |
|-------------|:-----:|:-:|:-:|:-:|:-:|:-:|
| get | Stop | Water(on/off) | Pferdname |Trainingszeit |  Anzahl der Drehrichtungsänderung | Geschwindigkeit |  

Beispiel

C: {"command":"get","error":"er01"} 

S: {"command":"get","water":"nothing","water":"on","name":"Franz","time":"400","5"]} 

Die Anweisung ist dafür da um im stetigen Kontakt mit der Anlage zu sein, um die Anlage zu starten(Wasser auch) um gegebenfalls Fehler von der Anlage abzufragen.  

#### 2.2.9 Login

| command |
|---------|
| login |

Antwort:

| command | Password |
|-------------|:-:|
| login | Passwort |

Beispiel:  

C: {"anweisung":"login"}

S: {"anweisung":"login","password":"blabla"}

Zum Anmelden

#### 2.2.10 Version

| command |
|---------|
| version |

Antwort:

| command | version |
|-------------|:-:|
| version | Version |

Beispiel:  

C: {"anweisung":"login"}

S: {"anweisung":"login","password":"blabla"}

Zum Anmelden

## Fehler  

| Code  | Funktion | beschreibung | Was passiert?|
| ------------- |:-------------:|:-----:|:--:|
|err01 | Timeout Error | Wenn ein Client oder der Server innerhalb des Timeouts keine Rücklmeldung mehr gibt kommt es zu einem Timeout Error| Maschiene wird ausgeschalten |
|err02 | Database not rechable | Datenbank kann nicht erreicht werden | Fehlermeldung an den Client |
|err03 | Telegram fehlerhaft | Das Telergramm vom Server/Client ist fehlerhaft | Der Fehler wird an den Client geschickt und es wird vom Sender verlangt, es erneut zu senden |  
