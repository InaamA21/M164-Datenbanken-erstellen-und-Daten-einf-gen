# Erweiterte DDL & DML Beispiele

## DDL (Data Definition Language)

### 1. Erstellen einer Tabelle mit mehreren Fremdschlüsseln
```sql
CREATE TABLE kunden (
    id INT AUTO_INCREMENT PRIMARY KEY,
    vorname VARCHAR(50) NOT NULL,
    nachname VARCHAR(50) NOT NULL,
    email VARCHAR(100),
    telefon VARCHAR(20)
);
```
CREATE TABLE bestellungen (
    id INT AUTO_INCREMENT PRIMARY KEY,
    bestelldatum DATE NOT NULL,
    kunde_id INT,
    FOREIGN KEY (kunde_id) REFERENCES kunden(id)
);


### 2. Hinzufügen einer neuen Spalte zu einer bestehenden Tabelle
ALTER TABLE mitarbeiter ADD COLUMN adresse VARCHAR(255);


### 3. Ändern des Datentyps einer Spalte
ALTER TABLE mitarbeiter MODIFY COLUMN telefon VARCHAR(50);


### 4. Löschen einer Spalte aus einer Tabelle
ALTER TABLE mitarbeiter DROP COLUMN adresse;


### 5. Erstellen eines Indexes auf einer Spalte
CREATE INDEX idx_nachname ON mitarbeiter(nachname);


### 6. Erstellen einer Tabelle mit einer CHECK-Bedingung
CREATE TABLE produkte (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    preis DECIMAL(10,2),
    CONSTRAINT check_preis CHECK (preis > 0)
);


### 7. Erstellen einer Tabelle mit einem zusammengesetzten Primärschlüssel
CREATE TABLE bestellpositionen (
    bestellnummer INT,
    produkt_id INT,
    menge INT,
    PRIMARY KEY (bestellnummer, produkt_id),
    FOREIGN KEY (bestellnummer) REFERENCES bestellungen(id),
    FOREIGN KEY (produkt_id) REFERENCES produkte(id)
);


## DML (Data Manipulation Language)

### 1. Einfügen von mehreren Datensätzen in eine Tabelle
INSERT INTO kunden (vorname, nachname, email, telefon) 
VALUES 
    ('Max', 'Mustermann', 'max@beispiel.de', '0123456789'),
    ('Erika', 'Musterfrau', 'erika@beispiel.de', '0987654321');


### 2. Abfragen von Daten mit WHERE-Bedingung
SELECT * FROM mitarbeiter WHERE abteilung_id = 2;


### 3. Aktualisieren von mehreren Datensätzen
UPDATE mitarbeiter 
SET telefon = '+49 170 1234567' 
WHERE abteilung_id = 3;


### 4. Löschen von Datensätzen mit einer WHERE-Bedingung
DELETE FROM bestellungen WHERE bestelldatum < '2024-01-01';


### 5. Abfragen von Daten mit ORDER BY
SELECT * FROM mitarbeiter ORDER BY nachname ASC;

### 6. Zählen der Anzahl der Datensätze in einer Tabelle
SELECT COUNT(*) FROM mitarbeiter;


### 7. Verwendung von Aggregatfunktionen (SUM, AVG, MAX, MIN)
* Durchschnittliches Einkommen der Mitarbeiter
SELECT AVG(einkommen) FROM mitarbeiter;

* Gesamtumsatz eines Kunden
SELECT SUM(preis * menge) AS gesamtumsatz 
FROM bestellpositionen 
JOIN produkte ON bestellpositionen.produkt_id = produkte.id
WHERE bestellpositionen.bestellnummer = 101;


### 8. Verwendung von GROUP BY
SELECT abteilung_id, COUNT(*) AS anzahl_mitarbeiter 
FROM mitarbeiter 
GROUP BY abteilung_id;


### 9. Abfragen mit HAVING
SELECT abteilung_id, AVG(einkommen) AS durchschnittseinkommen 
FROM mitarbeiter 
GROUP BY abteilung_id 
HAVING AVG(einkommen) > 5000;


### 10. Verwenden von INNER JOIN
SELECT m.vorname, m.nachname, b.bestellnummer 
FROM mitarbeiter m
JOIN bestellungen b ON m.id = b.kunde_id
WHERE b.bestelldatum > '2024-01-01';


### 11. Verwenden von LEFT JOIN
SELECT m.vorname, m.nachname, b.bestellnummer 
FROM mitarbeiter m
LEFT JOIN bestellungen b ON m.id = b.kunde_id
WHERE m.abteilung_id = 2;


### 12. Einfügen eines Datensatzes und verwenden von Funktionen für die Datenbearbeitung
INSERT INTO bestellungen (bestelldatum, kunde_id)
VALUES (CURDATE(), 5);


