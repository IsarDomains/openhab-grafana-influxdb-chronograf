# openhab-grafana-influxdb-chronograf
YAML Datei für Docker um openHAB2 in Verbindung mit Grafana (verwendet InfluxDB) auf einen Raspberry Pi 3 auszuführen. 

# Voraussetzungen
Folgende Voraussetzungen sollten gegeben sein um die Container zu starten:
 - Raspberry Pi 3 (Model B) mit Raspbian Image (https://www.raspberrypi.org/downloads/raspbian/)
 - Zugriff auf den RasPi via SSH und FTP mit einem User mit Root-Rechten
 - ```docker``` muss installiert sein (https://www.docker.com/blog/happy-pi-day-docker-raspberry-pi/) und als Service bei Systemstart geladen werden (```sudo systemctl enable docker.service``` && ```sudo systemctl start docker.service```) 
 - ```docker-compose``` muss installiert sein
 - [Optional] Portainer zur einfachen Verwaltung und Kontrolle der Docker-Container installieren (http://portainer.io/) 
 
# Mapping der Containerinhalte
Damit nach dem Abräumen der Container die darin angelegten Daten auch nach einem Neustart wieder verfügbar sind, werden die Datenverzeichnisse der Container auf Verzeichnisse des RasPi gemappt. Das Root-Verzeichnis auf dem RasPi dazu ist ```/opt/smarthome``` (muss angelegt werden ```sudo mkdir /opt/smarthome/```). Darunter befindet sich für jeden gestarteten Container ein eigenes Unterverzeichnis.
