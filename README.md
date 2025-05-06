# Lernjournal Inaam: Relationale Datenbanken & SQL

## 1. Tag - 18.02. (Dienstag)
### Thema: Einführung in Datenbanken und SQL
- **Ziel:** Auffrischen von Fachbegriffen (z.B. Tabellen, Relationen, Kardinalitäten), Normalisierung (1NF, 2NF, 3NF)
- **Themen:** ERM und ERD am Beispiel "Tourenplaner"
- **Praxis:** Installation von MySQL/MariaDB auf Xampp, Docker oder AWS
- **Ziel:** Erstellen eines ERD (Entity-Relationship-Diagramms) für den Tourenplaner in 1NF, 2NF und 3NF.

## 2. Tag - 25.02. (Dienstag)
### Thema: Generalisierung, Spezialisierung und DDL
- **Ziel:** Erweiterung des ERD mit Generalisierung/Spezialisierung (is_a-Beziehung)
- **Themen:** Identifizierende vs. nicht-identifizierende Beziehungen, Einführung in DDL (Data Definition Language)
- **Praxis:** Erstellen einer Datenbank und Tabellen mit MySQL Workbench (Forward Engineering)
- **Ziel:** DDL-Befehle (CREATE TABLE, CHARSET) verwenden.

## 3. Tag - 04.03. (Dienstag)
### Thema: Datentypen und Mehrfachbeziehungen/ LB1 Prüfung geschrieben 
- **Ziel:** Einführung in SQL-Datentypen, Mehrfachbeziehungen (n:m-Beziehungen), Rekursion und Hierarchien (inkl. BOM-Problem)
- **Praxis:** Erstellen von Tabellen mit verschiedenen Datentypen und Beziehungen (z.B. n:m-Beziehung)
- **Ziel:** Arbeiten mit DML (SELECT I, SELECT II, INSERT) und einfache Datenabfragen.

## 4. Tag - 11.03. (Dienstag)
### Thema: Referentielle Integrität und JOINs
- **Ziel:** Arbeiten mit FK-Constraints (Fremdschlüssel-Constraints), Mengenlehre und Mengenoperationen (Union, Intersection, etc.)
- **Praxis:** Erstellen und Testen von JOIN-Abfragen (INNER JOIN, LEFT JOIN, RIGHT JOIN)
- **Ziel:** DML-Befehle mit JOINs üben, Aggregatfunktionen verwenden (COUNT, SUM).

## 5. Tag - 18.03. (Dienstag)
### Thema: Datenintegrität und Constraints
- **Ziel:** FK-Constraint-Optionen und deren Anwendung
- **Praxis:** Üben von SELECT ... WHERE ... Abfragen, mit speziellen Filterbedingungen (z.B. Subquery)
- **Ziel:** Sicherstellen der referenziellen Integrität und Anwendung von WHERE- und HAVING-Klauseln.

## 6. Tag - 25.03. (Dienstag)
### Thema: Subqueries und Bulk Import
- **Ziel:** Einführung in Subqueries (Subselects), Arbeiten mit `LOAD DATA INFILE` (Bulk Import von CSV-Dateien)
- **Praxis:** Import von CSV-Daten und Anwendung von Subqueries in komplexeren Abfragen
- **Ziel:** Subqueries erstellen und Daten aus CSV-Dateien in eine normalisierte Datenbank importieren.

## 7. Tag - 01.04. (Dienstag)
### Thema: Backup und Normalisierung
- **Ziel:** Backup und Wiederherstellung von Datenbanken (DUMP erstellen, Tools verwenden)
- **Praxis:** Erstellen von Backups und Import von normalisierten Daten in eine Datenbank
- **Ziel:** Daten sichern und in eine normalisierte DB importieren.

## 8. Tag - 08.04. (Dienstag)
### Thema: Praxisarbeit und Vorbereitung auf LB2
- **Ziel:** Übung mit OpenData-Projekten
- **Praxis:** CSV-Daten in einer normalisierten Datenbank strukturieren
- **Ziel:** Arbeiten an OpenData-Projekten und Datenbanknormalisierung (bis 3. Normalform).

