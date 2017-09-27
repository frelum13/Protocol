# Protocol
### Protocol Pferdefiueranlage
### Version: 1.0.5

## Zeitplan
1. Kommunikationsmanagment  
1.1 Zweck  
1.2 Protocol Daten  
2. Telegram  
2.1 Allgemeine Form der Telegramme  
2.2 Funktionen  
2.2.1 Wasser  
2.2.2 Neues Pferd hinzufügen  
2.2.3 Benutzer Registrieren  
2.2.4 Pferd löschen  
2.2.5 Benutzer löschen  
2.2.6 Info Pferd  
2.2.7 Info Benutzer  
2.2.8 Pferd überarbeiten  
2.2.9 Benutzer überarbeiten  
2.2.10 Stop  
2.2.11 Status  
2.2.12 Start  
2.2.13 Anlage  
2.3 Beispiele von Telegrammen  
3. Fehler  

## 1. Kommunikationsmanagment  
### 1.1 Zweck
Zweck dieses Protokolls ist es das eine Android App über TCP/IP mit einem Datenbankserver komunizieren kann. Ein zweiter Client kann auf den Datenbankserver zugreifen und die Daten abfragen die auf der Datenbank abgekegt sind um die Anlaga zu starten. Der Server und die Clients bleiben im regelmäßigen Kontakt. Das Timeout beträgt bei dieser Verbindung 100ms wird eine Ausgelößt bleibt die Anlage sofort stehen.

### 1.2 Protocol Daten
Es ist TCP/IP Protokoll was über das Ethernet funktioniert. Außerdem ist es ein Texorientiertes Zustandsloses Protokoll.


## 2. Telegram  

### 2.1 Allgemeine Form der Telegramme  

| Anweisung  | Daten |
| ------------- |:-------------:|
|Code | Daten | 
  
Beispiel:  

| Anweisung  | Daten |
| ------------- |:-------------:|
|water | on | 
  
Dieser String wird dann in json zusammengesetzt und versendet

### 2.2 Funktionen  

#### 2.2.1 Wasser an/aus
| Anweisung  | Daten|
|-------------|:-----:|
|water| Wasser on/off |  

Antwort:

| Anweisung  | Daten|
|-------------|:-----:|
|water| true/false |  

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
|water| on |

Die Anweisung ist dafür da um die Wassersprühanlage ein oder aus zu schalten.  

#### 2.2.2 Neues Pferd hinzufügen

| Anweisung  | Daten|
|-------------|:-----:|
| new | Name + Trainigszeit(s) + Anzahl der Drehrichtungsänderungen | 

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
|new | true/false | 

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| new | Franz + 500 + 4 |  

Es ist dafür da um einen neues Pferd in die Datenbank zu schreiben

#### 2.2.3 Benutzer Registrieren

| Anweisung  | Daten|
|-------------|:-----:|
| registrate | Vorname + Nachname + Benutzername + Passwort |  

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
|registrate| true/false | 

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| registrate | Franz + 500 + 4 |

Es ist dafür da um einen neuen Beutzer in die Datenbank hinzuzufügen.

#### 2.2.4 Pferd löschen  
| Anweisung  | Daten|
|-------------|:-----:|
| deletehorse | Name |  

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
|deletehorse| true/false | 

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| deletehorse | Franz |  

Um ein Pferd aus der Datenbank zu löschen.  

#### 2.2.5 Benutzer löschen

| Anweisung  | Daten|
|-------------|:-----:|
| deleteuser | Benutzername |  

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
|registrate| true/false |

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| deleteuser | Lukas123 |  

Um einen Benutzer aus der Datenbank zu löschen.  

#### 2.2.6  Info Pferd

| Anweisung  | Daten|
|-------------|:-----:|
| infohorse | Name vom Pferd |  

Antwort:

| Anweisung  | Daten|
|-------------|:-----:|
| infohorse | Name + Traingszeit(s) + Anzahl der Drehrichtungsänderung |  

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| infohorse |  Franz |  

Um alle Daten über das Pferd zu bekommen.  

#### 2.2.7 Info Benutzer

| Anweisung  | Daten|
|-------------|:-----:|
| infouser | Benutzername |

Antwort:
| Anweisung  | Daten|
|-------------|:-----:|
| infouser | Vorname + Nachname + Benutzername + Passwort |  

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| infouser | Lukas123 |  

Um alle Daten von einem Benutzer zu bekommen

#### 2.2.8 Pferd überarbeiten

| Anweisung  | Daten|
|-------------|:-----:|
| updateuser |  Name + Trainigszeit(s) + Anzahl der Drehrichtungsänderungen |  

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
|updateuser| true/false |

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| updateuser | Lukas123 |  

Server erhaltet neue Daten von einem Pferd die in der Datenbank ausgetauscht werden.

#### 2.2.9 Benutzer überarbeiten

| Anweisung  | Daten|
|-------------|:-----:|
| updateuser | Benutzername |  

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
|updateuser| true/false |  

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| updateuser | Lukas123 |  

Server erhält neue Daten von einem Benutzer die in der Datenbank ausgetauscht werden.

#### 2.2.10 Stop

| Anweisung  | Daten|
|-------------|:-----:|
| stop | Art des stops |  

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
|stop| true/false |  

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| stop | hardstop |  

Die Anweisung ist dafür wie der Benutzer die Maschine Stoppen will (z.B. Notstop, Pausieren).

Weitere Arten von Stopps:

#### 2.2.11 Status

| Anweisung  | Daten|
|-------------|:-----:|
| status |  |  

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
|status | Fehler |  

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| status |  |  

Die Anweisung ist dafür da, dass das Handy und der Server im Regelmäßigen Kontakt bleiben wenn igrgendein Fehler auftritt das der Benutzer reagieren kann.  

#### 2.2.12 Start

| Anweisung  | Daten|
|-------------|:-----:|
| start | Pferdename |  

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
|start | true/false |  

Beispiel:

| Anweisung  | Daten|
|-------------|:-----:|
| start | Franz |  

Die Anweisung ist für den Anlagenstart da. Es wird der Name von dem schwächsten Pferd übergeben und die anlage dann auf das gestartet.  

#### 2.2.13 Anlage

| Anweisung  | Daten|
|-------------|:-----:|
| get | Fehler |  

Antwort:  

| Anweisung  | Daten|
|-------------|:-----:|
| get | Water(on/off) + Trainingszeit +  Anzahl der Drehrichtungsänderung|   

Beispiel

| Anweisung  | Daten|
|-------------|:-----:|
| get | err01 |  

Die Anweisung ist dafür da um im stetigen Kontakt mit der Anlage zu sein, um die Anlage zu starten(wasser auch) und gegebenfalls Fehler von der Anlage abzufragen.  

## Fehler  

| Code  | Funktion | beschreibung | Was passiert?|
| ------------- |:-------------:|:-----:|:--:|
|err01 | Timeout Error | Wenn ein Client oder der Server innerhalb des Timeouts keine Rücklmeldung mehr gibt kommt es zu einem Timeout Error| Maschiene wird ausgeschalten |
|err02 | Database not rechable | Datenbank kann nicht erreicht werden | Fehlermeldung an den Client |
|err03 | Telegram Fehlerhaft | Das Telergramm vom Server/Client ist fehlerhaft | Der Fehler wird an den Client geschickt und es wird vom Sender verlangt es erneut zu senden |  
