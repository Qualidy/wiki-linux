# Einführung

#  Open Source & Proprietäre Software


## Open Source

### Die Grundlagen – Was bedeutet "Quellcode"?
Der Quellcode enthält eine Reihe von Befehlen, die logisch miteinander verbunden sind. Er beschreibt, was das Programm tun soll:

**Input**: Was wird benötigt (z. B. die Eingabe eines Benutzers).
Verarbeitung: Was mit den Daten geschehen soll (z. B. die Zahlen addieren, einen Text filtern).  
**Output**: Was am Ende sichtbar oder nutzbar sein soll (z. B. das Ergebnis auf dem Bildschirm ausgeben).Der Prozess:

```mermaid
---
config:
    look: handDrawn
---
flowchart LR
    A[Quellcode] -->|Wird durch| B(Uebersetzer Compiler Interpreter)
    B -->|Erzeugt| C["Maschinencode (Computervariablen)"]
```



**Compiler**: (z. B. bei C++ oder Java) Ein Compiler liest den gesamten Quellcode einmal und übersetzt ihn dann vollständig in eine separate ausführbare Datei (.exe unter Windows). Dieser Code besteht nur noch aus Nullen und Einsen (Maschinensprache) und kann vom Computer direkt ausgeführt werden.

**Interpreter**: (z. B. bei Python oder JavaScript) Ein Interpreter liest den Quellcode Zeile für Zeile. Er führt jede Zeile aus und geht dann zur nächsten. Es gibt keine separate, fertige ausführbare Datei.

| Spaltenöberschrift 1 | spalte 2 |
|----------------------| -|
| twat | hshua| 



Unterschiede von Quellcode Proprietär und Open Source


| Merkmal                | Proprietär                                                     | Open Source   |
| -|-|-|                                                  
| **Wer besitzt den Code?**    | Ein einzelnes Unternehmen (Vendor Lock-in).                          | Die Gemeinschaft (Community) und Lizenzen.                            |
| **Verfügbarkeit des Codes?** | Nein. Der Code ist ein Geschäftsgeheimnis.                           | Ja. Der Code ist frei zugänglich.                                     |
| **Was kauft man?**           | Das Nutzungsrecht (die Lizenz).                                      | Zugangsrechte                                                         |
| **Vergleichs-Analogie**      | Ein Auto, dessen Motor nur der Hersteller sehen und reparieren darf. | Ein LEGO-Set, dessen Bauanleitung und alle Teile frei verfügbar sind. |




Modell A: Proprietäre Software (Geschlossenes System)
Proprietäre Software ist das, was wir meistens mit "kommerziell" in Verbindung bringen.

:fontawesome-solid-magnifying-glass: Wie funktioniert es?

Der Kern: Der Quellcode wird streng geheim gehalten. Man erhält nur die fertige ausführbare Datei (den Binärcode).
Lizenzierung: Man kauft eine Lizenz, die lediglich das Recht zur Nutzung des Programms für eine bestimmte Zeit und auf bestimmte Geräte gewährt.
Nachteil: Man ist vom Anbieter abhängig. Wenn das Unternehmen pleitegeht oder die Nutzungsbedingungen ändert, sind Sie oft machtlos.  

**Vorteile**:

Benutzerfreundlichkeit: Oft sehr poliert, intuitiv und durch Marketing optimal vermarktbar.
Support: Garantierte professionelle Hilfe und Wartung vom Hersteller.
Stabilität: Der Entwickler garantiert die Kompatibilität und Updates.  

**Nachteile**

Transparenz-Mangel: Man weiß nicht, was "im Hintergrund" passiert (Black Box).
Kosten/Lock-in: Man zahlt für die Nutzung und ist an das Ökosystem des Anbieters gebunden.
Keine Kontrolle: Man kann das Programm nicht selbst ändern oder verbessern.


Modell B: Open-Source-Software (Offenes System)
Open Source bedeutet, dass die "Baupläne" nicht geheim sind.

:fontawesome-solid-magnifying-glass: Wie funktioniert es?

Der Kern: Der Quellcode ist frei zugänglich. Die Nutzung wird durch eine sogenannte Open-Source-Lizenz (z.B. GPL, MIT) geregelt. Diese Lizenzen definieren, was man mit dem Code tun darf (nutzen, kopieren, anpassen, verteilen).
Prinzip der Gemeinschaft: Die Fehlerbehebung, das Feature-Upgrade und die Weiterentwicklung erfolgen dezentral durch Tausende von Entwicklern weltweit.
Der Vorteil: Niemand kann sich "gegen" die Gemeinschaft verkaufen. Das Wissen ist verteilt.  

**Vorteile**

Transparenz: Jeder Experte kann überprüfen, ob das Programm sicherer und sauber ist (Security through Scrutiny).
Flexibilität & Kontrolle: Man kann das Programm zu seinen spezifischen Bedürfnissen anpassen.
Kosten: Meistens kostenlos nutzbar (man zahlt ggf. nur für professionellen Support/Wartung).
Kein Vendor Lock-in: Man kann das System ohne Angst vor einem Anbieterwechsel verlassen.  

**Nachteile**

Heterogenität: Das Design kann unübersichtlich sein, da viele Gruppen daran arbeiten.
Support-Fragmentierung: Der Support ist nicht immer zentralisiert (einzelne Unternehmen müssen Support einkaufen).
Komplexität: Die Einarbeitung kann anfangs komplexer sein, da die Dokumentation sehr umfangreich sein kann.



**Beispiele und Vergleichstabelle**  

| Anwendung | Typ | Anbieter/Community | Schlüssel-Argument |
| :--- | :--- | :--- | :--- |
| Microsoft Windows | Proprietär | Microsoft | Garantierter, einheitlicher Support; hohe Benutzerfreundlichkeit. |
| Adobe Photoshop | Proprietär | Adobe | Industriestandard; extrem poliertes, kommerzielles Tool. |
| Linux (z.B. Ubuntu) | Open Source | Community | Maximale Kontrolle, höchste Flexibilität, Sicherheit. |
| Firefox | Open Source | Mozilla Foundation | Nutzer können im Code mitwirken, da die Quelle frei ist. |
| Python | Open Source | Community | Riesige, frei verfügbare Bibliothek an Programmierbausteinen. |

---

***Kurzübersicht vergleich Open Source - Proprietär***  

| Frage | Open Source | Proprietär |
| :--- | :--- | :--- |
| **Was ist der größte Wert?** | Kontrolle, Flexibilität, Transparenz | Benutzerfreundlichkeit, garantierter Support, Einheitlichkeit |
| **Sicherheit?** | Transparenz des Codes (Wer sieht, ist sicherer). | Zentrale Kontrolle (Der Anbieter kümmert sich darum). |
| **Anpassbarkeit?** | Maximal (Ich kann es komplett umbauen). | Minimal (Ich nutze es so, wie es ist). |
| **Kosten?** | Meist kostenlos (Kosten fallen auf Support/Training). | Oft hohe Lizenzkosten. |
| **Das größte Risiko?** | Inkompatibilität/fehlender Standard. | Abhängigkeit vom Anbieter (Vendor Lock-in). |


{{ task(file="tasks/module1/opensource_vs_properitär_1.yaml") }}
{{ task(file="tasks/module1/opensource_vs_properitär_2.yaml") }}
{{ task(file="tasks/module1/opensource_vs_properitär_3.yaml") }}







