# KN03: Installation von Web- und Datenbankserver

## Aufgabe A: Installation von Web- und Datenbankserver

In dieser Aufgabe wird eine virtuelle Instanz aufgesetzt und mit einem Web- und Datenbankserver konfiguriert. Es wird Apache als Webserver und MariaDB als Datenbankserver verwendet. Zusätzlich wird PHP installiert, um dynamische Webseiten zu ermöglichen.

### Schritte zur Installation und Konfiguration:

1. **System aktualisieren und Pakete installieren**
    - Update der Pakete:
    ```bash
    sudo apt update
    ```
    - Apache Webserver installieren:
    ```bash
    sudo apt install apache2
    ```
    - PHP installieren:
    ```bash
    sudo apt install php
    ```
    - PHP-Erweiterung für Apache installieren:
    ```bash
    sudo apt install libapache2-mod-php
    ```
    - MariaDB (Datenbankserver) installieren:
    ```bash
    sudo apt install mariadb-server
    ```
    - PHP MySQL-Modul installieren:
    ```bash
    sudo apt install php-mysqli
    ```

2. **Datenbankkonfiguration und Benutzererstellung**
    - Einen neuen Benutzer für MariaDB erstellen:
    ```bash
    sudo mysql -sfu root -e "GRANT ALL ON *.* TO 'admin'@'%' IDENTIFIED BY 'Ihr-Passwort' WITH GRANT OPTION;"
    ```
    *Hinweis:* Passen Sie das Passwort an und verwenden Sie ein einzigartiges Passwort.

3. **Webserver und Datenbank-Server neu starten**
    - Neustart von MariaDB:
    ```bash
    sudo systemctl restart mariadb.service
    ```
    - Neustart des Apache Webservers:
    ```bash
    sudo systemctl restart apache2
    ```

4. **Git-Repo klonen und PHP-Dateien kopieren**
    - Klonen des Git-Repositories:
    ```bash
    git clone https://gitlab.com/ch-tbz-it/Stud/m346/m346scripts.git
    ```
    - Kopieren der PHP-Dateien in das Webserver-Verzeichnis:
    ```bash
    sudo cp ./m346scripts/KN03/*.php /var/www/html/
    ```

5. **Sicherheitsgruppe konfigurieren**
    - Die Sicherheitsgruppe so anpassen, dass die Ports 80 (HTTP) und 22 (SSH) zugänglich sind. 
    - Passen Sie nur die eingehenden Regeln an.

### URLs zum Testen:
- **Apache**: `http://[Ihre-IP]/index.html` - Bestätigt, dass Apache erfolgreich installiert wurde.
- **PHP**: `http://[Ihre-IP]/info.php` - Bestätigt, dass PHP korrekt funktioniert.
- **Datenbank**: `http://[Ihre-IP]/db.php` - Zeigt die Datenbank-Benutzer an und prüft die Verbindung zur Datenbank.

### MySQL-Konsole:
- Loggen Sie sich in die MySQL-Konsole mit dem erstellten Benutzer `admin` ein:
    ```bash
    mysql -u admin -p
    ```
- Führen Sie dieselbe SQL-Abfrage aus wie auf der `db.php`-Seite:
    ```sql
    SELECT Host, User FROM mysql.user;
    ```

### Screenshots:
- **Apache Informationsseite**: ![Apache Informationsseite](KN03/Bilder/2.png)
- **PHP Informationsseite**: ![PHP Informationsseite](KN03/Bilder/3.png)
- **Datenbank Benutzer**: ![Datenbank Benutzer](KN03/Bilder/4.png)
- **Instanz Details**: ![Instanz Details](KN03/Bilder/5.png)
- **Sicherheitsgruppen Regeln**: ![Sicherheitsgruppen Regeln](KN03/Bilder/6.png)
- **MySQL Login und Abfrage Resultat**: ![MySQL Login](KN03/Bilder/1.png) ![MySQL Abfrage Resultat](KN03/Bilder/7.png)

### Erklärung der SQL-Abfrage:
Die ausgeführte SQL-Abfrage lautet:
```sql
SELECT Host, User FROM mysql.user;
