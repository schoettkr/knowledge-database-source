+++
title = "Einführung in die Funktion von Computersystemen - Lecture 03: Von Neumann Rechner"
author = ["eo shiru"]
date = 2019-10-15
lastmod = 2019-12-03T10:28:38+01:00
tags = ["uni", "funktion-computersysteme"]
draft = false
+++

## Von-Neumann-Architektur {#von-neumann-architektur}

-   1946: ENIAC als erster vollständiger Rechner aus den USA
-   **EDVAC**: Konzept des stored program computer von _John von Neumann_
    -   Speicher enthält Programm & Daten

{{< figure src="/knowledge-database/images/von-neumann-architektur.png" >}}

Abstrakt gesehen besteht die Informationsverarbeitung in der Von-Neumann-Architektur aus drei Stufen:

1.  Datengewinnung und -eingabe
2.  Verarbeitung und Speicherung
3.  Datenausgabe

Diese Stufen sollten sich in Geräten zur Informationsverarbeitung wiederspiegeln.

{{< figure src="/knowledge-database/images/von-neumann-rechner.png" >}}

-   John v. Neumann veröffentlichte erstmals die nach ihm benannten Prinzipien des Rechnerentwurfs, nachdem er für das Manhattan-Projekt beim Entwurf des EDVAC (Electronic Discrete Variable Automatic Computer) mitgearbeitet hatte


### Von-Neumann-Prinzipien {#von-neumann-prinzipien}

-   ein Rechner besteht aus **Rechenwerk**, **Steuerwerk**, Speicher und Ein-/Ausgabegeräten
-   die Zentraleinheit arbeitet **taktgesteuert**
-   die Signale werden **binär** kodiert
-   der Inhalt eines Speicherwortes wird über eine **Adresse** angesprochen
-   der Rechner verarbeitet **externe Programme** die intern gespeichert werden
-   Programmbefehle und Daten werden im **einheitlichen Hauptspeicher** gespeichert
-   Programme und Daten werden **sequentiell** abgearbeitet; der sequentielle Programmfluss kann durch (bedingte oder unbedingte) Sprünge verändert werden
-   jede theoretisch mögliche Berechnung ist (im Rahmen der Kapazität des Rechners) **berechenbar**

Harvard Architektur vs Von Neumann Architektur:<br />
![](/knowledge-database/images/harvard-vs-neumann.png)


### Komponenten des von Neumann Rechners {#komponenten-des-von-neumann-rechners}


#### Komponenten: Bus {#komponenten-bus}

-   ein **Bus** (_bidirectional universal switch_) ist eine Verbindungseinheit zwischen verschiedenen logisch getrennten Funktionseinheiten

{{< figure src="/knowledge-database/images/bus.png" >}}


#### Komponenten: Zentrale Verarbeitungseinheit (CPU) {#komponenten-zentrale-verarbeitungseinheit--cpu}

-   ist Kernstück eines jeden Von-Neumann-Rechners
-   CPU = central processing unit (ZVE, zentrale Verarbeitungseinheit)
-   liegt häufig als ein IC (integrated circuit, integrierte Schaltung) vor
    -   Mikroprozessor (microprocessor)
-   bekannte Prozessorfamilien sind:
    -   x86, IA-32, Intel-64
    -   m68k, m88k
    -   PowerPC
    -   ARM
    -   MIPS
    -   SPARC
-   in der CPU findet die eigentliche Informationsverarbeitung statt
-   die CPU besteht mindestens aus **Rechenwerk (ALU)** und **Steuerwerk**
    -   Rechenwerk macht die Arbeit
    -   Steuerwerk bestimmt welche Arbeit gemacht werden soll
-   neben der CPU kann es noch andere Prozessoren geben die spezialisierte Aufgaben erfüllen (**Koprozessoren**) zb für: Gleitkommaarithmetik, Speichermanagement, Bus-Controller

**ALU / Rechenwerk**

