# SELECT Befehle 
## COUNT
### Gibt die Anzahl der Zeilen in einer Tabelle oder Gruppe zurück
SELECT COUNT(*) FROM customers;
SELECT COUNT(salary) FROM customers;
## SUM
### Berechnet die Summe der Werte in einer Spalte oder Gruppe
SELECT SUM(salary) FROM employees;
## AVG
### Berechnet den Durchschnittswert der Werte in einer Spalte oder Gruppe
SELECT AVG(salary) FROM employees;
## MIN
### Gibt den kleinsten Wert in einer Spalte oder Gruppe zurück
SELECT MIN(salary) FROM employees;
## MAX
### Gibt den grössten Wert in einer Spalte oder Gruppe zurück
SELECT MAX(salary) FROM employees;
## GROUP BY
### Gruppiert Daten, basierend auf dem Inhalt einer oder mehrerer Spalten
SELECT customer_id, SUM(order_total) FROM orders GROUP BY customer_id;
## HAVING
### Gibt nach der Gruppierung nu die an die die Anforderungen erfühlt
SELECT customer_id, SUM(order_total) FROM orders GROUP BY customer_id HAVING SUM(order_total) > 500;

## SUBQUERY
### Abfrage innerhalb einer anderen Abfrage. Tabellen die Bedingungen erfühllen abzufragen. 
### z.B. in den Klauseln: WHERE, FROM, HAVING und SELECT
### Unterabfragen: UPDATE, DELETE, INSERT

## skalaren und nicht-skalaren Subqueries 
### skalaren: Gibt einen einzelnen Wert zurück, wenn nichts gefunden wird kommt der Wert NULL zurück 
### nicht-skalaren: Gibt 0, 1 oder mehrere Zeilen zurück, von denen jede 1 oder mehrere Spalten enthalten kann
### Skalere Unterabfrage: SELECT * FROM artikel WHERE einkaufspreis > (SELECT AVG(enkaufspreis) FROM artikel); 
### Nicht-skalare Unterabfrage: SELECT Name FROM Mitarbeiter WHERE AbteilungsID IN (SELECT AbteilungsID FROM Abteilung WHERE Standort = 'Zürich');

## Operatoren 
### Nur in einere Unterabfrage skalar: =, >, >=, <, <=

## JOIN + Subquery
### use northwind;
SELECT customers.ContactName, orders.orderdate FROM customers
INNER JOIN orders ON customers.customerid = orders.customerid
WHERE orders.orderdate IN           
(SELECT MAX(orderdate) FROM orders 
GROUP BY customerid);

## LOAD DATA INFILE
### CSV-Datei vom Server laden 
### z.B. LOAD DATA LOCAL INFILE "C:/path/import.csv"


# Datensicherung von Datenbanken #

### **Wichtigkeit der Datensicherung**
Datenbanken sind essenziell für Webhosting und Unternehmenssoftware. Sie enthalten oft sensible Informationen wie Personal- und Finanzdaten. Ein Datenverlust kann durch Hardwareausfälle oder Benutzerfehler entstehen und erhebliche Probleme verursachen. Daher sind regelmässige Backups notwendig.

### **Backup-Konzepte**
Es gibt verschiedene Möglichkeiten, Datenbanken zu sichern:
- **Online-Backup**: Die Datenbank bleibt aktiv, Änderungen werden während der Sicherung separat gespeichert.
- **Offline-Backup**: Die Datenbank wird heruntergefahren, was für Webseiten oder Anwendungen eine temporäre Nichtverfügbarkeit bedeutet.

### **Backup-Typen**
1. **Voll-Backup**: Sichert alle Daten, benötigt aber viel Speicherplatz.
2. **Differentielles Backup**: Erstellt ein Voll-Backup und speichert danach nur die geänderten/neuen Dateien.
3. **Inkrementelles Backup**: Speichert nur die seit dem letzten Backup veränderten Dateien, erfordert zur Wiederherstellung alle vorherigen Backups.

### **Backup-Methoden und Tools**
- **MySQLDump**: Shell-Befehl zur Sicherung von MySQL-Datenbanken.
- **phpMyAdmin**: Export von SQL-Datenbanken, jedoch begrenzte Datei-Grösse.
- **BigDump**: Ergänzung zu phpMyAdmin für grosse Backups.
- **HeidiSQL**: Backup-Tool für Windows, aber ohne Automatisierung.
- **Mariabackup**: Open-Source-Tool für MariaDB-Datenbanken.

