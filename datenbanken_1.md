# DATENBANKEN 1

## 1. EINFÜHRUNG

### 1.1 DAS KONZEPT DES DATENBANKSYSTEMS

**Begriff der Datenbank:**

> Eine Datenbank ist eine integrierte Ansammlung von Daten, die allen Benutzern eines Anwendungsbereiches als gemeinesame Basis aktueller Information dient.

**DBMS:** *Datanbankmanagementsystem* 
> Das DBMS ist ein Softwaresystem, das es ermöglicht, eine Datenbank zu definieren, Daten zu speichern, zu verändern und zu löschen, sowie Anfragen an die Datenbank zu stellen. 

Ein DBMS isoliert die DB von den Anwendungsprogrammen, sodass der Programmierer die Details der Datenbank nicht kennen muss. 

### 1.2 Datenbanksysteme und traditionelle Datenverwaltung

**Dateisysteme** (file systems), als konventionelle Form der Verwaltung großer Datenmengen.

#### COBOL 

COBOL wurde in den 70er 80er entwickelt, und hat eine wichtige Rolle bei der Datenverarbeitung gespiert vor der Einführung von relationalen Datenbanken.

**Satz:** ist eine Gruppierung von **Datenelementen a.k.a. Felder**.

**Satztyp:** difiniert welche Datenelementen den Satz aufbauen. z.B.: 

````
Satztyp 		ANGESTELLTER
Datenelemente 	ANGNR 			Angestelltennummer
				NAME 			Name des Angestellten
				W-ORT 			Wohnort
				GEHALT 			Gehalt
				PERS 			Persönliche Daten;
								Zahl der Kinder usw
````

**Datei:** ist eine benannte Sammlung von Sätzen. 

**Dateisystem**

> Ein **Dateisystem** ist ein Softwarepaket, das den Zugriff auf einzelne Sätze in einer Datei besort, wenn das Anwendungsprogramm die entsprechenden Parameter liefert. 

**Schlüssel** werden benutzt um Datein aufzurufen.

**Dateiorganisation**
> Die Speicherung der Sätze einer Datei kann unterschiedlich organisiert werden, üblich sind: *sequentielle Organisation, index-sequentielle Organisationen, direkte Organisationen* (z. B. Hash-Verfahren).````FD 		ANGESTELLTEN-DATEI
		DATA RECORD IS ANGESTELLTER; ... .
01 		ANGESTELLTER; ... .
		02 ANGNR PIC 9(5);
		02 NAME PIC X(30);
		02 W-ORT PIC X(30);
		02 PERS; ... .
		02 GEHALT; ... .````
Es herrscht also eine enge Kopplung zwischen Programm und Datei, dies führt zu schwierige probleme:

#### Probleme der traditionelle Datenverwaltung
1. **Redudanz**
> Da die Daten jeweils speziell für bestimmte Anwendungen entworfen werden, werden dieselben Daten in verschiedenen Dateien wieder auftauchen. Redundanz führt zu Speicherverschwendung und zu erhöhten Verarbeitungskosten, vor allem bei Änderungen. Schlimmer jedoch ist es, dass diese Redundanz in der Regel nicht zentral kontrolliert wird, so dass Konsistenzprobleme auftreten. 2. **Inkonsistenz**
> Die Konsistenz der Daten (d.h. die logische Übereinstrimmung der Datei-Inhalte) kann nur schwer gewährleistet werden. Bei der Änderung einer Gröse müssten alle Dateien geändert werden, die diese Größe beinhalten. und diese verschiedene Programme zum selben Zeitpunkt unterschiedliche Werte derselben Größe sehen können.3. **Daten-Programm-Abhängigkeit**
> Ändert sich der Aufbau einer Datei oder ihrer Organisationsform, so müssen darauf basierende Programme geändert werden. [...]4. **Inflexibilität**> Da die daten nicht in ihrer Gesamtheit, sondern nu anwendungsbezogen gesehen werden, ist es in vielen Fällen sehr kompliziert, neue Anwendungen oder Auswerungen vorhandener Daten zu realisieren. Dies gilt insbesondere für Auswertungen, die Daten aus verschiedenen Daeien benötigen würden. Die Organisation nach diesem konventionellen Vorgehen ist sehr wenig anpassungsfähig an die sich verändernden Anforderungen in einem Unternehmen. 
Um die probleme zu lösen wurden Daten als eingesdtändiges Betriebsmittel eines Unternehmens. Dazu ist auch die Trennung von Programm und Daten, **die Datenunabhängigkeit**, zentral. 
**Integrität der Daten:** Korrektheit und Vollständigkeit der abgespeicherten Daten. 
> Die zentrale Verwaltung der Daten durch das DBMS ermöglicht es, bei Änderung von Daten Kontrollroutinen einzuschalten oder von Zeit zu Zeit mit Hilfe spezieller Prüfprogramme nach Integritätsverlet-zungen zu suchen.
#### Vorteile der Datenbank-Philosophie:
1. Es gibt eine gemeinsame Basis für alle Anwendungen.
2. Redundanz entfällt.
3. Keine Konsistenzprobleme der traditioneller Dateiorganisationen. (wegen pt. 2)
4. Die Anwendungsprogrammierung wird einfacher. Der Programmierer muss nur die Eigenschaften der Daten kennen, nicht wie die gespeichert sind.
5. Application-Data abhängigkeit wird reduziert. 
6. DBS verschafft mehr flexilibität für diue Datenauswertung.
7. Daws DBS kann zentral die Korrektheir von Daten überprüfen. 
