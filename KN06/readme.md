# KN06: Skalierung

## Einleitung
In dieser Kompetenznachweis-Aufgabe habe ich eine .NET Applikation installiert und Instanzen horizontal, vertikal sowie automatisiert skaliert. Dabei wurden verschiedene AWS-Services wie EC2, Load Balancer und Auto Scaling verwendet. 

---

## Schritt-für-Schritt-Anleitung

### A Installation der Applikation

#### 1. MongoDB Atlas einrichten
- Kostenloses Konto auf MongoDB Atlas erstellt
- Neues Cluster erstellt und Verbindung über IP-Whitelist konfiguriert
- Verbindung mit MongoDB Compass getestet

**Screenshot:**
![MongoDB Atlas Cluster](/KN06/imgs/Screenshot%202025-01-31%20145150.png)

#### 2. Webserver auf AWS installieren
- EC2 Instanz gestartet (Ubuntu 22.04)
- Cloud-Init Datei mit den Platzhaltern angepasst und zur Instanz hinzugefügt
- Webserver gestartet und getestet:
  - .NET API lief auf Port 5000
  - Nginx als Reverse Proxy konfiguriert für Weiterleitung auf Port 80


#### 3. Reverse Proxy mit Nginx
- Nginx installiert und konfiguriert:
  ```bash
  sudo apt update
  sudo apt install nginx -y
  ```
- Konfigurationsdatei angepasst:
  ```bash
  server {
      listen 80;
      location / {
          proxy_pass http://localhost:5000;
      }
  }
  ```
- Nginx neu gestartet: `sudo systemctl restart nginx`


**Abgabe:**
- Erklärung zum Reverse Proxy: Ein Reverse Proxy leitet Anfragen von Clients an einen internen Server weiter, um Lastverteilung, Sicherheit und Skalierbarkeit zu verbessern.
- Screenshot von Swagger-UI und API-Endpoints
- Screenshot einer MongoDB Collection


---

### B Vertikale Skalierung

#### 1. Festplattenkapazität auf 20GB erhöhen
- In AWS EC2 Instanz -> Speicher -> Volume auf 20GB erweitert
- Dateisystem aktualisiert: `sudo resize2fs /dev/xvda1`


#### 2. Instanztyp auf t2.medium erhöhen
- EC2-Instanz gestoppt, Instanztyp auf t2.medium geändert und wieder gestartet

**Screenshot:**
![Änderung des Instanztyps](images/instance_type.png)

**Abgabe:**
- Vorher-Nachher Screenshots der Instanz-Ressourcen
- Erklärung der durchgeführten Schritte

---

### C Horizontale Skalierung

#### 1. Load Balancer erstellen
- AWS Load Balancer erstellt (Application Load Balancer)
- Zwei EC2-Instanzen zur Target Group hinzugefügt
- Health Checks konfiguriert

**Screenshot:**
![Load Balancer Konfiguration](/KN06/imgs/Screenshot%202025-01-30%20154157.png)

#### 2. DNS Konfiguration
- Load Balancer Domain mit `app.tbz-m346.ch` verknüpft
- CNAME-Eintrag in Route 53 erstellt


**Abgabe:**
- Erklärung zur DNS-Konfiguration
- Screenshot des Swagger-Aufrufs über die LoadBalancer URL

---

### D Auto Scaling

#### 1. Auto-Scaling Gruppe erstellen
- AWS Auto Scaling konfiguriert:
  - Min. Instanzen: 2
  - Max. Instanzen: 5
  - Skalierung basierend auf CPU-Auslastung

**Screenshot:**
![Auto Scaling Gruppe](images/auto_scaling.png)

#### 2. Funktionstest
- Eine Instanz manuell heruntergefahren und überprüft, ob eine neue Instanz erstellt wurde


**Abgabe:**
- Dokumentation der Auto Scaling Konfiguration
- Erklärungen zu Template, Health Checks usw.

---

**Screenshot:**
![200 ok](/KN06/imgs/Screenshot%202025-01-30%20152225.png)

## Fazit
Durch diese Aufgabe habe ich gelernt, wie man eine skalierbare Web-Applikation mit AWS einrichtet. Die vertikale Skalierung verbessert die Leistung einer einzelnen Instanz, während die horizontale Skalierung mit Load Balancer und Auto Scaling für Hochverfügbarkeit sorgt.