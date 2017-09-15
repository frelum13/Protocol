# Protocol
### Protocol Pferdefiueranlage

1.) Kommunikationsmanagment  
2.) Telegramme  
2.1) Allgemeine Form der Telegramme  
2.2) Funktionen  
2.3) Beispiele von Telegrammen  
3.) Fehler  


Freyler: Server  
Pölzl: Client  
Riegelnegg: Client  

// todo Bild   
  
Wir arbeiten über das Ethernet (WLan)

Wir arebiten mit einer Verbindungsorientierte Verbindung  

Fehler:
- Bei keiner Antwort von 100 ms wird das das Telegramm erneut versendet
- Wenn das Telegram fehlerhaft sein sollte wird eine Response gesendet der den Sender aufvordert um das Telegram erneut zu versenden         oder Richtig zu stellen
