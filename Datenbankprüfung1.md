# Datenbankprüfung 1 

## Teil 1: Theoriefragen & Konzepte

### 1. Was ist der Unterschied zwischen einer relationalen und einer dokumentenbasierten Datenbank?
- **Relationale Datenbank**: Speichert Daten in Tabellen, die miteinander durch Schlüssel (Fremd- und Primärschlüssel) verbunden sind. Ideal für strukturierte Daten und komplexe Abfragen.
- **Dokumentenbasierte Datenbank**: Speichert Daten in JSON- oder BSON-Formaten, die flexibler und schemalos sind. Ideal für unstrukturierte oder sich ändernde Daten.

### 2. Welche Normalformen gibt es und warum sind sie wichtig?
- **1. Normalform (1NF)**: Alle Attribute müssen atomar sein, keine wiederholten Gruppen oder Arrays in einer Zelle.
- **2. Normalform (2NF)**: Die Tabelle ist in 1NF und alle Nicht-Schlüsselattribute hängen voll funktional vom gesamten Primärschlüssel ab (Eliminierung partieller Abhängigkeiten).
- **3. Normalform (3NF)**: Die Tabelle ist in 2NF und keine Nicht-Schlüsselattribute hängen transitiv vom Primärschlüssel ab.
- **Bedeutung**: Normalisierung verhindert Redundanz und Inkonsistenzen in der Datenbank und sorgt für Datenintegrität.

### 3. Wann verwendet man eine Zwischentabelle?
- Bei **m:n-Beziehungen** (z. B. ein Mitarbeiter kann mehrere Projekte haben, und ein Projekt hat mehrere Mitarbeiter). Die Zwischentabelle speichert die Verknüpfung (z. B. `Mitarbeiter_Projekte` mit den Fremdschlüsseln `Mitarbeiter_ID` und `Projekt_ID`).

### 4. Was ist eine Identifying vs. Non-Identifying Relationship?
- **Identifying Relationship**: Der Fremdschlüssel in der Kind-Tabelle ist Teil des Primärschlüssels der Kind-Tabelle (z. B. Bestellposition in einer Bestellung).
- **Non-Identifying Relationship**: Der Fremdschlüssel in der Kind-Tabelle ist nicht Teil des Primärschlüssels der Kind-Tabelle (z. B. Mitarbeiter → Abteilung).

### 5. Welche Probleme entstehen durch Redundanz in einer Datenbank?
- **Dateninkonsistenz**: Unterschiedliche Daten zu derselben Entität.
- **Höherer Speicherbedarf**.
- **Schwierigerer Datenpflege und -aktualisierung**.

### 6. Was ist der Unterschied zwischen einem Primärschlüssel und einem Fremdschlüssel?
- **Primärschlüssel**: Ein eindeutiges Attribut, das jede Zeile in einer Tabelle eindeutig identifiziert.
- **Fremdschlüssel**: Ein Attribut in einer Tabelle, das auf den Primärschlüssel einer anderen Tabelle verweist, um eine Beziehung zwischen den Tabellen herzustellen.

### 7. Warum ist ein Primärschlüssel immer eindeutig?
- Ein Primärschlüssel stellt sicher, dass jeder Datensatz in einer Tabelle eindeutig identifiziert werden kann. Er verhindert doppelte Datensätze, weil er nur einmalig sein darf.

### 8. Warum dürfen Fremdschlüssel NULL sein? Wann nicht?
- **NULL erlaubt**: Wenn eine Entität keine Beziehung zu einer anderen Entität hat (z. B. ein Mitarbeiter ohne Vorgesetzten).
- **NULL nicht erlaubt**: Wenn die Beziehung erforderlich ist (z. B. wenn jeder Mitarbeiter einen Vorgesetzten haben muss).

### 9. Was ist ein zusammengesetzter Primärschlüssel?
- Ein zusammengesetzter Primärschlüssel besteht aus mehr als einem Attribut, um eine Zeile eindeutig zu identifizieren. Zum Beispiel kann eine Bestellposition mit einer Bestellnummer und einer Produkt-ID eindeutig identifiziert werden.

### 10. Was sind Constraints? Nenne drei Beispiele.
- **Constraints** stellen Regeln dar, die die Integrität der Daten sichern.
  - **NOT NULL**: Ein Attribut darf nicht NULL sein.
  - **UNIQUE**: Werte in einer Spalte müssen eindeutig sein.
  - **CHECK**: Werte müssen einer bestimmten Bedingung entsprechen (z. B. `CHECK (alter >= 18)`).

### 11. Was ist der Unterschied zwischen 1:1, 1:n und m:n Beziehungen?
- **1:1**: Ein Datensatz in einer Tabelle ist mit höchstens einem Datensatz in einer anderen Tabelle verbunden.
- **1:n**: Ein Datensatz in der ersten Tabelle ist mit mehreren Datensätzen in der zweiten Tabelle verbunden.
- **m:n**: Mehrere Datensätze in der ersten Tabelle sind mit mehreren Datensätzen in der zweiten Tabelle verbunden.

### 12. Wie wird eine rekursive Beziehung in SQL dargestellt?
- Eine rekursive Beziehung tritt auf, wenn ein Datensatz auf einen anderen Datensatz derselben Tabelle verweist (z. B. ein Mitarbeiter, der einen anderen Mitarbeiter als Vorgesetzten hat).
  - Beispiel: 
    ```sql
    ALTER TABLE mitarbeiter ADD COLUMN vorgesetzter_id INT;
    ```

### 13. Wann braucht man eine Hierarchietabelle statt einer rekursiven Beziehung?
- Eine Hierarchietabelle ist erforderlich, wenn es mehrere Vorgesetzte oder Beziehungen gibt (z. B. bei einer Netzwerkstruktur).

### 14. Welche Probleme können bei Fremdschlüsseln auftreten?
- **Referentielle Integrität**: Wenn ein Datensatz in der übergeordneten Tabelle gelöscht wird, könnte dies zu fehlerhaften Verweisen in der untergeordneten Tabelle führen.
  - Lösungen: `ON DELETE CASCADE`, `ON DELETE SET NULL`.

### 15. Wann sollte ein Fremdschlüssel ON DELETE CASCADE oder ON DELETE SET NULL haben?
- **ON DELETE CASCADE**: Wenn beim Löschen eines Datensatzes alle zugehörigen Datensätze in der untergeordneten Tabelle auch gelöscht werden sollen.
- **ON DELETE SET NULL**: Wenn der Datensatz in der übergeordneten Tabelle gelöscht wird und die Beziehung zu den untergeordneten Datensätzen verloren geht, aber diese nicht gelöscht werden sollen.

---

## Teil 2: SQL-Anwendungen & Befehle

### 1. Datenbank erstellen & Tabellen definieren (DDL)
```sql
CREATE DATABASE firma CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE firma;

CREATE TABLE mitarbeiter (
    id INT AUTO_INCREMENT PRIMARY KEY,
    vorname VARCHAR(50) NOT NULL,
    name VARCHAR(50) NOT NULL,
    geburtsdatum DATE NOT NULL,
    telefon VARCHAR(20),
    fk_abteilung INT,
    FOREIGN KEY (fk_abteilung) REFERENCES abteilungen(id)
);
