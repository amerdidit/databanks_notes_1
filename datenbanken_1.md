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
## 2. Architektur eines DBS
### 2.1 Drei Datenebenen
#### Logische Gesamtsicht

Die Beschreibung  der Gesamtheit der Daten des betrachteten Anwendungsbereiches. Alle Daten werden auf logischer Ebene in Form von Informationseinheiten und deren Beziehungen untereinander beschrieben.

#### Interne Sicht

Wie die Daten auf den Speichern organisiert werden. Muss für die Zugriffsanforderungen der verschiedenen Benutzer optimiert werden.
#### Externe Sichten
Verschiedene Darstellung der Daten für verschiedene Benutzergruppen.
-----
* Der Benutzer arbeitet Ausschließlich über die Externe Schicht. Das DBMS übernimmt die notwendigen Umsetzungen von einer *externen Schicht -> logische Gesamtsicht -> Interne Sicht*
* **Schema:** Jede Ebene Besitzt ein **Daten Model** was mit einer **Datenbescheibungsspache** beschrieben weird. Es gibt also:
 * Verschiedene externe Schemata
 * Ein konzeptuelles Schema
 * Internes Schema
 
 ![image](img/database-architecture.png)
 
### 2.2 Das konzeptuelle Modell

* Logische Gesamtsicht.
* Versucht die Realität abzubilden: alle Daten, und alle Beziehungen dieser Daten.
* **Integritätsbedingungen:** Beschreiben die Vorschriften zur Existenz dieser Daten, und zur Änderung dieser Daten. (Preconditions & Effects)
* Die Operationen die auf die Daten ausgeführt werden werden hier auch festgelegt.
> Bei den heute verbreiteten Relationen Datenbanksystemen gibt es diese Spezifikation von Operationen im konzeptuellen Schema der Datenbank nicht. Alle diese Systeme bieten sogenannte **generische Operationen** an, also Operationen, die auf alle Datentypen in der Datenbank anwendbar sind. Dies sind unter anderem speichern, lesen, löschen und modifizieren. Der Zugriff auf die Datenbank erfolgt mittels einer **Datenmanipulationssprache**, die diese Operationen zur Verfügung stellt.
*  **Objektorientierten Datenbanken**: jüngere Datenbanken wo Operationen als teil vom Schema festgelegt wurden.
* **Datenbescheibungsprache** *data definition language, DDL* ist für die Beschreibung des konzeptuelle Model geignet.



> Beachten Sie den Unterschied zwischen den Begriffen „Datenbanksystem“ und „Informationssystem“. Leider werden beide Begriffe oft synonym verwendet. Das Informationssystem eines Unternehmens ist die Gesamtheit aller Instanzen und Prozesse, die die für das Unternehmen wichtige Information von außen aufnehmen, verarbeiten und entsprechende Information nach außen wieder abgeben. Das Datenbanksystem ist damit nur ein Teil des Informationssystems, nämlich derjenige Teil, in dem die Informationsbasis des Unternehmens verwaltet wird.

#### Vorteile des Konzeptuellen Modells:

1. Bietet einen stabilen Bezugspunkt für alle Anwendungen dar.
2. Stellt eine einheitliche Dokumentation wesentlicher Aspekte des Unternehmens dar.
3. Gebrauch der Daten kann zentral kontrolliert werden.
4. Schafft die wesentliche Vorraussetzungen für Datenunabhängigkeit der Anwendungsprogramme.

### 2.3 Das interne Modell

