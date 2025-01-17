# Cloud-Migrationskostenanalyse

## A Kostenrechnung: Migration zu Cloud-Infrastrukturen

### 1. **Rehosting (IaaS)**

#### AWS (Amazon Web Services)

![AWS Konfiguration](/levin_pamaym346/KN10/imgs/KN10_1.png "AWS Konfiguration")

Für die Rehosting-Option bei AWS wurde folgende Infrastruktur gewählt:
- **2 EC2-Instanzen**: Eine für den Webserver, eine für die Datenbank, zur Nachbildung der On-Premise-Infrastruktur.
- **AWS Backup**: Tägliche, wöchentliche und monatliche Sicherungen der Datenbank.
- **Elastic Load Balancer**: Lastverteilung zur Steigerung der Verfügbarkeit.
- **Elastic Block Store (EBS)**: Speicherung von Daten.

**Begründung:**  
Die AWS-Konfiguration basiert auf den aktuellen Anforderungen und der bestehenden Infrastruktur. Es wurden mögliche Optimierungen berücksichtigt, obwohl einige Details unklar blieben.

## Azure (Microsoft)

### Für Azure wurde diese Konfiguration gewählt:
2 Virtual Machines (VMs): 
Eine für den Webserver, eine für die Datenbank (Azure bietet keine dedizierten Datenbankinstanzen).

Azure Backup: Regelmässige Sicherungen der Datenbank.

Azure Load Balancer: 
Effiziente Verteilung des Datenverkehrs (kostengünstig oder kostenlos).

**Begründung:**  
Die Azure-Konfiguration erfüllt die grundlegenden Anforderungen und wurde mit Blick auf Kosteneffizienz gewählt.

**Kostenübersicht:**
- **Estimated Upfront Cost:** $0.00
- **Estimated Monthly Cost:** $116.25

---

### 2. **Replattforming (PaaS)**

#### Heroku

![Heroku Konfiguration](/levin_pamaym346/KN10/imgs/KN10_3.png "Heroku Konfiguration")

Für die Replattforming-Option bei Heroku wurde folgende Konfiguration gewählt:
- **Performance M Dyno**: Mittlere Leistung, passend zu den Anforderungen.
- **Postgres Standard 2**: Datenbankoption mit über 100 GB Speicher.

**Begründung:**  
Die Auswahl bei Heroku ist eingeschränkt, jedoch erfüllt die Konfiguration die Grundanforderungen. Aufgrund der hohen Kosten ist Heroku jedoch weniger attraktiv als langfristige Lösung.

**Fazit:**  
Heroku sollte nur in Betracht gezogen werden, wenn andere Optionen nicht praktikabel sind.

---

### 3. **Repurchasing (SaaS)**

#### Zoho CRM

![Zoho CRM](/levin_pamaym346/KN10/imgs/KN10_4.png "Zoho CRM")

**Paket:** Professional Plan – 23 € pro Benutzer/Monat.

**Funktionen:**
- Bestandsmanagement
- SalesSignals
- E-Mail-Integration
- Zuweisungsregeln

**Begründung:**  
Das Professional-Paket bietet ein gutes Preis-Leistungs-Verhältnis und deckt die Grundanforderungen effizient ab.

#### Salesforce Sales Cloud

![Salesforce](/levin_pamaym346/KN10/imgs/KN10_5.png "Salesforce Sales Cloud")

**Paket:** Starter Suite – 25 USD pro Benutzer/Monat.

**Funktionen:**
- Lead-Management
- Kontaktverwaltung
- E-Mail-Integration
- Einfaches Setup und Onboarding

**Begründung:**  
Die Starter Suite ist preislich attraktiv und bietet die grundlegenden Funktionen. Sie erfordert jedoch mehr Aufwand bei der Verwaltung und Anpassung.

---

## B **Interpretation der Resultate**

### **Vergleich der Migrationsoptionen**

| **Lösung**        | **Kostenstruktur**                                      | **Aufwand**                                      |
|-------------------|--------------------------------------------------------|-------------------------------------------------|
| **IaaS (AWS & Azure)** | Monatliche Gebühren für Server, Speicher und Netzwerk | Technisches Know-how erforderlich               |
| **PaaS (Heroku)**  | Höhere Gebühren durch integrierte Dienste              | Weniger Verwaltungsaufwand                      |
| **SaaS (Zoho CRM & Salesforce)** | Fixe Kosten pro Benutzer + Schulungskosten | Minimaler technischer Aufwand                   |

---

### **Empfehlung:**

Die Migration zu einer **SaaS-Lösung** wie **Zoho CRM** ist die effizienteste Option. Sie reduziert den internen Aufwand und bietet eine transparente Kostenstruktur.

#### **Fazit:**
Zoho CRM stellt eine kosteneffiziente, wartungsarme Lösung dar, die die Anforderungen gut abdeckt. Eine Testphase wird empfohlen, um sicherzustellen, dass alle spezifischen Anforderungen des Unternehmens berücksichtigt werden.