### **Datenschutz und Sicherheit**
Backups sollten sicher und verschlüsselt auf externen Speichermedien gespeichert werden, um sie vor Diebstahl oder Schäden zu schützen. Ein eigener Backup-User mit spezifischen Rechten wird empfohlen:
```sql
GRANT RELOAD, PROCESS, LOCK TABLES, REPLICATION CLIENT ON *.* TO 'backupuser'@'localhost' IDENTIFIED BY 'backup123';
```

---

## **Aufgabenbearbeitung**

### **1. Daten normalisiert einbinden (DB Freifächer)**
#### **Datenbankanforderungen**
- Schüler haben eine Nummer und eine Stammklasse.
- Schüler können sich in beliebige Freifächer eintragen.
- Klassenlehrer unterrichten auch Freifächer.
- Ein Freifach hat eine Nummer, ein Thema, ein Zimmer und einen bestimmten Tag.
- Jedes Freifach wird von einem Lehrer unterrichtet.

### **2. Schritte zur Normalisierung und Datenverarbeitung**
1. **Erstellen der 1. Normalform (1NF)**: Atomare Felder in Excel-Tabelle umwandeln und als CSV exportieren.
2. **Erstellung des logischen ERD**: Tabellen und Kardinalitäten bestimmen.
3. **Erstellung des physischen ERD**: NN- und UQ-Constraints setzen, SQL-DDL-Script erzeugen.
4. **Import der Daten**: CSV-Dateien mit `LOAD DATA LOCAL INFILE` in die normalisierten Tabellen laden.
5. **Datenbereinigung**: Entfernen von Redundanzen und Inkonsistenzen.
6. **Datenprüfung**: Vergleich von CSV-Daten mit normalisierten Tabellen durch SELECT-Abfragen.
7. **Erweiterung um 290 Testdatensätze**: Generieren zusätzlicher Schülerdaten.
8. **SQL-Abfragen ausführen**:
   - Teilnehmerzahl von „Inge Sommer“ im Freifach ermitteln.
   - Klassenliste mit Schüleranzahl in Freifächern ausgeben.
   - Schüler, die „Chor“ oder „Elektronik“ besuchen, auflisten.
9. **Ergebnisse speichern**:
   ```sql
   SELECT * FROM ergebnisse INTO OUTFILE 'C:/M164/outfile.csv';
   ```
10. **Backup der Freifächer-DB erstellen**:
   ```sql
   mysqldump -u backupuser -p --databases Freifaecher > backup.sql
   ```

### **3. Checkpoint-Fragen**

1. **Grundsätzlicher Ablauf der Normalisierung**
   - Daten analysieren und atomare Felder definieren (1NF)
   - Beziehungen und Fremdschlüssel festlegen (2NF)
   - Eliminierung funktionaler Abhängigkeiten (3NF)

2. **Unterschied zwischen logischem und physischem Backup**
   - Logisches Backup: Export von Daten im SQL-Format
   - Physisches Backup: Kopieren kompletter Datenbankdateien

3. **Restore-Prozess für verschiedene Backups**
   - **Voll-Backup**: `mysql -u user -p < backup.sql`
   - **Inkrementelles Backup**: Reihenfolge von Voll- und Inkrement-Backups beachten.
   - **Differentielles Backup**: Letztes Voll-Backup + Differentielles Backup wiederherstellen.

4. **Drei Backup-Methoden**
   - **mysqldump**: `mysqldump -u user -p dbname > backup.sql`
   - **phpMyAdmin**: Exportieren der Datenbank als SQL-Datei
   - **HeidiSQL**: Backup über grafische Oberfläche

5. **Fünf Schritte zur 3NF**
   - Entfernen von Mehrfachwerten (1NF)
   - Eliminierung partieller Abhängigkeiten (2NF)
   - Entfernen transistiver Abhängigkeiten (3NF)
   - Überprüfung von Fremdschlüsseln und Beziehungen
   - Implementierung von Constraints

6. **Funktion von `SELECT INTO OUTFILE`**
   - Exportiert eine SQL-Abfrage direkt in eine Datei.
   ```sql
   SELECT * FROM schueler INTO OUTFILE 'C:/M164/schueler.csv';
   ```


