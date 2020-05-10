# DNMS
Digital Noise Measurement System, see https://luftdaten.info/einfuehrung-zum-laermsensor/. 

In Dec/2019 I worked on my frist DNMS and I had some difficulties. So I decide to supprt pepole with hints and material.

Im Dec/2019 habe ich mein erstes DNMS mit einigen Hürden erstellt. Um bastel-ungeübten Leuten auch die Möglichkeit zu geben an dem Lärm-Projekt teilzuhaben, habe ich mich entschlossen diese hier mit Tipps und Material zu unterstützen.

1. Mikrofon
- löten und vergießen ist nicht Jedermanns Sache
- von 300g Vergussmasse werden nur 15g benötigt
2. PCB's
- meistens müssen mind. 3...5 gekauft werden (~20€ BRD)
- Auslands-Bestellung dauren lange
- Bauteile, löten

Also wer bei dem Lärmprojekt mitmachen will, aber nicht basteln kann, kann bei mir per mail anfragen, ob ich Material bzw. fertige Teile verfügbar habe - s.a. ebay-Kleinanzeigen.

Bisher habe ich mehrere DNMS gebaut und abgegeben (Teensy3.6: T3.6 u. Airrohr, T3.6+NodeMCU und zwei T4.0 u. Airrohr)

Zur Funktion:
Das Mikro ICS-43434 mißt (35ms) die Schallpegelwerte und werden per I²S digital an den Teensy Prozessor übergeben, der berechnet LAeq/LAmin/LAmax (145s) und übergibt diese per I2C an das (Feinstaub-Wifi-) NodeMCU/ESP8226 ins Internet.
Die Teensy-LED flacket/leuchtet im Betrieb gelb.

Tipps:
- Vor dem Mikro Vergießen Funktion testen (hatte 3 Ausfälle von 19): Wareneingang / Löten /vergießen
- Holzbrett mit 13mm Löcher als Mikrohalterung
- Muffe für Verschraubung kann mit Heißluft selbst erzeugt werden (Föhn 180°C und Kupferrohr)
- Airrohr-Platine verwenden, verbessert Steckkontakte 
- Platz für Airrohr mit HT-Doppelmuffe DN75, 111mm
- Bei der Luftdaten.org Konfiguration den Lärm-SENSOR auswählen. Vermutlich sind bisher ID’s für SDS011(Feinstaub) und DHT22(t,RH) ausgewählt. Eine zusätzliche #ID (für DNMS, ggf. BME280) muß bei Rajko Zschiegner <rajko@codefor.de> per email angefragt werden. Leider geht das noch nicht anders. 
- bei madavi.de sind DNMS-Ärme Daten aktuell nicht verfügbar, s. archive.luftdaten.info
- Mikrofon-Kabel-Anschluss Belegung (I²S) von mir: 
    (3V3)=rot, (SCK)=blau, (Gnd)=schwarz;    (SD)=grün, (WS)=gelb, (L/R)=weiß
- Zum Schutz habe ich die Mikro‘s vorne mit einer Frischhaltefolie abgedeckt u. mit Tesa fixiert, Dämpfung ist aber 1-3dB. 
Meine Mikros betreibe ich ohne Folie ich achte darauf dass das Schallloch (sw Linie) bei Einbau oben ist und ziehe den Windschutz ~5mm zurück damit ein kleiner Freiraum vorhanden ist und Wasser nicht vor dem Schallloch steht. Ohne Folie sind die Werte auf ~1dB genau.


Links:
Einführung Lärmsensor: https://luftdaten.info/einfuehrung-zum-laermsensor/
Lärmsensor Bauanleitung: https://luftdaten.info/laermsensor-bauen/
Githib:https://github.com/hbitter/DNMS
Sensor Anmeldung ID: https://meine.luftdaten.info/
FeinstaubMap luftdaten.info  https://maps.sensor.community/#14/48.7759/9.1793  
Lärmkarte von Rainer: https://laerm.citysensor.de/map?sid=38366 
API-Dadten: https://api.luftdaten.info/static/v1/sensor/IDNR/
CSV-Daten: https://archive.luftdaten.info/2020-05-06/2020-05-06_laerm_sensor_IDNR.csv
Martin's interaktive Karte Überschreitungswerte: https://openmaps.online/noise/ 
Allg.Infos: https://blog.helmutkarger.de/category/projekte/feinstaubsensor/
Feinstaub messen: http://blog.bubux.de/feinstaub-messen-nodemcu-und-sds011/


