# Protocol
### Protocol Pferdefueranlage
### Version: 0.1.7

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
2.2.11 Liste von Pferden
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

| command  | id|
|-------------|:-----:|
| deletehorse | id vom Pferd |  

Antwort:

| command |
|-------------|
| deletehorse |

Beispiel:

C: {"command":"deletehorse","id":"2"}

S: {"command":"deletehorse"} 

Die Anweisung ist dafür da, um alle Daten über das Pferd zu bekommen.  

#### 2.2.4  Info Pferd

| command  | id |
|-------------|:-----:|
| infohorse | id vom Pferd |  

Antwort:

| command | id |name| time | turnaround | speed |
|-------------|:-----:|:---:|:---:|:---:|:---:|
| infohorse | id |Name | Traingszeit(s) | Anzahl der Drehrichtungsänderung | Geschwindigkeit |  

Beispiel:

C: {"command":"infohorse","id":"1"}

S: {"command":"infohorse","id":"1","name":"Franz","time":"500","turnaround":"5","speed":"5"} 

Die Anweisung ist dafür da, um alle Daten über das Pferd zu bekommen.  


#### 2.2.5 Pferd überarbeiten

| command | id |name| time | turnaround | speed |
|-------------|:-----:|:---:|:---:|:---:|:---:|
| infohorse | id |Name | Traingszeit(s) | Anzahl der Drehrichtungsänderung | Geschwindigkeit |  

Antwort:  

| command  |
|-----------|
|updatehorse|

Beispiel:

C: {"command":"updatehorse","id":"1","name":"Franz","time":"500","turnaround":"5","speed":"5"} 

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

| command | id |
|-------------|:-----:|
| start | Pferdeid |  

Antwort:  

| Anweisung  |
|-------------|
|start | 

Beispiel:

C: {"anweisung":"start","id":"1"} 

S: {"anweisung":"start"} 

Die Anweisung ist für den Anlagenstart da. Es wird der Name des schwächsten Pferdes übergeben. Die Parameter der Anlage werden auf dieses Pferd eingestellt und gestartet.  

#### 2.2.8 Maschine

| command | errors|
|-------------|:-----:|
| get | Fehler |  

Antwort:  

| Anweisung  | stop | water | time | turnaround | speed |
|-------------|:-----:|:-:|:-:|:-:|:-:|
| get | Stop | Water(on/off) | Trainingszeit |  Anzahl der Drehrichtungsänderung | Geschwindigkeit |  

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

C: {"command":"login"}

S: {"command":"login","password":"blabla"}

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

C: {"command":"version"}

S: {"command":"login","password":"blabla"}

Man bekommt die Version des Protokolls die ist zu überprüfen

#### 2.2.11 Liste der Pferde

| command |
|---------|
| all |

Antwort:

| command | names |
|-------------|:-:|
| all | Liste von Pferden |

Beispiel:  

C: {"command":"all"}

S: {"command":"all","names":[{"id":"1","name":"Lukas"},{"id":"2","name":"Lisa"},{"id":"3","name":"allli"}]}

Zum Anmelden


## Fehler  

| Code  | Funktion | beschreibung | Was passiert?|
| ------------- |:-------------:|:-----:|:--:|
|err01 | Timeout Error | Wenn ein Client oder der Server innerhalb des Timeouts keine Rücklmeldung mehr gibt kommt es zu einem Timeout Error| Maschiene wird ausgeschalten |
|err02 | Database not rechable | Datenbank kann nicht erreicht werden | Fehlermeldung an den Client |
|err03 | Telegram fehlerhaft | Das Telergramm vom Server/Client ist fehlerhaft | Der Fehler wird an den Client geschickt und es wird vom Sender verlangt, es erneut zu senden |  
