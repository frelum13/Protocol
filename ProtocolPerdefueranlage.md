# Protocol
### Protocol Pferdefiueranlage

## Zeitplan
1. Kommunikationsmanagment  
2. Telegram  
2.1 Allgemeine Form der Telegramme  
2.2 Funktionen  
2.3 Beispiele von Telegrammen  
3. Fehler  

## 1. Kommunikationsmanagment  

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
| Code  | Funktion | Beispiel |
| ------------- |:-------------:|-----:|
|water| Water on/off | Um das Wasser ein und aus zu schalten | 
| deletehorse | Pferd löschen | Um ein Pferd aus der Datenbank zu löschen |
| deleteuser | Benutzer löschen | Um ein User aus der Datenbank zu löschen|
| infohorse | Info Pferd | Schickt alle Datenbankeinträge über dieses Pferd an den Client|
| infouser | Info Benutzer | Schickt alle Datenbankeinträge über diesen User an den Client|
| updatehorse | Pferd überarbeiten | Bekommt Daten vom Client die in der Datenbank verändert werden sollen|
| updateuser | Benutzer überarbeiten | Bekommt Daten vom Client die in der Datenbank verändert werden sollen|


### 2.3 Beispiele von Telegrammen  

## Fehler  

| Code  | Funktion | beschreibung |
| ------------- |:-------------:|:-----:|
|err01 | Timeout Error | Wenn ein Client oder der Server innerhalb des Timeouts keine Rücklmeldung mehr gibt kommt es zu einem Timeout Error| 
