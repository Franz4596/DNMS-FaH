# DNMS
Digital Noise Measurement System, see https://github.com/hbitter/DNMS. 

In Dec/2019 I worked on my frist DNMS and I had some difficulties. So I decide to support here pepole with hints and material.

Im Dez/2019 habe ich mein erstes DNMS mit einigen Hürden erstellt. Um bastel-ungeübten Leuten auch die Möglichkeit zu geben an dem Lärm-Projekt teilzuhaben, habe ich mich entschlossen diese hier mit Tipps und Material (auf Anfrage) zu unterstützen. 


# Allgemein:
Das DNMS ist eine Schallpegel-Sensor Ergänzung zum Feinstaub-Projekt. Es gibt zwei Platinen-Varianten (2010-09-27_DNMS-Schema.jpg)
1. DNMS und Airrohr: Das Mikro am 25mm Rohr wird mit einem Kabel an das Feinstaub-Gerät in DN75-Bögen angeschlossen. Dabei wird die Airrohplatine unter den SDS011 plaziert (2020-01-18_DNMSHauseck.jpg). 
2. DNMS+NodeMCU: Das Mikro wird an ein DN40 Rohr montiert, sinnvoll wenn kein SDS011 verwendet werden soll (2020-10-09_DNMS-T4NodeMCU.jpg).

Inzwischen gibt es ein etwas besseres Miko IM72D128, es wird von watterott zu einem annehmbaren Preis verkauft:
https://shop.watterott.com/Mikrofon-IM72D128V01-im-127mm-Rundrohr bzw. https://shop.watterott.com/Mikrofon-IM72D128V01-Platine-mit-Anschlussleitung

Das Zusammenstecken, ESP8266 u. Teensy Flashen ist für die meisten Leute machbar, Hürden sind:
1. Mikrofon 
- löten und vergießen ist nicht Jedermanns Sache, alternativ s. watterrott
- von 300g Vergussmasse (28€) werden nur 12g für ein Mikro benötigt, und es muss mind. 25g (3 Mikros) angesetzt werden.
- Beschaffung des ICS43434-Breackouts bei Tindy bzw SensorMasters in USA umständlich (Zoll) und teuer (15€)
- Z.Zt. wird ein neuer etwas besserer Mikrofontyp (niedriger Pegel, wetterfester) IM72D128 getestet.  
2. PCB's
- meistens müssen mind. 3...5 gekauft werden (~20€ in EU)
- Auslands-Bestellung dauert ggf. lange, Zoll-Handling 
- Bauteile besorgen, löten

Also wer bei dem Lärmprojekt mitmachen will, aber nicht basteln kann, kann bei mir per mail anfragen, ob ich Material bzw. fertige Teile verfügbar habe - s.a. Kleinanzeigen.de DNMS.

Ich habe bisher viele Platinen u. Breakouts abgegeben und mehrere DNMS gebaut (DNMS mit Airrohr, DNMS+NodeMCU), betreibe das als Hobby und will kein Gschäft daraus machen. Also wer mithelfen will gerne bitte melden.  

# Zur Funktion:
Das Mikro ICS-43434 bzw. IM72D128 mißt kontinuierlich (35ms Intervall) die Schallpegelwerte und werden per I²S digital an den Teensy Prozessor übergeben, der berechnet die A-bewerteten Schallpegel LAeq/LAmin/LAmax und übergibt diese (145s) per I2C an das (Feinstaub-Wifi-) NodeMCU/ESP8226 ins Internet an sensor.community.
Die Teensy-LED flacket/leuchtet im Betrieb gelb.