-   ALU steht für arithmetic/logic unit
-   Begriffe Rechenwerk und ALU sind nicht klar unterscheidbar
-   zu den Aufgaben des Rechenwerks gehören:
    -   Ausführung **arithmetischer Operationen** wie Addition, Subtraktion, Inkrementierung Dekrementierung und Bildung von Zahlenkomplementen
    -   Ausführung **logischer Operationen** wie bitweise Negation, Disjunktion, Konjunktion, Antivalenz etc
    -   Ausführung von **Vergleichsoperationen** zwischen Zahlen
    -   Ausführung von **Schiebeoperationen** also zyklisches und nichtzyklisches Rechts- oder Linksschieben
        -   mitunter deshalb auch manchmal ALSU gennant (arithmetic/logic/shifting unit)

**ALU - Parameterschaltung**<br />

-   durch verschiedene Eingangssignale `a` und `b` kann die Parameterschaltung alle einstelligen Binärfunktionen für `y` darstellen:

{{< figure src="/knowledge-database/images/alu-parameterschaltung.png" >}}

-   durch Hinzuanehme der OR-Funktion wird die ALU **logisch vollständig**
    -   dadurch große Flexibilität

{{< figure src="/knowledge-database/images/alu-parameterschaltung2.png" >}}

-   ist die Steuerleitung `d=0` so wird **kein** Übertrag zwischen den einzelnen ALU-Kernzellen übertragen
    -   aus arithmetischen Operationen werden logische, bei denen das Ergebnis einer Bitstelle nicht von anderen Bitstellen abhängt

{{< figure src="/knowledge-database/images/alu3.png" >}}

**Steuerung ders ALU / des Rechenwerks**

-   schwarze Busse: **Datensignale**
    -   Informationen die verarbeitet werden
-   graue Busse: **Steuersignale**
    -   bestimmen, **wie** die Informationen verarbeitet werden
    -   die Steuersignale können jedoch wieder zu Datenwörtern zusammengefasst werden

{{< figure src="/knowledge-database/images/steuerung-alu.png" >}}


#### Komponenten: Status {#komponenten-status}

-   zur Realisierung von **Vergleichsoperationen** dient ein Statusregister (flag register)
-   **Flags** werden entsprechend dem Ergebnis der letzten Operation gesetzt
-   typische Flags sind:
    -   **Carry** (\\(C=c\_n\\)): eine arithmetische Operation hat einen Überlauf erzeugt
    -   **Zero** (\\(Z = \overline{q\_0 \lor q\_1 \lor ... \lor q\_{n-1}}\\)) : ein Ergebnis besteht nur aus Nullen
    -   **Negative** (\\(N=q\_n\\)): ein Ergebnis stellt eine negative Zahl dar
    -   **Overflow** ($V=c<sub>n+1</sub> &oplus; c\_n): bei einer 2er Komplement Berechnung trat ein Überlauf auf

{{< figure src="/knowledge-database/images/status.png" >}}

-   die Auswertung von Vergleichen erfolgt im Statusregister
-   Vergleich (compare) erfolgt durch Ausführung einer Subtraktion ohne Speichern des Rechenergebnisses
-   das Ergebnis des Vergleichs ist dann aus den Flags ablesbar

{{< figure src="/knowledge-database/images/status-vergleich.png" >}}


#### Komponenten: Registersatz {#komponenten-registersatz}

-   in der CPU gibt es i.d.R ein oder mehrere Register, deren Verwendungszweck nicht von vorneherein bestimmt ist
    -   &rarr; **Allzweckregister** (general purpose register)
-   diese Register kann ein Programmierer frei verwenden
-   bestimmte Register in der CPU sind auf spezielle Aufgaben spezialisert
    -   &rarr; **Spezialregister** (special purpose register)
-   Anzahl und Einsetzbarkeit von Registern stellen ein wesentliches Merkmal einer Architektur dar
-   die Gesamtheit der für den Programmierer nutzbaren Register wird Registersatz genannt

**Sichtbare und unsichtbare Register**

-   PC (_programm counter_, Befehlszähler, BZ, häufig auch IP _instruction pointer_) hält die Adresse der Speicherzelle, in der der nächste auszuführende Befehl steht
-   IR (_instruction register_, Befehlsregister, BR) speichert den gerade ausgeführten Befehl

{{< figure src="/knowledge-database/images/pc-ir.png" >}}


