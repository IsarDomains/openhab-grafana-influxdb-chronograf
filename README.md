# openhab-grafana-influxdb-chronograf
YAML Datei für Docker um openHAB2 in Verbindung mit Grafana (verwendet InfluxDB) auf einen Raspberry Pi 3 auszuführen. 

# Voraussetzungen
Folgende Voraussetzungen sollten gegeben sein um die Container zu starten:
 - Raspberry Pi 3 (Model B) mit Raspbian Image (https://www.raspberrypi.org/downloads/raspbian/)
 - Zugriff auf den RasPi via SSH und FTP mit einem User mit Root-Rechten
 - ```docker``` muss installiert sein (https://www.docker.com/blog/happy-pi-day-docker-raspberry-pi/) und als Service bei Systemstart geladen werden (```sudo systemctl enable docker.service``` && ```sudo systemctl start docker.service```) 
 - ```docker-compose``` muss installiert sein
 - [Optional] Portainer zur einfachen Verwaltung und Kontrolle der Docker-Container installieren (http://portainer.io/) 
 
# Installation
Zur Vereinfachung befinden sich sämtliche Dateien - sowohl die YAML Datei als auch alle Container Mappings (siehe unten) - in einem Verzeichnis auf dem RasPi: ```/opt/smarthome```
1) Login auf den RasPi per SSH.
2) Verzeichnis anlegen: ```sudo mkdir /opt/smarthome/```
3) Den Ordner **docker-compose** dieses Projektes in das Verzeichnis kopieren:
    - ```cd /tmp/```
    - ```sudo git clone https://github.com/IsarDomains/openhab-grafana-influxdb-chronograf.git``` 
    - ```sudo cp -r /tmp/openhab-grafana-influxdb-chronograf/docker-compose /opt/smarthome/```

# Mapping der Containerinhalte
Damit nach dem Abräumen der Container die darin angelegten Daten auch nach einem Neustart wieder verfügbar sind, werden die Datenverzeichnisse der einzelnen Container auf gleichnamige Verzeichnisse des RasPi unter ```/opt/smarthome``` gemappt. Diese müssen angelegt werden:
 - openHAB2: ```sudo mkdir /opt/smarthome/openhab```
 - Grafana: ```sudo mkdir /opt/smarthome/grafana```
 - InfluxDB: ```sudo mkdir /opt/smarthome/influxdb```
 - Chronograf: ```sudo mkdir /opt/smarthome/chronograf```
 - deCONZ: ```sudo mkdir /opt/smarthome/deconz```
  
So sollte das ```/opt/smarthome``` Verzeichnis am Ende aussehen, wenn alle Ordner vorhanden sind:
<img src="https://user-images.githubusercontent.com/35771024/72264484-1d312b80-361b-11ea-9b92-f7f53d46c69e.png" title="Verzeichnisstruktur auf dem RasPi 3." width="300" />

# Starten der Container
Der folgende Befehl führt die Befehle in der YAML Datei aus und startet die Container:

```docker-compose -f /opt/smarthome/docker-compose/docker-compose.yml up```

Das dauert etwas, da die Images für openHAB2, Grafana, InfluxDB und Chronograf erst heruntergeladen werden müssen. Für alle Images wird der Tag ```:latest``` verwendet.

Sollte optional Portainer auf dem RasPi laufen, kann man hierüber einfach nachschauen, ob alle Images bereits gestartet sind. Ist dies der Fall, schaut es in der Portainer Oberfläche im Bereich *Container* ungefähr so hier aus:
![image](https://user-images.githubusercontent.com/35771024/72262426-320bc000-3617-11ea-9bee-9cc2dafa0b8d.png)

### Login ###
Die einzelnen Web-Logins erreicht ihr über die gemappten Standardports der jeweiligen Applikationen:
 - openHAB2: ```http://<ip_des_raspi>:8080```
 - deConz: ```http://<ip_des_raspi>:8085```
 - Grafana: ```http://<ip_des_raspi>:3000```
 - Chronograf: ```http://<ip_des_raspi>:8888``` 
 - InfluxDB: ```http://<ip_des_raspi>:8086``` Achtung: Diese IP wird nun beim Aufsetzten der Datenbank in Chronograf benötigt.
