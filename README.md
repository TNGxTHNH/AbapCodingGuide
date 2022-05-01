# AbapCodingGuide


### ABAP CODING GUIDE FOR NEWBIES – Für eine bessere Laufzeit
## Inhaltsverzeichnis
1. [General Info](#general-info)
2. [Datenbank](#technologies)
3. [Interne Tabellen](#installation)
4. [Quellenverzeichnis](#collaboration)
5. [Literaturverzeichnis](#faqs)



### General Info 
Dieser Guide richtet sich an Anfänger bzw. Leute, die mit der ABAP Programmierung anfangen wollen, ein wichtiger Bestandteil der Programmierung ist die Effizienz und Performance in einem SAP System. Bei einer kleinen Menge von Daten, spielt der Programmierstil eine untergeordnete Rolle, da man keine spürbare Laufzeit Veränderung erkennen kann, aber sobald es um eine höhere Menge an Daten geht, muss man auf seinen eigenen Programmierstil achten, damit es zur keinem Verlust der Laufzeit kommt. Der Hauptkern dieses GUIDES liegt in der Sprache SQL und die internen Tabellen von ABAP. Die Sprache SQL ist besonders wichtig, da SAP den OpenSQL Standard benutzt und man dadurch SQL-Befehle mit ABAP verknüpfen kann. Außerdem bietet die SAP HANA Datenbank, die Sprache SQLScript an, die syntaktisch dem OpenSQL ähnelt. Mithilfe von SQLScript ist es möglich direkt auf der Datenbankebene zu programmieren. Die internen Tabellen sind in ABAP besonders wichtig, da sie dynamisch auf dem Arbeitsspeicher erzeugt werden können, man kann sie mit Arrays oder Listen von anderen Programmiersprachen vergleichen.

### Die Datenbank
In diesem Abschnitt geht es darum wie man eine bessere Laufzeit rausholen kann, mithilfe der Datenbank und den SQL-Befehlen. 


| Was ist eine Datenbank und SQL? | 
| ------------------ | 
| Eine Datenbank ist eine organisierte Sammlung von strukturierten Informationen oder Daten, die auf ein Computersystem gespeichert sind. Die Datenbank wird mithilfe eines Datenbankverwaltungssystems (DBMS) gesteuert. Zusammen wird die Datenbank und das -verwaltungssystem als Datenbanksystem bezeichnet.SQL ist eine Datenbanksprache. Mit ihr kann man Daten wie Tabellen und Spalten, in einer Datenbank abfragen, verändern, hinzufügen oder löschen. Mithilfe von OpenSQL, kann man SQL-Befehle mit dem ABAB-Code kombinieren. | 

#### SQL-Hinweise
Um eine performante Ausführung von Programmen mit Datenbankzugriff sicherzustellen. Sollte man Datenbankzugriffe, Treffermenge, übertragene Datenmenge, Suchaufwand und Datenbanklasten versuchen möglichst klein zu halten, dies erreicht man durch gut überlegte SQL-Befehle. Zusätzlich werden wichtige SQL-Befehle anhand von Beispielen erklärt, um den Inhalt des dieses Kapitels besser zu verstehen.

| SQL-Befehl | Bedeutung | Beispiel |
|:--------------|:-------------:|--------------:|
| SELECT | Mit dem SELECT-Befehl kann man eine Spalte in einer Tabelle selektieren. | SELECT * FROM Kunde.(Bei diesem Beispiel fragen wir alle Spalten in der Tabelle Kunde ab.) |
| * | Der * bedeutet, dass man alle Spalten in der Tabelle abfragt. | SELECT * FROM Kunde. (Bei diesem Beispiel fragen wir alle Spalten in der Tabelle Kunde ab.)|
| FROM | Mit der FROM Befehl wählen wir die Tabelle aus, für die Abfrage | SELECT name[Spaltenname] FROM Kunde. (Bei diesem Beispiel fragen die Spalte „name“ von der Tabelle Kunde. |
| WHERE | Mit der WHERE Bedingung, kann man eine Abfrage filtern. Der WHERE Befehl stellt eine Bedingung, die erfüllt werden muss, damit eine Ergebnismenge geliefert werden kann. | SELECT alter FROM Kunde WHERE alter > 18.(Bei diesem Beispiel fragen wir in der Tabelle Kunden, die Spalte alter ab, aber nur die dessen alter höher als 18 sind und kriegen als Ergebnis nur Kunden dessen alter höher als 18 sind.) |
| Vergleichsoperatoren <;>;=;<=;>= | Mit den Vergleichsoperatoren können wir eine Abfrage noch besser filtern. Die Bedeutungen der Vergleichsoperatoren „>:= größer“, „< := kleiner“, „= := gleich“, „>= := größer gleich“, „<= := kleiner gleich“ | SELECT alter FROM Kunde WHERE alter >= 18 AND alter <= 25.(Bei diesem Beispiel fragen wir in der Tabelle Kunden, die Spalte alter ab und kriegen als Ergebnis das die Kunden vom Alter 18 -25 Jahre.) |
| Logische Operatoren AND; OR; NOT | Die logischen Operatoren vergleichen Bedingungen miteinander. Beim AND müssen alle Bedingungen erfüllt sein. Beim OR musst mindestens eine Bedingung erfüllt sein. Beim NOT muss die Bedingung nicht erfüllt sein | SELECT alter, geschlecht FROM Kunde WHERE alter = 18 AND geschlecht = ‚männlich‘. (Bei diesem Beispiel fragen wir die Spalte alter und geschlecht, der Tabelle Kunde ab, mit der Bedingung das sie genau 18 Jahre alt und männlich sind.) SELECT alter, geschlecht FROM Kunde WHERE alter = 18 OR geschlecht = ‚männlich‘. (Bei diesem Beispiel fragen wir die Spalte alter und geschlecht, der Tabelle Kunde ab, mit der Bedingung das sie genau 18 Jahre alt oder männlich sind. Hier können wir auch weibliche Kunden kriegen, dessen alter 18 Jahre alt ist.) SELECT geschlecht FROM Kunde WHERE NOT geschlecht = ‚männlich‘. (Bei diesem Beispiel fragen wir die Spalte geschlecht der Tabelle Kunde ab, mit der Bedingung das keiner männlich sein darf und würden als Ergebnis nur weiblich kriegen. |
| GROUP BY | Mit dem Befehl GROUP BY, können wir ausgewählte Daten gruppieren. Der Vorteil bei dem Befehl ist, dass man die Aggregatsfunktionen anwenden kann. | SELECT rubrik, SUM(Seitenanzahl) FROM buecher WHERE rubrik='Horror' GROUP BY rubrik; (Als Ergebnis der Abfrage, erhält man 1560) |
| Aggregatsfunktionen COUNT(), MIN(), MAX(), SUM(), AVG()  | COUNT zählt die ausgewählten Datensätze ab. SUM addiert alle ausgewählten Datensätze zusammen. AVG berechnet den Durchschnittswert aller ausgewählten Datensätze zusammen. MAX liefert den größten Wert des ausgewählten Datensatzes. MIN liefert den kleinsten Wert des ausgewählten Datensatzes. | SELECT COUNT(*) FROM kunde.(Zählt alle Spalten der Tabelle Kunde auf) SELECT SUM(alter) FROM kunde. (Addiert alle Spalten alter zusammen.) SELECT AVG(alter) FROM kunde. (Berechnet das Durchschnittsalter der Tabelle Kunden.) SELECT MAX(alter) FROM kunde. (Gibt das älteste Alter von der Tabelle Kunde aus.) SELECT MIN(alter) FROM kunde. Gibt das niedrigste Alter von der Tabelle Kunde aus.) |
| HAVING | Ist ähnlich der WHERE Bedingung, aber HAVING dient als Bedingung für GROUP BY. | SELECT Rubrik, SUM(Seitenanzahl) AS Summe_Seiten FROM buecher GROUP BY Rubrik HAVING Summe_Seiten >500 (Als Ausgabe würden wir die Rubrik mit der Summe der Seitenzahl kriegen, die über 500 haben. Horror mit einer Seitenzahl von 1560 Thriller mit einer Seitenzahl von 956) |
| JOINS INNER JOIN LEFT  (OUTER) JOIN RIGHT (OUTER) JOIN  | Der JOIN ermöglicht es eine Selektion über mehrere Quellen durchzuführen (Datenbanktabellen und CDS-Views). Der INNER JOIN liefert die Schnittmenge zwischen den Tabellen. Beim LEFT/ RIGHT OUTER JOIN werden alle Datensätze der linken/rechten Tabelle ausgegeben und zusätzlich zu der rechten/linken Tabelle existieren, dazu ergänzt. | INNER JOIN: SELECT sf~carrid sf ~ connid sf ~ fldate  FROM sflight AS sf INNER JOIN splfi AS sp ON sf ~ carrid = sp ~ carrid  AND sf ~ connid = sp ~ connid WHERE sf ~ carrid = ‚AA‘ INTO @DATA(lt_fluganzeige) (In diesem Beispiel selektieren wir carrid connid und fldate und geben ihnen den Aliasnamen sf mit dem ~Zeichen von der Tabelle slfight. Jetzt JOINEN wir slfight mit splfi und es als Ergebnis kriegen wir die Schnittmenge wo carrid= AA ist und packen sie in die interne Tabelle lt_fluganzeige.) LEFT OUTER/RIGHT OUTER JOIN:  SELECT sf ~ carrid sf ~ connid sf ~ fldate FROM sflight AS sf LEFT/RIGHT JOIN splfi AS sp ON sf ~ carrid = sp ~ carrid AND sf ~ connid = sp ~ connid WHERE sf ~ carrid = ‚AA‘ INTO @DATA(lt_fluganzeige)(In diesem Beispiel selektieren wir carrid connid und fldate und geben ihnen den Aliasnamen sf mit dem ~ Zeichen von der Tabelle slfight. Jetzt LEFT/RIGHT JOIN wir sie mit der Tabelle spfli und kriegen als Ergebnis die Schnittmenge carrid = AA und zusätzlich die rechte/linke Datensätze von der Tabelle und packen sie in die interne Tabelle lt_fluganzeige.) |

- Versuche immer den SELECT * Befehl zu vermeiden, wenn man vorher die erforderlichen Felder kennt, da man ansonsten die komplette Datenbank durchläuft und dies sich negativ auf die Laufzeit wirkt.
- Versuche HAVING/WHERE Klauseln zu verwenden, um die aufgerufenen Daten einzuschränken, um nicht unnötig durch die Datenbank zu durchlaufen.
- Versuche verschachtelte SELECT-Befehle zu vermeiden, denn jeder SELECT Befehl, bedeutet einen Durchgang durch die Datenbank und dies hat wiederum Auswirkungen auf die Laufzeit.

| Beispiel am Code für eine verschachtelte SELECT-Abfrage: |
| ------------------ | 
| SELECT * FROM VBAK INTO TABLE t_vbak WHERE… LOOP AT t_vbka. SELECT * FROM vbap APPENDING TABLE t_vbap WHERE vbeln = t_vbak-vbeln. … ENDLOOP. |
| In diesem Beispiel führen wir für jeden vbak ein SELECT aus, um die Positionsdaten zu lesen. Um eine geschachtelte SELECT- Abfrage zu lösen, kann man JOINS oder das FOR ALL ENTRIES benutzen. |

| Wichtige ABAP Begriffe kurz erklärt  |
| ------------------ | 
| LOOP AT.. (wir laufen durch eine Tabelle) <br> ENDLOOP (Wir beenden den durchlauf der Tabelle) <br> DATA (wir deklarieren eine Variable mit einem Datentyp) <br> TYPE TABLE OF (wir definieren uns einen Tabellentyp) <br> INTO TABLE (damit ABAP weißt, dass es sich um eine interne Tabelle handelt) <br> APPEND (wir fügen einen Wert der Tabelle hinzu) <br> WRITE (Wir geben etwas auf die Konsole aus) <br> FIELD-SYMBOL (kann man sich wie ein Zeiger vorstellen, der mithilfe des LOOP, durch eine Tabelle geht) | 
| SELECT * FROM VBAK INTO TABLE t_vbak WHERE… LOOP AT t_vbka. SELECT * FROM vbap APPENDING TABLE t_vbap WHERE vbeln = t_vbak-vbeln. … ENDLOOP. |
| Beispiel am Code: <br> DATA: lt_sflight TYPE TABLE OF sflight <br> lt_grpdaten TYPE TABLE OF sflight. <br> SELECT * FROM sflight <br> INTO TABLE <br> lt_sflight. <br> LOOP AT lt_slight ASSIGNING FIELD-SYMBOL (<fs_gruppe>) <br> GROUP BY ( key1 = <fs_gruppe>-planetype Key2 = <fs_gruppe>-seatsmax). <br> WRITE : <fs_gruppe>-planetype, <br> <fs_gruppe>-seatsmax. <br> Append <fs_gruppe> TO lt_grpdaten. <br> ENDLOOP. |
| In diesem Beispiel definieren wir 2 interne Tabellen mit den Tabellentypen sflight. Wir selektieren mithilfe des SELECTS Befehl alle Spalten der Tabelle sflight und füllen sie mit Hilfe des Befehls INTO TABLE, in die interne Tabelle lt_sflight (Interne Tabellen werden im Kapitel 3 nochmal ausführlich erklärt). Jetzt laufen wir mit Hilfe des FIELD-SYMBOL, durch und gruppieren nach Flugzeugtyp und maximale Sitzplätze. Wir geben sie mit den Befehl WRITE einmal auf der Konsole aus und fügen sie danach in die interne Tabelle lt_grpdaten hinzu mit APPEND. Dies führt der Code solange aus bis alle Daten übernommen wurden und verlässt die LOOP mit ENDLOOP. |

- Versuche innerhalb eines LOOPS, SELECT Befehle zu vermeiden und benutze stattdessen „JOINS“ oder „FOR ALL ENTRIES“.
- Das Prinzip von „FOR ALL ENTRIES“ ist es, anstatt für jeden Eintrag einer Tabelle einen SELECT auf eine andere Tabelle zu ausführen, macht man einen SELECT-Befehl auf die Tabelle und übergeben die die Werte, für die selektiert werden soll, direkt mit.
- Der Vorteil bei einen „FOR ALL ENTRIES“ ist, dass er performanter arbeitet als durch eine Tabelle zu loopen mit einzelnen SELECTs.
- Durch die Benutzung vom FOR ALL ENTRIES, kann man sich die notwendigen Felder in eine RANGES-Tabelle übertragen zu müssen, ersparen. 

| Wichtige ABAP Begriffe kurz erklärt | 
| ------------------ | 
| RANGES-Tabelle <br> Eine Range Tabelle ist eine interne Tabelle mit dem gleichen Aufbau wie eine Selektionstabelle. <br> Selektionstabelle <br> Eine Selektionstabelle ist eine interne Tabelle mit dem Typ STANDARD TABLE, mit einem Standardschlüssel und mit einer Kopfzeile. In Selektionstabellen werden komplexe Selektionen auf standardisierte Weise abgespeichert. Ihr Hauptzweck ist es, mit Hilfe des WHERE-Zusatzes in Open SQL-Anweisungen die Selektionskriterien direkt in Datenbankabgrenzungen umzusetzen. | 
| Beispiel am Code: <br> DATA: it_mara TYPE TABLE OF mara, <br> wa_mara TYPE mara. <br> DATA: it_makt TYPE TABLE OF makt,<br> wa_makt TYPE makt. <br> <br> IF it_mara IS NOT INITIAL. <br> SELECT * FROM makt <br> INTO TABLE it_makt <br> FOR ALL ENTRIES IN it_mara <br> WHERE matnr = it_mara-matnr. <br> ENDIF. |
| In diesem Beispiel deklarieren wir als erstes eine interne Tabelle mit den namen it_mara mit dem Tabellentyp mara mit einer Struktur vom Typ mara, dass gleiche machen wir im nächsten für die interene Tabelle it_makt mit der Struktur makt. Jetzt prüfen wir mit hilfe des „IF-Anweisung“, ob die interne Tabelle schon befüllt ist, in diesem Fall ist sie leer und dadurch springen wir in den Code. Wir selektieren mithilfe des SELECTS Befehl alle Spalten der Tabelle makt und füllen sie mit Hilfe des Befehls INTO TABLE, in die interne Tabelle it_makt. Jetzt Filtern wir mit dem „FOR ALL ENTRRIES IN it_mara WHERE matnr = it_mara-matnr“ alle identische Matrikelnummer aus und verlassen danach die „IF-Anweisung“ mit „ENDIF“. |

- Sollte die interne Tabelle zu viele Daten haben, kann es zu einen Laufzeitfehler kommen, da sie dynamisch erzeugt werden und keine festen Größen hat.
- Eine interne Tabelle sollte immer gefüllt sein, da es ansonsten zu keiner Einschränkung durch die WHERE Klausel kommt.
 
- Benutze Aggregatsfunktionen, wie MIN, MAX, AVG, SUM, um die Datenbanklast klein zu halten. Die Berechnung findet dann im Datenbanksystem statt.

| Beispiel am Code |
| ------------------ |
| SELECT COUNT(*){MIN(), MAX(), SUM(), AVG()}  FROM persons <br> INTO count <br> WHERE city = 'NEW YORK'. |

Eine kurze Zusammenfassung dieses Abschnittes für eine optimale Laufzeit mithilfe von SQL-Befehlen an der Datenbank. Das Ziel dieses Kapitels ist es dem Datenbankserver zu entlasten, indem man 
- eine Optimale Suchabfrage ausführt
- eine Zeilenreduzierung mithilfe von WHERE/HAVING Klauseln
- Benutzung von Aggregatsfunktionen, damit weniger Daten übertragen werden müssen
- Benutzung von JOINS/FOR ALL ENTRIES anstatt verschachtelten SELECT-Abfragen

### 3. Interne Tabellen
In diesem Abschnitt geht es um die internen Tabellen, worauf man achten und welche man verwenden sollte, um eine bessere Laufzeit zu erreichen. Das Hauptaugenmerk liegt auf der HASHED- sowie SORTED-Tabelle, da sie die besseren Laufzeiten bieten, als die STANDARD Tabelle.s

| Wichtige ABAP Begriffe kurz erklärt |
| ------------------ |
| Was sind interne Tabellen? <br> Interne Tabellen sind Konstrukte, die Daten in einer Tabellenform speichern. Die internen Tabellen existieren nur während der Laufzeit im Arbeitsspeicher. Es gibt 3 Typen von internen Tabellen: <br> HASHED-Tabelle <br> SORTED-Tabelle <br> Standard-Tabelle <br>
Wofür braucht man eine interne Tabelle? <br> Interne Tabellen werden immer dann verwendet, wenn Datenmengen einer festen Struktur programmintern verarbeitet werden. Ein wichtiges Einsatzgebiet ist z.B. die programminterne Speicherung und Aufbereitung von Inhalten aus Datenbanktabellen. Weiterhin sind interne Tabellen ein wichtiges Mittel, um komplexe Datenstrukturen in einem ABAP-Programm zu implementieren. <br> Was ist der Unterschied zwischen einer Datenbanktabelle? <br>
Im Gegensatz zu einer Datenbanktabelle, haben interne Tabellen keine festgelegten Größen und existieren nur auf dem Arbeitsspeicher. Dadurch das sie auf dem Arbeitsspeicher existieren, erfolgt der Zugriff schneller als normale Datenbanktabellen. Eine Datenbanktabelle kann man mit der Transaktion SE11 (ABAP Dictionary) anlegen. |

- Verwende wenn möglichst eine HASHED-Tabelle, ansonsten die SORTED-Tabelle und als letztes die STANDARD-Tabelle.
- Bei einem eindeutigen Schlüssel (UNIQUE KEY) können keine mehrfachen Einträge in internen Tabellen vorkommen. 
- Bei einem nicht eindeutigen Schlüssel (NON UNIQUE KEY) darf eine Zeile in der internen Tabelle auch mehrfach vorkommen.
- KEYS, sind dazu da, um interne Tabellen zu definieren
- Dadurch, dass Inhalte einer internen Tabelle solange bleiben, bis sie überschrieben werden, muss sollte man die Tabelle ab und zu mit CLEAR löschen, damit keine komischen Ergebnisse kommen

#### Hashed-Tabellen

| Wichtige ABAB Begriffe kurz erklärt |
| ------------------ |
| Was sind HASHED-Tabellen? |
| Bei Hash-Tabellen wird kein Index erzeugt, der Zugriff erfolgt über einen eindeutigen Schlüssel. Der Schlüssel kann aus einem oder auch mehreren Feldern bestehen. HASHED-Tabellen sind am besten geeignet für große Tabellen, da durch den Hash-Algorithmus die Anwortzeit konstant bleibt. Der Schlüssel bei Hash-Tabellen muss eindeutig sein und zum Lesezugriff passen. |

- HASHED-Tabellen bieten die beste Laufzeit an, da sie ungeordnet sind und das hinzufügen am Ende der Tabelle passiert. Man kann es sich wie eine Warteschlange vorstellen, wo am Ende der Schlange einer hinzukommt.
- Die Zugriffszeit beim Lesen einer HASHED-Tabelle ist nicht abhängig von der Anzahl der Datensätze, deswegen ist sie gut geeignet für große Tabellen.
- HASHED Tabellen werden für große Tabellen benutzt, die einmal gefüllt und dann nicht mehr verändert werden müssen.
- HASEHD Tabellen können UNIQUE KEY oder DEFAULT KEY sein.
- Mit dem Schlüssel können Zeilen eindeutig identifiziert werden.
- Der Nachteil einer HASHED-Tabelle ist, dass sie einen eindeutigen Schlüssel besitzen und man keine kopierte HASHED-Tabelle speichern kann.

| HASHED Tabelle erstellen mit und ohne Schlüssel |
| ------------------ |
| 1. Beispiel am Code: <br> DATA: it_itab TYPE HASHED TABLE OF lt_typ <br> WITH UNIQUE KEY thandy. <br> 2. Beispiel am Code: <br> DATA: it_kunde TYPE <br> HASHED TABLE OF lt_long <br> WITH UNIQUE DEFAULT KEY. |
| Im ersten Beispiel erstellen wir eine HASHED Tabelle mit einem eindeutigen Schlüssel thandy, für den Zugriff.Im zweiten Beispiel erstellen wir eine HASHED Tabelle it_kunde mit dem Typ lt_long, mit einem DEFAULT KEY. Mit dem DEFAULT KEY werden alle Felder einer internen Tabelle als Standardschlüssel definiert. |

| Eine Tabelle füllen anhand eines Beispiels: |
| ------------------ |
| read table lt_hash into ls_hash with feld1 = 'T'. <br> if sy-subrc <> 0. <br> ls_hash-feld1 = ... <br> ls_hash-feld2 = ... <br> INSERT ls_hash INTO TABLE lt_hash. <br> endif. |
| Wir lesen die Tabelle lt_hash mit dem Schlüssel ‚T‘. Setzen die Feldr ls_hash-feld1, usw mit einem Wert gleich. Zum Schluss wird mit dem INSERT ls_hash INTO TABLE lt_hash die Datensätze in die Tabelle hinzugefügt. |

### SORTED-Tabellen
| Wichtige ABAP Begriffe kurz erklärt |
| ------------------ |
| Was ist eine SORTED- Tabelle? <br> Eine SORTED Tabelle, wird wie der Name schon sagt, direkt sortiert abgespeichert. Der Schlüssel in der SORTED Tabelle kann eindeutig oder nicht-eindeutig sein. |

- SORTED Tabellen werden für Tabellen benutzt, die immer sortiert sein müssen, Stück für Stück gefüllt oder modifiziert werden müssen und in einer bestimmten Reihenfolge abgearbeitet werden.


| Beispiel Code für die Erstellung einer SORTDED Tabelle |
| ------------------ |
| 1. Beispiel mit eindeutigem Schlüssel. |
| DATA lt_itab TYPE SORTED TABLE OF slfight <br> WITH UNIQUE KEY carrid. |
| 2. Beispiel mit nicht-eindeutigem Schlüssel. |
| DATA it_itab TYPE SORTED TABLE OF sflight <br> WITH NON-UNIQUE KEY DEFUALT KEY. |
| Im ersten Beispiel erstellen wir eine sortierte Tabelle mit dem Typ sflight und dem Schlüssel carrid. Jetzt werden die Einträge beim Hinzufügen nach der carrid sortiert gespeichert. <br> Im zweiten Beispiel erstellen wir eine sortierte Tabelle mit dem Typ sflight und einem nicht-eindeutigen default Schlüssel, dadurch werden alle Felder als Standardschlüssel definiert. Jetzt erfolgt der Zugriff über den Index. |

- Beim Schlüsselzugriff hängt die Antwortzeit logarithmisch von der Anzahl der Tabelleneinträge ab, da der Zugriff über eine binäre Suche erfolgt
- Der Aufbau der Tabelle ist langsamer, da er vorher sortiert werden muss.
- WHERE- Klauseln sind bei SORTED-Tabellen schneller, wenn die Schlüsselfelder optimal sortiert wurden
 
| Beispiel am Code.  |
| ------------------ |
| Wir suchen das Schlüsselfeld S1 <br>
Die optimale Variante <br> LOOP AT lt_demo <br> WHERE S1 = 'ABC'. <br>ENDLOOP. <br>
Hier loopen wir durch die Tabelle bis wir das Schlüsselfeld S1 mit dem Wert „ABC“ erreichen. <br> Die nicht optimale Variante, für das Schlüsselfeld S1 <br>LOOP AT lt_demo <br> WHERE S2 = 'XYZ' <br> AND S3 = '123' <br> AND S4 = '0'. <br>ENDLOOP. <br>
Wir suchen das Feld S1, haben aber keine optimale WHERE Klausel eingebaut und deswegen wird man durch die ganze Tabelle loopen. |

### STANDARD- Tabellen
| Wichtige ABAP Begriffe kurz erklärt |
| ----------------------------------- |
| Was ist eine Standard Tabelle? <br> Bei einer Standard Tabelle erfolgt der Zugriff über einen nicht-eindeutigen Schlüssel oder durch den Index.  Dadurch, dass die Standardtabelle keinen Primärschlüssel hat, können sie Datensätze mehrfach in der Tabelle vorkommen. |

- STANDARD Tabellen werden für kleine Tabellen verwendet, in denen Indizierung zu mehr Kosten als Nutzen führen würden („Pseudo-Arrays“).
- Die Standard Tabelle kann sehr schnell gefüllt werden, da nicht nach Redundanz geprüft wird.
- Je mehr Zeilen, desto länger dauert die Laufzeit, da oft die komplette Tabelle durchsucht wird, um den betreffenden Satz zu finden.

| STANDARD Tabelle erstellen |
| -------------------------- |
| Beispiel am Code <br>  DATA lt_itab TYPE STANDARD TABLE OF sflight. <br> Wir erstellen eine interne Standard Tabelle mit dem Typ sflight. |


| STANDARD Tabelle Daten hinzufügen |
| --------------------------------- |
| APPEND <wa> TO <itab> <br> Mit APPEND fügen wir Daten <wa> in die Tabelle <itab> |
  
### Zusammenfassung vom Kapitel
  In diesem Kapitel ging es allgemein um die internen Tabellen, da sie in der ABAP Programmierung eine wichtige Rolle spielen. Es wurden die 3 Laufzeiten der Tabelle erklärt, welche bevorzugt verwendet werden sollten und welche man vermeiden kann. Zum Schluss gibt es eine Abbildung von allen 3 internen Tabellen mit Zugriffsarten und Komplexität.
- Interne Tabellen sind wie Arrays, sie werden während der Laufzeit erzeugt
- die HASHED-Tabelle ist von der Laufzeit am besten
- die SORTED-Tabelle, für Tabellen die sortiert werden müssen.
- die STANDARD-Tabelle sollte wegen der Laufzeit, wenn möglichst vermieden werden.
- die Verarbeitungsgeschwindigkeit nimmt bei allen 3 internen Tabellen je nach größe ab, das bedeutet wie mehr Inhalt die Tabelle besitzt, desto länger ist die Laufzeit. <br>
  
Bei HASHED- sowie SORTED-Tabellen fügen wir Daten mit INSERT <wa> INTO <itab> hinzu und bei STANDARD-Tabellen mit APPEND <wa> TO <itab>.

 (Abbildung)
Auf der Abbildung sind die Laufzeiten für alle 3 Tabellen bei unterschiedlichen Zugriffsarten aufgelistet.
Beim normalen lesen (READ TABLE tab WITH KEY) bleibt die Laufzeit O(n), da wir einen kompletten Durchlauf machen und die Laufzeit abhängig von der Tabellengröße ist. <br>
Beim Lesen mit einem Index (READ TABLE tab INDEX), ist die Laufzeit O(1), da wir den Index direkt eingeben und die Tabelle sie uns wieder gibt. Bei einer HASHED-Tabelle ist ein Zugriff über den Index nicht möglich.
 
## Quellenverzeichnis
https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Performance+and+Tuning
https://tricktresor.de/blog/verwendung-von-for-all-entries-2/
https://www.berater-wiki.de/Select_for_all_entries
https://www.dsag.de/sites/default/files/dsag_handlungsempfehlung_abap_2016.pdf
https://www.berater-wiki.de/Hashed_Tabellen_und_Sorted_Tabellen
https://www.denisreis.com/interne-tabellen-in-abap/#hash
https://infocient.de/blog/sap-grundlagen/was-ist-sap-hana-teil-3-code-pushdown-transformationen/
https://mind-forms.de/sap-formulartechnologien/abap-entwicklung-unter-sap-hana-sqlscript/
https://blogs.sap.com/2014/09/26/code-push-down-for-hana-from-abap-starts-with-open-sql/
http://www.sql-lernen.de/having.php
https://help.sap.com/doc/abapdocu_752_index_htm/7.52/de-de/abaptypes_itab.htm
https://www.berater-wiki.de/Der_Schl%C3%BCsselbefehl_LOOP_AT_im_neuen_ABAP_mit_GROUP_BY
https://help.sap.com/doc/abapdocu_751_index_htm/7.51/de-DE/abenranges_table_glosry.htm
https://help.sap.com/saphelp_nwpi71/helpdata/de/9f/dba71f35c111d1829f0000e829fbfe/content.htm?no_cache=true
https://help.sap.com/saphelp_46c/helpdata/de/fc/eb35de358411d1829f0000e829fbfe/content.htm?no_cache=true
https://www.tricktresor.de/blog/geschachtelter-select/
https://www.tricktresor.de/blog/verwendung-von-for-all-entries-2/
https://www.denisreis.com/tabellenviews-und-joins-in-abap/
https://help.sap.com/doc/abapdocu_751_index_htm/7.51/de-DE/abapselect_join.htm

## Literaturverzeichnis
Felix Roth. (2017). ABAP Objects Das umfassende Handbuch Rheinwerk Publishing

  
