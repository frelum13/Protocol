# Protocol
### Protocol Pferdefiueranlage
### Version: 1.0.5

## Zeitplan
1. Kommunikationsmanagment  
2. Telegram  
2.1 Allgemeine Form der Telegramme  
2.2 Funktionen  
2.2.1 Wasser  
2.2.2 Neues Pferd hinzufügen  
2.2.3 Benutzer Registrieren  
2.2.4 Pferd löschen  
2.2.5 Benutzer löschen  
2.3 Beispiele von Telegrammen  
3. Fehler  

## 1. Kommunikationsmanagment  
Es ist ein Kommunikationsprotokoll auf TCP/IP. 


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

Beispiel

| Anweisung  | Daten|
|-------------|:-----:|
|water| on |

Die Anweisung ist dafür da um die Wassersprühanlage ein oder aus zu schalten.  

#### 2.2.2 Neues Pferd hinzufügen

| Anweisung  | Daten|
|-------------|:-----:|
| new | Name + Traingszeit(s) + Anzahl der Drehrichtungsänderung |

Beispiel

| Anweisung  | Daten|
|-------------|:-----:|
| new | Franz + 500 + 4 |  

Es ist dafür da um einen neues Pferd in die Datenbank zu schreiben

#### 2.2.3 Benutzer Registrieren

| Anweisung  | Daten|
|-------------|:-----:|
| registrate | Vorname + Nachname + Benutzername + Passwort |

Beispiel

| Anweisung  | Daten|
|-------------|:-----:|
| registrate | Franz + 500 + 4 |

Es ist dafür da um einen neuen Beutzer in die Datenbank einzufügen

#### 2.2.4 Pferd löschen  
| Anweisung  | Daten|
|-------------|:-----:|
| deletehorse | Name |

Beispiel

| Anweisung  | Daten|
|-------------|:-----:|
| deletehorse | Franz |  

Um ein Pferd aus der Datenbank zu löschen.  

#### 2.2.5 Benutzer löschen

| Anweisung  | Daten|
|-------------|:-----:|
| deleteuser | Benutzername |

Beispiel

| Anweisung  | Daten|
|-------------|:-----:|
| deleteuser | Lukas123 |  

#### 2.2.6  Info Pferd

| Anweisung  | Daten|
|-------------|:-----:|
| deleteuser | Benutzername |

Beispiel

| Anweisung  | Daten|
|-------------|:-----:|
| deleteuser | Lukas123 |  

#### 2.2.7 Info Benutzer

| Anweisung  | Daten|
|-------------|:-----:|
| deleteuser | Benutzername |

Beispiel

| Anweisung  | Daten|
|-------------|:-----:|
| deleteuser | Lukas123 |  

#### 2.2.8 Pferd überarbeiten
#### 2.2.9 Benutzer überarbeiten
#### 2.2.10 Stop
#### 2.2.11 status
#### 2.2.12 start
#### 2.2.13 get
## Fehler  

| Code  | Funktion | beschreibung | Was passiert?|
| ------------- |:-------------:|:-----:|:--:|
|err01 | Timeout Error | Wenn ein Client oder der Server innerhalb des Timeouts keine Rücklmeldung mehr gibt kommt es zu einem Timeout Error| Maschiene wird ausgeschalten |
|err02 | Database not rechable | Datenbank kann nicht erreicht werden | Fehlermeldung an den Client |
|err03 | Telegram Fehlerhaft | Das Telergramm vom Server/Client ist fehlerhaft | Der Fehler wird an den Client geschickt und es wird vom Sender verlangt es erneut zu senden |  