## 9. Tag - 15.04. (Dienstag)
### Thema: LB2 Prüfung geschrieben 
- **Ziel:** Vertiefung und Wiederholung der wichtigsten Konzepte
- **Praxis:** Arbeiten mit den erstellten Datenbankprojekten (Prüfungssimulation)
- **Ziel:** Fertigstellung der Praxisarbeit für LB2.

## 10. Tag - 06.05. (Dienstag)
### Thema: Common Table Expressions & Stored Procedures
- **Ziel:** Einführung in CTEs und deren Anwendung, Erstellung und Nutzung von Stored Procedures
- **Praxis:** Arbeiten mit CTEs und Stored Procedures in einer komplexeren Abfrage
- **Ziel:** Abgabe des Lernjournals/Dossiers und Abschluss der praktischen Übungen.

---

## Zusammenfassung der Lernziele und Übungen pro Tag:

| **Tag** | **Thema** | **Lernziel** | **Übung/Beispiel** |
|---------|-----------|--------------|---------------------|
| 18.02. | Einführung, Normalisierung, ERM | Fachbegriffe auffrischen, Normalformen verstehen | Erstellen eines ERD für den Tourenplaner (1NF, 2NF, 3NF) |
| 25.02. | Generalisierung, DDL, Spezialisierung | Generalisierungsbeziehungen in ERD anwenden | Erstellen einer Datenbankstruktur mit MySQL Workbench |
| 04.03. | Datentypen, Mehrfachbeziehungen | Datenbank mit verschiedenen Datentypen erstellen | SELECT, INSERT, Mehrfachbeziehungen testen |
| 11.03. | Referentielle Integrität, JOINs | Arbeiten mit Fremdschlüssel-Constraints und JOINs | JOINs mit INNER, LEFT, RIGHT und FULL OUTER |
| 18.03. | Datenintegrität, DQL, DCL | Verständnis der Datenintegrität und Anwendung von SELECT | Übung mit WHERE, HAVING, und Subqueries |
| 25.03. | Subqueries, Bulk Import | Subqueries erstellen und Bulk Import üben | CSV-Daten importieren, Subquery-Abfragen |
| 01.04. | Backup, Normalisierung | Erstellen und Wiederherstellen von Backups | Normalisierte Daten in die DB importieren |
| 08.04. | Praxisarbeit, Vorbereitung LB2 | Übung und Wiederholung zur Vorbereitung | Arbeiten an OpenData-Projekten und CSV-Import |
| 15.04. | LB2 Prüfung | Intensives Üben und Simulieren der praktischen Prüfung | Pfrüfungeschrieben |
| 06.05. | CTEs, Stored Procedures | Einführung in fortgeschrittene SQL-Techniken | Arbeiten mit CTEs und Stored Procedures |

---

## Quizfragen zur Selbstkontrolle

1. Was sind die Hauptunterschiede zwischen den Normalformen 1NF, 2NF und 3NF?
2. Erkläre den Unterschied zwischen einer Identifizierenden und einer Nicht-Identifizierenden Beziehung.
3. Was ist der Zweck von **JOINs** in SQL?
4. Was versteht man unter referenzieller Integrität?
5. Wie kannst du einen Bulk-Import in eine MySQL-Datenbank durchführen?
6. Was ist der Unterschied zwischen einem INNER JOIN und einem LEFT JOIN?

## Themen Notizen 
### ![Notizen zur LB1](https://github.com/InaamA21/M164-Datenbanken-erstellen-und-Daten-einf-gen/blob/main/Grund_Informationen.md) 
### ![Notizen zur LB2](https://github.com/InaamA21/M164-Datenbanken-erstellen-und-Daten-einf-gen/blob/main/SELECT_Datensicherung.md)
### ![CTEs Befehle](https://github.com/InaamA21/M164-Datenbanken-erstellen-und-Daten-einf-gen/blob/main/Common-Table-Expressions-CTEs.md)

