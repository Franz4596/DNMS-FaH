# DNMS
Digital Noise Measurement System, see https://github.com/hbitter/DNMS. 

In Dec/2019 I worked on my frist DNMS and I had some difficulties. So I decide to supprt pepole with hints and material.

Im Dez/2019 habe ich mein erstes DNMS mit einigen Hürden erstellt. Um bastel-ungeübten Leuten auch die Möglichkeit zu geben an dem Lärm-Projekt teilzuhaben, habe ich mich entschlossen diese hier mit Tipps und Material (auf Anfrage) zu unterstützen. 
Hürden:
1. Mikrofon
- löten und vergießen ist nicht Jedermanns Sache
- von 300g Vergussmasse (28€) werden nur 15g für ein Mikro benötigt
2. PCB's
- meistens müssen mind. 3...5 gekauft werden (~20€ in EU)
- Auslands-Bestellung dauert ggf. lange, Zoll-Handling 
- Bauteile besorgen, löten

Also wer bei dem Lärmprojekt mitmachen will, aber nicht basteln kann, kann bei mir per mail anfragen, ob ich Material bzw. fertige Teile verfügbar habe - s.a. ebay-Kleinanzeigen.

Bisher habe ich mehrere DNMS gebaut und abgegeben (Teensy3.6 u. Airrohr, T3.6+NodeMCU sowie Teensy4.0)

# Zur Funktion:
Das Mikro ICS-43434 mißt kontinuierlich (35ms Intervall) die Schallpegelwerte und werden per I²S digital an den Teensy Prozessor übergeben, der berechnet die A-bewerteten Schallpegel LAeq/LAmin/LAmax und übergibt diese (145s) per I2C an das (Feinstaub-Wifi-) NodeMCU/ESP8226 ins Internet an sensor.community.
Die Teensy-LED flacket/leuchtet im Betrieb gelb.

# Tipps:
- Vor dem Mikro Vergießen dessen Funktion testen (hatte 3 Ausfälle von 19): Wareneingang / Löten /vergießen
- Holzbrett mit ~13mm Löcher als Mikrohalterung als Ständer zum Vergiesen 
- Muffe für Verschraubung kann aus DN Rohr mit Heißluft selbst erzeugt werden (Föhn 180°C/380°C und Kupferrohr)
- Airrohr-Platine verwenden, verbessert Steckkontakte (anstatt Dupont Kabel)
- Platz für Airrohr-PCB mit Huckepack verschraubten SDS011 in HT-Doppelmuffe DN75, 111mm
- Bei der sensor.community (früher Luftdaten.org) Konfiguration den Lärm-SENSOR auswählen. Vermutlich sind bisher ID’s für SDS011(Feinstaub) und DHT22(t,RH) ausgewählt. Eine zusätzliche #ID (für DNMS, ggf. BME280) muß bei Rajko Zschiegner <rajko@codefor.de> per email angefragt werden. Leider geht das noch nicht anders. 
- bei madavi.de sind DNMS-Lärm Daten aktuell nicht verfügbar, s. archive.luftdaten.info
- Mikrofon-Kabel-Anschluss Belegung (I²S), Farbcode von mir: 
    (3V3)=rot, (SCK)=blau, (Gnd)=schwarz;    (SD)=grün, (WS)=gelb, (L/R)=weiß
- Zum Schutz des Mikrofonloches habe ich die Mikro‘s vorne mit einer Frischhaltefolie abgedeckt u. mit Tesa fixiert, Dämpfung ist aber ~1dB. 
Meine Mikros betreibe ich ohne Folie ich achte darauf dass das Schallloch (sw Linie) bei Einbau oben ist und ziehe den Windschutz ~5mm zurück damit ein kleiner Freiraum vorhanden ist und Wasser nicht vor dem Schallloch steht. Ohne Folie sind die Werte auf ~1dB genau.
- bei mir hat ein Vogel in den schwarzen Windschutz Löcher gepickt


# Links:  
Einführung Lärmsensor: https://luftdaten.info/einfuehrung-zum-laermsensor/  
Lärmsensor Bauanleitung: https://luftdaten.info/laermsensor-bauen/  
Github Doku, Beschreibung, PCBs,...: https://github.com/hbitter/DNMS  
Sensor Anmeldung ID: https://devices.sensor.community  (früher https://meine.luftdaten.info) 
FeinstaubMap luftdaten.info  https://maps.sensor.community/#14/48.7759/9.1793  
Lärmkarte von Rainer: https://laerm.citysensor.de/map?sid=38366  
API-Daten: https://api.luftdaten.info/static/v1/sensor/IDNR/  
CSV-Daten: https://archive.luftdaten.info/2020-05-06/2020-05-06_laerm_sensor_IDNR.csv  
Martin's interaktive Karte Überschreitungswerte: https://openmaps.online/noise/  
Allg.Infos: https://blog.helmutkarger.de/category/projekte/feinstaubsensor/   
Feinstaub messen: http://blog.bubux.de/feinstaub-messen-nodemcu-und-sds011/ 
meine Infos: https://github.com/Franz4596/DNMS-FaH


# wie Platinen kaufen:  
Gebe einzelne Platinen für 0,60€/Stk+Porto an Bastler ab <franz.hoefle(a)buergerforum-gladbeck.de>. 
Größere Anzahl bitte selbst bestellen:  
1. von https://github.com/hbitter/DNMS <Code> <Download ZIP>  zip runterladen: "https://github.com/hbitter/DNMS/archive/master.zip"
2. entzippen, Gerber-Datei steht in entsprechendem Verzeichnis:  C:\...\PCBs\DNMS-????\???.???-Gerber.zip  
3. Shop/Homepage des PCB-Verkäufers aufrufen z.B. jlcpcb.com oder dirtypcbs.com (10Stk ~30€) oder aisler.net(3Stk ~25€) oder ...  
4. Gerber-Datei hochladen: Menü Leiterplatten "online kalkulieren" oder "berechnen" oder "File" 
5. Kontrollieren, Kaufabwicklung abschließen    
    