# Tipps:
- Vor dem Mikro in Rohr vergießen dessen Funktion testen (hatte 15% Ausfälle): Wareneingang / Löten /vergießen
- Holzbrett mit ~13mm Löcher als Mikrohalterung als Ständer zum Vergiesen verwenden
- Das Vergußharz muss vor abwiegen gründlich aufgerührt werden (Bodensatz)  
- andere / ähnliche Vergussmassen können auch vervendet werden
- Muffe für Verschraubung kann aus DN Rohr mit Heißluft selbst erzeugt werden (Föhn 180°C/380°C und mit Kupferrohr aus Sanitärbereich weiten)
- Bei Feinstaub SDS011 Airrohr-Platine verwenden, verbessert Steckkontakte (anstatt Dupont Kabel)
- Airrohr-PCB mit Huckepack verschraubten SDS011 passt in Feinstaub-DN75-Bögen, ggf. HT-Doppelmuffe DN75, 111mm, zwischensetzen
- Bei der sensor.community (früher Luftdaten.org) Konfiguration den Lärm-SENSOR auswählen. Vermutlich sind bisher ID’s für SDS011(Feinstaub) und DHT22(t,RH) ausgewählt. Eine zusätzliche #ID (für DNMS, ggf. BME280) muß bei erster Konfig oder ggf. bei Rajko Zschiegner <rajko@codefor.de> per email angefragt werden. Leider geht das noch nicht anders. 
- bei madavi.de sind DNMS-Lärm Daten ab Feb.2020 auch verfügbar (Log.Skala war mal falsch), s. http://archive.sensor.community (früher:archive.luftdaten.info)
- Mikrofon-Kabel-Anschluss Belegung (I²S), Farbcode von mir: 
    (3V3)=rot, (SCK)=blau, (Gnd)=schwarz;    (SD)=grün, (WS)=gelb, (L/R)=weiß
- Zum Schutz des Mikrofonloches habe ich die Mikro‘s vorne mit einer Frischhaltefolie abgedeckt u. mit Tesa fixiert, Dämpfung ist aber >0,5dB. 
Meine Mikros betreibe ich nur mit Folie, wenn der Messwerte nicht exakt sein braucht. Ich achte darauf, dass in das Schallloch kein Wasser/Schnutz eintritt, also ziehe den Windschutz ~5mm zurück damit ein kleiner Freiraum vorhanden ist und Wasser nicht vor dem Schallloch steht. Ohne Folie sind die Werte auf ~1dB genau.
Reflexionen von Wand, Dach können Schallpegelwert beeinflussen.
- bei mir hat ein Vogel in den schwarzen Windschutz Löcher gepickt, ggf. 5cm Drahtstücke halten Vögel ab drauf zu sitzen. 

# Messwerte, Frequenzanalyse:  
Bisher wurde "nur" das Zeitsignal ausgewertet (LAeq, LAmin, LAmax). Inzwischen hat Helmut B. eine FFT (FastFourierTransform) zur Umrechnung des Zeitsignals in ein Frequenzspektrum realisiert. Das Terzspektrum umfasst 32 Werte und wird NICHT an madavi, sensor.community übermittelt, wird lokal (192.168.178.?values) angezeigt, ggf. per InfluDB/MQTT speichern, näheres s. github.com/hbitter/DNMS.

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
Ich gebe einzelne Platinen für 1.50€/Stk +Porto an Bastler ab <franz.hoefle(a)buergerforum-gladbeck.de>, 
oder größere Anzahl ggf. selbst bestellen:  
1. von https://github.com/hbitter/DNMS <Code> <Download ZIP>  zip runterladen: "https://github.com/hbitter/DNMS/archive/master.zip"
2. entzippen, Gerber-Datei steht in entsprechendem Verzeichnis:  C:\...\PCBs\DNMS-????\???.???-Gerber.zip  
3. Shop/Homepage des PCB-Verkäufers aufrufen z.B. jlcpcb.com oder dirtypcbs.com (10Stk ~30€) oder aisler.net(3Stk ~25€) oder ...  
4. Gerber-Datei hochladen: Menü Leiterplatten "online kalkulieren" oder "berechnen" oder "File" 
5. Kontrollieren, Kaufabwicklung abschließen

Material (Teensy, ESP8266, R, C, ...) gibt bei den bekannten (Google-)Lieferanten (aliexpress/Mouser/Exp-Tech/Conrad/Bürkin/voelkner/Pollin/Reichelt/adafruit/berrybase/watterrott...)