#### Komponenten: Control Unit / Steuerwerk {#komponenten-control-unit-steuerwerk}

-   das Steuerwerk (auch _control unit_; Steuereinheit) koordiniert das Rechenwerk, Ein-/Ausgabeeinheit und Speichersystem
-   es fungiert als Nervenzentrum
    -   sendet Steuersignale an andere Einheiten
    -   ergründet deren Status
-   wesentliche Funktionen:
    -   **sequencing** &rarr; Generierung von Steuersignale zur Abarbeitung einer beliebigen, gegebenen Instruktion (innerhalb der CPU)
    -   Steuerung/Überwachung von Speicher und E/A-System


### Interagieren mit dem Speicher {#interagieren-mit-dem-speicher}

-   Speicher dient zum Ablegen von Informationen (Daten, Programmen, Ergebnissen)
    -   es ist aus HW-Sicht im Allgemeinen nicht zu erkennen _was_ im Speicher liegt (Datentyp)
    -   die Interpretation obliegt der auf den Speicher zugreifenden Einheit
-   um Zugriff zum Speicher zu erhalten muss ein Adresssignal erzeugt werden, außerdem muss ein Steuersignal erzeugt werden, das besagt ob gelesen oder geschrieben wird
-   es gibt verschiedene Arten von Speicher:
    -   Schreiben + Lesen möglich: _random access memory_ (**RAM**, Speicher mit wahlfreiem Zugriff)
    -   nur Lesen möglich: _read only memory_ (**ROM**, nur Lese-speicher)
-   um mit dem Speicher kommunizieren zu können gibt es eine Reihe von Spezialregistern in der CPU (siehe weiter oben)
-   **MAR** (_memory adress register_, **Speicheradressierungsregister, \*SAR**)
    -   speichert die Adresse eines gesuchten Wertes im Speicher
-   **MDR** (_memory data register_, **Speicherdatenregister**, SDR)
    -   speichert den Wert, der in den Speicher geschrieben werden soll oder der aus dem Speicher gelesen wurde
-   MAR und MDR stehen dem Programmierer nicht direkt zur Verfügung

Warum werden MAR und MDR gebraucht? Es könnte ja auch direkt auf/vom das/dem betreffenden Register gelesen werden.

-   Werte auf dem Bus müssen u.U. länger anliegen
    -   die CPU interne Verarbeitung wäre solange blockiert
-   Adressen können sich aus komplexen Ausdrücken zusammensetzen
    -   MAR dient als Zwischenspeicher
-   Busse speichern keinen Wert
    -   Register dienen als Busrepräsentation (Portal)
-   aus ähnlichen Gründen gibt es innerhalb der CPU bestimmte Register, die als Portal zu nichtspeichernden Einheiten dienen
    -   bei der ALU: **Operandenregister** (meist mit X und Y bezeichnet) und **Ergebnisregister** (meist mit Z bezeichnet)


#### Speicherlesen und -schreiben {#speicherlesen-und-schreiben}

-   **Lesen**
    -   lade Adresse nach MAR
    -   setze R/W auf "Lesen"
    -   warte bis R-RDY = "okay" (MFC = memory function complete)
    -   übernehme Daten in MDR
-   **Schreiben**
    -   lade Adresse nach MAR
    -   lade Datenwert in MDR
    -   setze R/W auf "Schreiben"
    -   setze W-RDY auf "okay"
    -   warte bis R-RDY = "okay" (MFC = memory function complete)

{{< figure src="/knowledge-database/images/mar-mdr.png" >}}


### Ein- und Ausgabe {#ein-und-ausgabe}

-   die Ein- und Ausgabe an Geräte funktioniert analog zum Speicherlesen und -schreiben
-   durch eine Adresse wird ein Gerät ausgewählt; aus Sicht der CPU heißt eine solche Adresse **Port**
-   ein auf den Port geschriebener oder von dort gelesener Wert wird in bestimmten Registern zwischengespeichert
-   in manchen Architekturen wird nicht zwischen Speicher und anderen Geräten unterschieden
    -   Geräte haben speziellen Adressbereich
-   andere Architekturen besitzen spezielle Steuerleitungen für Ein- und Ausgabe
