# M164 Stoff - Fragen Reflexion

## Inhaltsverzeichnis
- [Stufen der Wissenstreppe](#stufen-der-wissenstreppe)
- [Anomalien in einer Datenbasis](#anomalien-in-einer-datenbasis)
- [Redundante Daten](#redundante-daten)
- [Datenstrukturierung bei der Erhebung und Ablage von Daten](#datenstrukturierung-bei-der-erhebung-und-ablage-von-daten)
- [Grundlagen der Datenmodellierung](#grundlagen-der-datenmodellierung)
- [Attributkonzept und Generalisierung/Spezialisierung](#attributkonzept-und-generalisierungspezialisierung)
- [Identifying vs. Non-Identifying Relationships](#identifying-vs-non-identifying-relationships)
- [Datenbanksysteme (DBS)](#datenbanksysteme-dbs)
- [Wann sind einfache Dateien sinnvoll?](#wann-sind-einfache-dateien-sinnvoll)
- [Zeichensatzkodierungen (CHARSET=)](#zeichensatzkodierungen-charset)
- [Forward Engineering](#forward-engineering)
- [Weitere Themen](#weitere-themen)
- [SQL-Anwendungen & Befehle](#sql-anwendungen--befehle)


## Stufen der Wissenstreppe

Die Wissenstreppe nach North beschreibt den Weg von Zeichen bis zur Kompetenz bzw. Wettbewerbsfähigkeit. Die Stufen sind:

1. **Zeichen**  
   Z.B. „1.10“

2. **Daten**  
   Z.B. „1.10 USD/EUR“ (isolierte Werte ohne Kontext)

3. **Information**  
   Z.B. „Der aktuelle Wechselkurs beträgt 1.10 USD für 1 EUR.“

4. **Wissen**  
   Z.B. „Der USD ist im Vergleich zum EUR stärker geworden.“

5. **Verständnis**  
   Z.B. „Wenn der USD stärker wird, werden Importe für die USA günstiger.“

6. **Handlung**  
   Z.B. „Ein Investor kauft jetzt EUR, um von einem späteren Kursanstieg zu profitieren.“

7. **Kompetenz**  
   Z.B. „Ein erfahrener Devisenhändler entwickelt Strategien zur Kurssicherung.“

8. **Wettbewerbsfähigkeit**  
   Z.B. „Ein Unternehmen sichert sich durch geschickte Währungsabsicherungen einen Marktvorteil.“

## Abbildung von Netzwerk-Beziehungen im logischen Modell

Netzwerk-Beziehungen werden im logischen Datenmodell meist durch relationale Verknüpfungen abgebildet, typischerweise durch Primär- und Fremdschlüssel in relationalen Datenbanken.

### Typen von Beziehungen:

- **1:1-Beziehung**  
  Ein Land hat eine Währung (Tabellen „Länder“ und „Währungen“ mit einer gemeinsamen Schlüsselspalte).

- **1:n-Beziehung**  
  Ein Kunde kann mehrere Bestellungen haben (Tabellen „Kunden“ und „Bestellungen“ mit Kunden-ID als Fremdschlüssel in „Bestellungen“).

- **m:n-Beziehung**  
  Ein Student kann mehrere Kurse belegen, ein Kurs kann mehrere Studenten haben (zusätzliche Beziehungstabelle „Einschreibung“ mit Student-ID und Kurs-ID als Schlüssel).

## Anomalien in einer Datenbasis

Anomalien entstehen in schlecht normalisierten Datenbanken und führen zu Inkonsistenzen. Die drei Hauptarten sind:

- **Einfügeanomalie**  
  Neue Daten können nicht eingefügt werden, ohne unnötige zusätzliche Informationen zu speichern.  
  Beispiel: Ein neuer Kurs kann nicht hinzugefügt werden, weil noch kein Student eingeschrieben ist.

- **Änderungsanomalie**  
  Änderungen müssen an mehreren Stellen durchgeführt werden, was Fehler verursachen kann.  
  Beispiel: Eine Adressänderung eines Kunden muss in mehreren Tabellen angepasst werden.

- **Löschanomalie**  
  Beim Löschen eines Datensatzes gehen ungewollt weitere Daten verloren.  
  Beispiel: Wenn der letzte Student eines Kurses entfernt wird, verschwindet auch die Kursinformation.

## Redundante Daten

Ja, redundante Daten entstehen, wenn dieselben Informationen mehrfach gespeichert werden. Dies kann zu Inkonsistenzen führen und den Speicherplatzverbrauch unnötig erhöhen.

**Beispiel**: Wenn die Adresse eines Kunden in mehreren Tabellen gespeichert ist, kann es zu Unstimmigkeiten kommen, wenn nur eine aktualisiert wird.

## Datenstrukturierung bei der Erhebung und Ablage von Daten

### Zwei strukturierbare Aspekte:

1. **Inhaltliche Strukturierung**  
   Welche Informationen gespeichert werden (z. B. Name, Adresse, Bestellungen).

2. **Formale Strukturierung**  
   Wie die Daten gespeichert werden (tabellarisch, hierarchisch, JSON, XML).

### Kategorien der Strukturierung:

- **Unstrukturierte Daten**: Freitext, Bilder, Videos.
- **Semistrukturierte Daten**: JSON, XML, Log-Dateien.
- **Strukturierte Daten**: Relationale Datenbanken mit Tabellen, Spalten und Datentypen.

### Datenstruktur in einer Datenbank:
- Daten müssen **normalisiert** sein (mindestens 3. Normalform), um Redundanzen und Anomalien zu vermeiden.
- Tabellen mit **Primär- und Fremdschlüsseln** zur Abbildung von Beziehungen.
- **Konsistente Datentypen** und Validierungen zur Sicherstellung der Datenintegrität.

## Grundlagen der Datenmodellierung

Datenmodellierung ist eine zentrale Phase der Datenbankentwicklung, in der die Struktur von Daten definiert wird. Dabei werden drei aufeinander aufbauende Datenmodelle erstellt:

1. **Konzeptionelles Datenmodell (ERM)**  
   Fachlich orientiert, unabhängig von der Implementierung, direkt aus den Anforderungen abgeleitet.

2. **Logisches Datenmodell (ERD)**  
   Übersetzung des konzeptionellen Modells in ein konkretes Datenbanksystem, mit Primär- und Fremdschlüsseln.

3. **Physisches Datenmodell**  
   Enthält produktespezifische Aspekte wie SQL-Definitionen (DDL), Indizes und Partitionierungen zur direkten Implementierung.

In operativen Systemen wird meist die **3. Normalform** (3NF) genutzt, um Daten anwendungsunabhängig zu speichern (z. B. in ERP-Systemen oder Data Warehouses). Für Analyse- und Reportingzwecke wird oft das **Star Schema** verwendet. Die **Data Vault Modellierung** ist eine neuere Methode, die auf Erweiterbarkeit und Automatisierung ausgelegt ist und vor allem im Core DWH und Integration Layer Anwendung findet.

## Attributkonzept und Generalisierung/Spezialisierung

Bei der Datenbankmodellierung nach dem **Attributkonzept** werden Attribute und deren Ausprägungen Entitätstypen zugeordnet. Ein Problem entsteht, wenn mehrere Entitätstypen viele gemeinsame Attribute haben, aber auch einige unterschiedliche – dies kann zu Redundanz führen.

**Lösung**:
- Gemeinsame Attribute werden in einem allgemeinen Entitätstyp (Generalisierung) zusammengefasst.
- Unterschiedliche Attribute bleiben in den spezialisierten Entitätstypen (Spezialisierung) erhalten.

Die spezialisierten Entitätstypen verweisen über Fremdschlüssel auf die generalisierte Tabelle, um Informationsverlust zu vermeiden.  
Diese Beziehung wird als „**is_a**“-Beziehung bezeichnet (z. B. „Eine Person ist ein Fahrer“). Dieses Konzept ähnelt der **Vererbung** in der objektorientierten Modellierung.

## Identifying vs. Non-Identifying Relationships

In relationalen Datenbanken gibt es zwei Arten von Beziehungen zwischen einer Parent-Tabelle (Master) und einer Child-Tabelle (Detail):

- **Identifying Relationship**:  
  Der Fremdschlüssel ist Teil des Primärschlüssels der Child-Tabelle.  
  Die Identität eines Datensatzes hängt direkt von der Parent-Tabelle ab.  
  Beispiel: Ein Raum gehört eindeutig zu einem Gebäude (der Fremdschlüssel auf das Gebäude ist Teil der Raum-ID).

- **Non-Identifying Relationship**:  
  Der Fremdschlüssel ist kein Bestandteil des Primärschlüssels der Child-Tabelle.  
  Die Beziehung ist flexibler, da der Fremdschlüsselwert geändert werden kann.  
  Beispiel: Ein Mitarbeiter gehört zu einer Abteilung, aber seine Identität bleibt unabhängig von der Abteilung bestehen.

Identifying Relationships sorgen für eine stärkere Abhängigkeit, während Non-Identifying Relationships mehr Flexibilität ermöglichen.

## Datenbanksysteme (DBS)

Ein **Datenbanksystem (DBS)** dient der effizienten Verwaltung großer Datenmengen. Es besteht aus einem **Datenbankmanagementsystem (DBMS)** und der eigentlichen **Datenbank (DB)**. Das DBMS organisiert die strukturierte Speicherung und den Zugriff auf die Daten.
![DMBS](https://github.com/user-attachments/assets/7131f1cc-4164-4f79-85f3-e9d4810cc913)

### Merkmale eines DBMS:
- **Integrierte Datenhaltung**: Vermeidung von Datenredundanz und effiziente Verknüpfung von Daten.
- **Datenbanksprache (SQL)**:
  - **DQL (SELECT)** für Abfragen,
  - **DDL (CREATE)** für Strukturverwaltung,
  - **DML (INSERT)** für Datenmanipulation,
  - **DCL (GRANT)** für Rechteverwaltung,
  - **TCL (COMMIT)** für Transaktionen.
- **Benutzersichten**: Anpassung der Datenansicht je nach Benutzeranforderung.
- **Konsistenzkontrolle**: Gewährleistung korrekter und widerspruchsfreier Daten.
- **Zugriffskontrolle**: Schutz sensibler Daten durch Benutzerrechte.
- **Transaktionsmanagement**: Gewährleistung der Atomarität und Dauerhaftigkeit von Änderungen.
- **Mehrbenutzerfähigkeit**: Synchronisierung gleichzeitiger Zugriffe.
- **Datensicherung**: Wiederherstellung im Fehlerfall.

### Vorteile eines DBS:
- Standardisierung und effiziente Verwaltung großer Datenmengen.
- Verkürzung der Entwicklungszeit durch zentrale Funktionen.
- Hohe Flexibilität und Anpassbarkeit.
- Hohe Verfügbarkeit und Synchronisation für parallele Benutzer.
- Kosteneffizienz durch zentrale Datenhaltung.

### Nachteile eines DBS:
- Hohe Anfangsinvestitionen für Software und Hardware.
- Weniger effizient für spezialisierte Anwendungen.
- Komplexität und Kosten für Sicherheit und Administration.
- Risiko der Zentralisierung (z. B. Systemausfälle).

## Wann sind einfache Dateien sinnvoll?

Einfache Dateien sind sinnvoll, wenn:
- Kein gleichzeitiger Mehrbenutzerzugriff nötig ist.
- Echtzeitanforderungen bestehen, die ein DBMS nicht optimal erfüllt.
- Die Daten statisch und wohldefiniert sind.

Ein **Datenbanksystem** ist ideal für komplexe, dynamische und mehrbenutzerfähige Anwendungen, während einfache Dateien für kleine, spezialisierte Anwendungen geeignet sind.

## Zeichensatzkodierungen (CHARSET=)

Zeichensatzkodierungen ordnen bestimmten Byte-Werten konkrete Zeichen zu. Wichtige Kodierungen sind:

- **ASCII** (veraltet): 7-Bit, 128 Zeichen, nur englische Zeichen und Steuerzeichen.
- **ANSI (ISO-8859-1 / Latin1)**: 8-Bit, enthält ASCII-Zeichen und zusätzliche Sonderzeichen für Westeuropa.
- **Unicode (UCS)**: Universeller Zeichensatz mit bis zu 100.000 Zeichen, 32-Bit pro Zeichen.
- **UTF-8** (Standard): Variable Länge (1-4 Byte), kompatibel mit ASCII, weltweit am häufigsten genutzt.
- **UTF-16 / UTF-32**: Unicode-Kodierungen mit fester 16-Bit bzw. 32-Bit Länge, höhere Speichernutzung.

**UTF-8** ist heute die meistgenutzte Zeichensatzkodierung, da sie Speicher effizient nutzt und universell einsetzbar ist.

## Forward Engineering
![Forward Engineering](https://github.com/user-attachments/assets/79c0b5fc-8a28-4c5c-b5f4-3f1610c2e4b0)
**Forward Engineering** ist der Prozess der Erstellung einer Datenbank aus einem physischen Datenmodell, das Tabellen, Spalten, Beziehungen und Einschränkungen beschreibt. Der Vorteil liegt in der Automatisierung der Datenbankerstellung, wodurch Fehler reduziert und Inkonsistenzen frühzeitig erkannt werden können, bevor die Datenbank in Betrieb geht.

## Weitere Themen

### Mehrfachbeziehungen
Hier bestehen zwischen zwei Tabellen mehrere unabhängige Beziehungen, die verschiedene Sachverhalte repräsentieren. Jede Beziehung muss mit einer aussagekräftigen Bezeichnung


## SQL-Anwendungen & Befehle

### 1. Datenbank erstellen & Tabellen definieren (DDL)
```sql
CREATE DATABASE BeispielDB;

USE BeispielDB;

CREATE TABLE Kunden (
    KundenID INT PRIMARY KEY,
    Name VARCHAR(100),
    Adresse VARCHAR(200)
);

CREATE TABLE Bestellungen (
    BestellID INT PRIMARY KEY,
    Bestelldatum DATE,
    KundenID INT,
    FOREIGN KEY (KundenID) REFERENCES Kunden(KundenID)
);
```

### 2. Erweiterte DDL & DML Beispiele
Erstellen einer Tabelle mit mehreren Fremdschlüsseln
```
CREATE TABLE Mitarbeiter (
    MitarbeiterID INT PRIMARY KEY,
    Name VARCHAR(100),
    AbteilungID INT,
    VorgesetzterID INT,
    FOREIGN KEY (AbteilungID) REFERENCES Abteilungen(AbteilungID),
    FOREIGN KEY (VorgesetzterID) REFERENCES Mitarbeiter(MitarbeiterID)
);
```
Hinzufügen einer neuen Spalte zu einer bestehenden Tabelle
```
ALTER TABLE Kunden ADD Email VARCHAR(100);
```
Ändern des Datentyps einer Spalte
```
ALTER TABLE Kunden MODIFY Name VARCHAR(150);
```
Löschen einer Spalte aus einer Tabelle
```
ALTER TABLE Kunden DROP COLUMN Email;
```
Erstellen eines Indexes auf einer Spalte
```
CREATE INDEX idx_KundenName ON Kunden(Name);
```
Erstellen einer Tabelle mit einer CHECK-Bedingung
```
CREATE TABLE Mitarbeiter (
    MitarbeiterID INT PRIMARY KEY,
    Name VARCHAR(100),
    Alter INT,
    CHECK (Alter >= 18)
);
```
Erstellen einer Tabelle mit einem zusammengesetzten Primärschlüssel
```
CREATE TABLE Bestellpositionen (
    BestellID INT,
    ProduktID INT,
    Menge INT,
    PRIMARY KEY (BestellID, ProduktID)
);
```
DML (Data Manipulation Language)
Einfügen von mehreren Datensätzen in eine Tabelle
```
INSERT INTO Kunden (KundenID, Name, Adresse)
VALUES
    (1, 'Max Mustermann', 'Musterstraße 1'),
    (2, 'Erika Mustermann', 'Musterstraße 2');
```
Abfragen von Daten mit WHERE-Bedingung
```
SELECT * FROM Kunden WHERE Name = 'Max Mustermann';
```
Aktualisieren von mehreren Datensätzen
```
UPDATE Kunden SET Adresse = 'Neue Adresse 1' WHERE KundenID = 1;
```
Löschen von Datensätzen mit einer WHERE-Bedingung
```
DELETE FROM Kunden WHERE KundenID = 1;
```
Abfragen von Daten mit ORDER BY
```
SELECT * FROM Kunden ORDER BY Name DESC;
```
Zählen der Anzahl der Datensätze in einer Tabelle
```
SELECT COUNT(*) FROM Kunden;
```
Verwendung von Aggregatfunktionen (SUM, AVG, MAX, MIN)
```
SELECT SUM(Menge) FROM Bestellpositionen WHERE BestellID = 1;
```
Verwendung von JOINs
```
SELECT Kunden.Name, Bestellungen.BestellID
FROM Kunden
JOIN Bestellungen ON Kunden.KundenID = Bestellungen.KundenID;
```
