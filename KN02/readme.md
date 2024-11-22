# **KN02: Einführung in IAAS mit AWS**

## **Zusammenfassung**

In dieser Aufgabe habe ich grundlegende Kenntnisse im Umgang mit AWS (Amazon Web Services) und der Virtualisierung von Servern (Instanzen) erlangt. Zudem habe ich die Verwendung von Public/Private Keys zur sicheren Authentifizierung über SSH erlernt.

---

## **Aufgabenübersicht**

### **A. Umgang mit AWS Kurs (20%)**
- Erstellung eines Accounts im "AWS Academy Learner Lab".
- Überwachung der Umgebung: Statusanzeige, Budget und Laufzeit.
- Navigieren zum EC2-Bereich, um Instanzen zu erstellen und zu verwalten.

---

### **B. Erstellen einer EC2-Instanz (40%)**
- **Parameter der Instanz:**
  - **Name:** KN02
  - **Betriebssystem:** Ubuntu 24.04
  - **Instanz-Typ:** t2.micro
  - **Diskgröße:** Standard (8 GB)
  - **RAM:** 1 GB
  - **CPUs:** 1 vCPU
- **Key-Pair:** Zwei SSH-Schlüssel (`levin1` und `levin2`) erstellt. Der erste Schlüssel wurde für den Zugriff ausgewählt.
- **Ergebnisse:**  
  ![Instanz-Liste](./img/instance_list.png)  
  ![Instanz-Details](./img/instance_details.png)

---

### **C. Zugriff mit SSH-Key (40%)**
- **Public/Private Key-Paare:**  
  - Der **öffentliche Schlüssel** liegt auf dem Server (EC2-Instanz).  
  - Der **private Schlüssel** liegt sicher auf meinem lokalen Rechner (z. B. `~/.ssh/levin1.pem`).

- **Zugriff mit SSH:**
  1. **Verwendung des ersten Schlüssels (`levin1`):**
     ```bash
     ssh -i ~/.ssh/levin1.pem ubuntu@[IP-Adresse]
     ```
     **Screenshot:**  
     ![SSH Zugriff levin1](./img/ssh_levin1.png)
  2. **Verwendung des zweiten Schlüssels (`levin2`):**
     ```bash
     ssh -i ~/.ssh/levin2.pem ubuntu@[IP-Adresse]
     ```
     **Screenshot:**  
     ![SSH Zugriff levin2](./img/ssh_levin2.png)

---

## **SSH mit Public/Private Keys**

### **Was ist SSH?**
SSH (Secure Shell) ist ein Protokoll, um eine sichere Verbindung zu einem Server herzustellen. Es wird bevorzugt mit Public/Private Key-Verfahren verwendet, um Passwörter zu vermeiden und die Sicherheit zu erhöhen.

**Befehl zum Zugriff:**
```bash
ssh <user>@<server> -i <path-to-privatekey>/<private-key-file>.pem -o ServerAliveInterval=30
```

- **Standard-Benutzer:**  
  - Für Ubuntu-Instanzen: `ubuntu`  
  - Für Amazon-Instanzen: `ec2-user`

**Beispiel:**
```bash
ssh ubuntu@121.12.3.1 -i ~/.ssh/levin1.pem -o ServerAliveInterval=30
```

### **Erstellen eines Schlüsselpaares**
Der private Schlüssel wird im Verzeichnis `~/.ssh/` gespeichert.

**Befehl:**
```bash
ssh-keygen -f ~/.ssh/<keyname>.pem -t rsa -b 2048 -C "<Kommentar>"
```
**Beispiel:**
```bash
ssh-keygen -f ~/.ssh/levin1.pem -t rsa -b 2048 -C "levin1"
```

**Parameter:**
- `-f`: Dateipfad und Name des Schlüssels.
- `-t`: Algorithmus (z. B. `rsa`).
- `-b`: Schlüssellänge (empfohlen: 2048).
- `-C`: Kommentar oder Name des Schlüssels.

**Exportieren eines öffentlichen Schlüssels:**
Wenn nur der private Schlüssel vorliegt, kann der öffentliche Schlüssel nachträglich exportiert werden:
```bash
ssh-keygen -y -f ~/.ssh/<keyname>.pem > ~/.ssh/<keyname>.pub
```

---

## **Erkenntnisse**

1. **AWS Academy Learner Lab:**
   - Effiziente Verwaltung von Cloud-Umgebungen.
   - Ressourcen wie Budget und Laufzeit sind leicht nachvollziehbar.

2. **EC2-Instanzen:**
   - Anpassung der Hardware-Parameter wie RAM, CPU und Diskgröße.
   - Bedeutung von SSH-Keys für die Authentifizierung.

3. **SSH Public/Private Keys:**
   - Public Key wird auf dem Server hinterlegt, der Private Key bleibt lokal.
   - Sicherheit durch asymmetrische Verschlüsselung.

---

## **Leitfragen / Checkpoints**
- ✔ Verwalten von AWS-Schulungsumgebungen.  
- ✔ Erstellen und Konfigurieren von EC2-Instanzen.  
- ✔ Verwendung und Schutz von SSH-Schlüsselpaaren.  
- ✔ Sicherer Zugriff auf Remote-Server mit `ssh`.

---

> **Hinweis:** Ersetze die Platzhalter (`./img/*.png`) durch deine eigenen Screenshots.