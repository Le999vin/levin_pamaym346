# KM04
 
# A Cloud-init Datei Verstehen
 
```
#cloud-config # Cloud-init Konfigurations-File
users:
  - name: ubuntu # Erstellen eines Benutzers mit dem Benutzernamen "ubuntu".
    sudo: ALL=(ALL) NOPASSWD:ALL # Gibt dem Benutzer ubuntu alle Rechte und verlangt ein Passwort.
    groups: users, admin # Hinzufügen des Benutzers ubuntu zu den Gruppen users und admin.
    home: /home/ubuntu # Gibt das Home-Verzeichnis des Benutzers an.
    shell: /bin/bash # Setzt die Standard-Shell auf bash
    ssh_authorized_keys: # SSH-Schlüssel für die Authentifizierung
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC6T+vUt44VhcETrWfdACh1OGWsdpw2L3O3HCq5up/A/MgiUcd5gq4YjMGmIxr3RC4IyLANGwhT3ve2mdirArUB8VpqwQmxmAo+oyd2xWJzX+B2eUFnHnD4I6qS7sBnDQTz3S6scdLRUZtodx6Y6RsA3j89ebbfBix0xhkb1kw+zBQ4clR1dOakQbdULSQX8KmLkZOZfTCYCepxGVgLyrEobWCtL8yw521sLTQu+EeiachGPUAF90XSP9DjeMsWm5YmVHAngVGoZ+eZO2rjvqW/FJx4uWKLrBwBdn0jV/xJ8fy5Ja0nH7YFuHZ3chqB7y6pkJYgTd/+/jEm/rYf/2/J aws-key      
ssh_pwauth: false # Deaktiviert die kennwortbasierte SSH-Authentifizierung.
disable_root: false # Root-Benutzer wird nicht deaktiviert
package_update: true # Aktualisierung der Paketliste
packages:
  - curl # installiert Curl
  - wget # installiert Wget
```
 
# B SSH-Key und Cloud-init
 
Ein Screenshot der Details der Instanz. Schauen sie auf das Feld "Key pair assigned at launch".
 
![Alt-Text](KN04//2.png)
 
Screenshot mit dem ssh-Befehl und des Resultats unter Verwendung des ersten Schlüssels.
 
![Alt-Text](KN04/Bilder/3.png)
 
Screenshot mit dem ssh-Befehl und des Resultats unter Verwendung des zweiten Schlüssels.
 
![Alt-Text](KN04/Bilder/4.png)
 
Screenshot mit dem Auszug aus dem Cloud-Init-Log
 
![Alt-Text](KN04/Bilder/5.png)
 
# C Template
 
```#cloud-config
users:
  - name: ubuntu
    sudo: ALL=(ALL) NOPASSWD:ALL
    groups: users, admin
    home: /home/ubuntu
    shell: /bin/bash
    ssh_authorized_keys:
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC6T+vUt44VhcETrWfdACh1OGWsdpw2L3O3HCq5up/A/MgiUcd5gq4YjMGmIxr3RC4IyLANGwhT3ve2mdirArUB8VpqwQmxmAo+oyd2xWJzX+B2eUFnHnD4I6qS7sBnDQTz3S6scdLRUZtodx6Y6RsA3j89ebbfBix0xhkb1kw+zBQ4clR1dOakQbdULSQX8KmLkZOZfTCYCepxGVgLyrEobWCtL8yw521sLTQu+EeiachGPUAF90XSP9DjeMsWm5YmVHAngVGoZ+eZO2rjvqW/FJx4uWKLrBwBdn0jV/xJ8fy5Ja0nH7YFuHZ3chqB7y6pkJYgTd/+/jEm/rYf/2/J aws-key      
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDyWyGTDzzqq9YjuMqsrcXRMhZVrCbD+cnL2YLpTLbTli2jXcX6mISWVzrPQWEkF5OPWCVtWpUpyEgjwe7m7E5zvpI0bGiPrdzrPmO5SMhFI0gRJK5VdJEVl59XColb4ueqh3cwvpbX2kMV8fq04WY+So8mGFlZ+EB+SdvWkgdzde0KOoX8pZQje/rD6GpHF9Jjul075D1kmlS4aUlUmGkM3c6Z5j/phLjyTRayKOD/dZyTEVSGZaS9csd3Qu/b98qoH9VpvG7+ri+RNMh3IYkIpORJjhlCxxvb6uTR89WcvNT94kNBA0GUECQkguElLjx9WSR0RwimfOv4b+Ewj/sX tbz_aws_atilgan aws-key      
ssh_pwauth: false
disable_root: false
package_update: true
packages:
  - curl
  - wget
```
 
# D PHP-Skript zur Datenbankverbindung
 
# Verbindung zur Datenbank testen
 
## 1. Verbindung zur Datenbank vom Webserver aus testen
Mit folgendem Befehl kann die Verbindung zur Datenbank geprüft werden:
 
```bash
mysql -u admin -p -h nc -zv 172.31.36.81
```
 
Wenn die Verbindung erfolgreich ist, wird der MySQL-Monitor geöffnet:
 
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 32
Server version: 5.5.5-10.11.8-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04
```
 
---
 
## 2. Verbindung mit `nc` testen
 
Mit `nc` (Netcat) kann geprüft werden, ob der Port 3306 (MySQL) erreichbar ist:
 
```bash
nc -zv nc -zv 172.31.36.81 3306
```
 
Ausgabe:
 
```
Connection to nc -zv 172.31.36.81 3306 port [tcp/mysql] succeeded!
```
 
## 3. PHP-Skript zur Datenbankverbindung
 
Ein PHP-Skript wurde erstellt, um die Verbindung von der Webserver-Seite zu testen.
 
```
<?php
$servername = "172.31.36.81";
$username = "admin";
$password = "admin";
$dbname = "MainDatabase";
 
$conn = new mysqli($servername, $username, $password, $dbname);
 
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully to the database.";
?>
```
 
## 3. Test Ausgabe der Seiten
Rufen Sie die Seiten index.html, info.php und db.php auf und erstellen Sie einen Screenshot
der URL und des Inhalts:
 
index.html:
 
![Screenshot](KN04/Bilder/8.png)
 
 
info.php:
 
![Screenshot](KN04/Bilder/7.png)
 
 
db.php:
 
![Screenshot](KN04/Bilder/9.png)
 
 
Adminer:
 
![Screenshot](KN04/Bilder/6.png)
hat Kontextmenü


hat Kontextmenü