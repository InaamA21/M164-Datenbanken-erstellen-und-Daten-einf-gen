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
### Gibt den größten Wert in einer Spalte oder Gruppe zurück
SELECT MAX(salary) FROM employees;
## GROUP BY
### Gruppiert Daten, basierend auf dem Inhalt einer oder mehrerer Spalten
SELECT customer_id, SUM(order_total) FROM orders GROUP BY customer_id;
## HAVING
### Gibt nach der Gruppierung nu die an die die Anforderungen erfühlt
SELECT customer_id, SUM(order_total) FROM orders GROUP BY customer_id HAVING SUM(order_total) > 500;

