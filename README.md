# MQTT Broker Installation Anleitung auf Linux

## Einleitung
Diese Anleitung beschreibt die Schritte zur Installation eines MQTT Brokers auf einem Linux-System. MQTT (Message Queuing Telemetry Transport) ist ein leichtgewichtiges Protokoll, das sich ideal für IoT-Anwendungen eignet.

## Voraussetzungen
- Ein Linux-basiertes Betriebssystem (z.B. Ubuntu, Debian, CentOS)
- Zugriff auf die Kommandozeile mit Root-Rechten oder Sudo-Rechten
- Internetverbindung

## Schritt 1: Systemaktualisierung
Bevor Sie mit der Installation beginnen, aktualisieren Sie Ihr System, um sicherzustellen, dass alle Pakete auf dem neuesten Stand sind.

```bash
sudo apt update
sudo apt upgrade -y
```
## Schritt 2: MQTT Broker installieren
- In diesem Beispiel verwenden wir Eclipse Mosquitto, einen der beliebtesten MQTT Broker. Führen Sie die folgenden Schritte aus, um ihn zu installieren.
```bash
sudo apt install mosquitto mosquitto-clients
```
## Schritt 3: Mosquitto-Dienst starten
```bash
sudo systemctl start mosquitto
```

## Schritt 4: Konfiguration
- Die Standardkonfiguration von Mosquitto sollte für viele Anwendungen ausreichend sein. Sie können die Konfigurationsdatei jedoch anpassen, um spezifische Anforderungen zu erfüllen.
```bash
sudo systemctl enable mosquitto
```

## Schritt 5: Passwort(Optional)
- Erstelle eine Passwortdatei:
```bash
sudo mosquitto_passwd -c /etc/mosquitto/passwd dein_benutzername
```
- Öffne die mosquitto.conf Datei:
```bash
sudo nano /etc/mosquitto/mosquitto.conf
```
- füge folgendes ein:
```bash
allow_anonymous false
password_file /etc/mosquitto/passwd

persistence true
persistence_location /var/lib/mosquitto/

log_dest file /var/log/mosquitto/mosquitto.log

include_dir /etc/mosquitto/conf.d

listener 1883
```

## Schritt 6:  Mosquitto neu starten
```bash
sudo systemctl restart mosquitto
```
## Schritt 7: Testen des MQTT Brokers
```bash
mosquitto_pub -h localhost -t test/topic -m "Hello MQTT"
```


```bash
mosquitto_sub -h localhost -t test/topic

