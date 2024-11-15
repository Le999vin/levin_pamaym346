# **KN01: Analyse und Tests mit Hypervisor Typ 2**

## **A. Hypervisor Typ 1 und Typ 2**

Ein **Hypervisor** ermöglicht die Virtualisierung, indem er mehrere virtuelle Maschinen (VMs) auf einer einzigen physischen Maschine verwaltet:

- **Typ 1 Hypervisor (Bare-Metal)**: Läuft direkt auf der Hardware und bietet hohe Leistung. Beispiel: VMware ESXi.
- **Typ 2 Hypervisor (Hosted)**: Läuft auf einem Betriebssystem und ist ideal für Tests und Desktop-Nutzung. Beispiel: VMware Player.

In diesem Projekt arbeite ich mit **VMware Player**, einem Typ-2-Hypervisor.

---

## **B. Virtualisierungssoftware: VMware Player**

### **Aufgabenübersicht:**
1. **Host-System analysieren**  
   CPU- und RAM-Ressourcen des Host-Systems anzeigen.
2. **Virtuelle Maschine erstellen**  
   Debian-VM konfigurieren und starten.
3. **CPU-Ressourcen zuweisen und testen**  
   Mehr Prozessoren zuweisen, als der Host hat, und Ergebnisse prüfen.  
4. **RAM-Ressourcen zuweisen und testen**  
   Mehr RAM zuweisen, als physisch verfügbar, und Ergebnisse analysieren.  
5. **Ergebnisse dokumentieren**  
   Screenshots und Beobachtungen festhalten.

---

### **1. Host-System analysieren**
- **CPU-Ressourcen prüfen:**  
  Befehl:  
  ```bash
  lscpu | grep "CPU(s)"
  ```  
  **Ergebnis:** *Anzahl der logischen Prozessoren am Host-System.*  
  **Screenshot:**  
  ![Host CPU](/KN01/img/Screenshot%202024-11-15%20144906%201.png)  

- **RAM prüfen:**  
  Befehl:  
  ```bash
  free -h
  ```  
  **Ergebnis:** *Gesamter Arbeitsspeicher am Host-System.*  
  **Screenshot:**  
  ![Host RAM](/KN01/img/Screenshot%202024-11-15%20144837%201.png)  

---

### **2. Virtuelle Maschine erstellen**
- **System:** Debian
- **Zugewiesene Ressourcen:**  
  - CPU: *X Prozessoren*  
  - RAM: *X GB*  
  **Screenshot:**  
  ![VM Einstellungen](/KN01/img/Bild%20(1).png)

---

### **3. CPU-Ressourcen zuweisen und testen**
- **Schritte:**  
  1. CPU-Zuweisung: Mehr Prozessoren als Host-System logische Prozessoren hat.  
  2. VM starten und Befehl ausführen:  
     ```bash
     lscpu | grep "CPU(s)"
     ```  
  **Ergebnis:** *Anzeige der Prozessoren oder Fehlermeldung.*  
  **Screenshot:**  
  ![CPU in VM](/KN01/img/Bild%20(2).png)

---

### **4. RAM-Ressourcen zuweisen und testen**
- **Schritte:**  
  1. RAM-Zuweisung: Mehr RAM als am Host-System verfügbar ist.  
  2. VM starten und Befehl ausführen:  
     ```bash
     free -h
     ```  
  **Ergebnis:** *Keine Fehlermeldung.*  
  **Screenshot:**  
  ![RAM in VM](/KN01/img/Bild%20(3).png)

---

## **C. Ergebnisse und Analyse**

- **CPU:**  
  *Beispiel:* Die Zuweisung von mehr Prozessoren war nicht möglich. Der Hypervisor Typ 2 kann nur auf vorhandene Host-Ressourcen zugreifen.  

- **RAM:**  
  *Beispiel:* Es war möglich, mehr RAM zuzuweisen, da der Hypervisor Ressourcen "overcommittet", also simuliert.  

---

## **D. Fazit**
- **Vermutung bestätigt:** Es handelt sich um einen Hypervisor Typ 2, da VMware Player auf ein Host-Betriebssystem angewiesen ist.  
- **Ergebnisse:** Ressourcenlimits wurden teilweise simuliert, was für Typ 2 üblich ist.  

--- 