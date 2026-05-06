# Open Source-Software und Lizenzierung


## 1. Einstieg: Was bedeutet Open Source?

**Open Source** bedeutet, dass der Quellcode einer Software öffentlich einsehbar ist.

Andere Personen dürfen den Code je nach Lizenz:

- nutzen
- verändern
- weitergeben
- in eigene Projekte einbauen

Wichtig:

!!! warning "Merke"
    Open Source heißt nicht automatisch: **Alles ist erlaubt.**

Die Rechte und Pflichten hängen immer von der jeweiligen **Lizenz** ab.

---

## 2. Unterschied: Open Source, Freeware und proprietäre Software

| Begriff | Bedeutung |
|---|---|
| Open Source | Quellcode ist öffentlich und darf je nach Lizenz genutzt, verändert und weitergegeben werden |
| Freeware | Software ist kostenlos nutzbar, der Quellcode ist aber meistens nicht offen |
| Proprietäre Software | Software gehört einem Anbieter, Quellcode ist geschlossen, Nutzung nur nach Lizenzbedingungen |

### Beispiel

**Google Chrome** ist kostenlos nutzbar, aber nicht vollständig Open Source.

**Chromium** ist das Open-Source-Projekt dahinter.

---

## 3. Warum gibt es Lizenzen?

Eine Lizenz regelt, was man mit einer Software machen darf.

Sie beantwortet Fragen wie:

- Darf ich die Software privat nutzen?
- Darf ich sie kommerziell nutzen?
- Darf ich den Code verändern?
- Darf ich den Code weiterverkaufen?
- Muss ich den ursprünglichen Autor nennen?
- Muss mein eigenes Projekt ebenfalls Open Source werden?

!!! danger "Wichtig"
    Nur weil Code öffentlich sichtbar ist, darf man ihn nicht automatisch frei verwenden.

Ohne Lizenz gilt nicht automatisch „frei verwendbar“. Im Zweifel darf man fremden Code ohne Lizenz nicht einfach nutzen.

---

## 4. Typische Open-Source-Lizenzen

### MIT-Lizenz

Die **MIT-Lizenz** ist sehr frei.

Man darf den Code:

- privat nutzen
- kommerziell nutzen
- verändern
- weitergeben
- in eigene Projekte einbauen

Pflicht:

- Copyright-Hinweis und Lizenz müssen erhalten bleiben

**Praxis:**  
Sehr beliebt bei JavaScript- und Webprojekten.

---

### Apache License 2.0

Die **Apache License 2.0** ist ähnlich frei wie MIT, aber etwas ausführlicher.

Zusätzlich enthält sie Regelungen zu Patenten.

Man darf den Code:

- nutzen
- verändern
- weitergeben
- kommerziell verwenden

Pflichten:

- Lizenzhinweise müssen erhalten bleiben
- Änderungen sollten dokumentiert werden

---

### GPL

Die **GPL** ist strenger.

Man darf den Code:

- nutzen
- verändern
- weitergeben

Aber:

Wenn man eine veränderte Version weitergibt, muss der Quellcode ebenfalls unter der GPL veröffentlicht werden.

Das nennt man **Copyleft**.

**Praxis:**  
Wichtig bei Projekten wie Linux oder WordPress.

---

### LGPL

Die **LGPL** ist eine abgeschwächte Form der GPL.

Sie wird häufig für Bibliotheken verwendet.

Eigene Software muss nicht immer komplett unter LGPL/GPL veröffentlicht werden, wenn nur eine Bibliothek eingebunden wird.

Trotzdem sollte man genau prüfen, wie die Bibliothek genutzt wird.

---

## 5. Copyleft einfach erklärt

**Copyleft** bedeutet:

Wenn jemand Open-Source-Code nutzt und daraus eine neue Version erstellt, soll diese neue Version ebenfalls offen bleiben.

Das Ziel ist, dass freie Software nicht einfach genommen und in komplett geschlossene Software verwandelt wird.

### Beispiel

Wenn ein Unternehmen GPL-Code verändert und das Produkt veröffentlicht, muss es den Quellcode der Änderungen ebenfalls offenlegen.

---

!!! note "Merksatz"
    **Open Source heißt nicht: „Mach damit, was du willst.“**

    **Open Source heißt: „Nutze es nach den Regeln der Lizenz.“**

## 6. Warum ist Lizenzierung in der Praxis wichtig?

In echten Softwareprojekten werden oft viele externe Pakete verwendet.

Beispiele:

- npm-Pakete in JavaScript-Projekten
- Composer-Pakete in PHP
- WordPress-Plugins
- Python-Bibliotheken
- Docker-Images
- Icons, Fonts und Bilder

Jedes Paket kann eigene Lizenzbedingungen haben.

Wenn man diese ignoriert, kann es später Probleme geben:

- rechtliche Abmahnungen
- Probleme bei Kundenprojekten
- Probleme bei Investorenprüfungen
- Probleme beim Verkauf eines Produkts
- Pflicht zur Offenlegung des eigenen Codes

---

## 7. Beispiel aus der Webentwicklung

Ein Entwickler baut eine Webseite mit:

- WordPress
- einem Theme
- mehreren Plugins
- einer Icon-Bibliothek
- JavaScript-Paketen
- Bildern aus dem Internet

Dann muss geprüft werden:

- Darf das Theme kommerziell genutzt werden?
- Sind die Plugins kostenlos oder kostenpflichtig?
- Welche Lizenz haben die Icons?
- Dürfen die Bilder überhaupt verwendet werden?
- Gibt es Namensnennungspflichten?
- Darf der Code verändert werden?

Gerade bei Kundenprojekten sollte man nicht einfach blind kopieren.

---

## 8. Häufige Missverständnisse

### „Es ist auf GitHub, also darf ich es benutzen.“

Falsch.

Nur weil Code öffentlich sichtbar ist, heißt das nicht, dass man ihn frei verwenden darf.

Entscheidend ist die Lizenz im Repository.

---

### „Open Source ist immer kostenlos.“

Nicht unbedingt.

Open Source kann kostenlos sein, aber Unternehmen können trotzdem Geld verdienen, zum Beispiel durch:

- Support
- Hosting
- Beratung
- Enterprise-Versionen
- Schulungen
- Zusatzfunktionen

---

### „Wenn ich nur einen kleinen Code-Schnipsel kopiere, ist das egal.“

Auch kleine Code-Stellen können urheberrechtlich geschützt sein.

In der Praxis ist das Risiko bei kleinen Standardlösungen oft geringer, aber sauber ist:

- Quelle prüfen
- Lizenz beachten
- eigenen Code schreiben

---

### „MIT und GPL sind ungefähr gleich.“

Nein.

**MIT** ist sehr frei.

**GPL** kann dazu führen, dass auch eigener Code offengelegt werden muss, wenn man die Software weiterverbreitet.

---

## 9. Praktische Checkliste für Entwickler

Vor der Nutzung eines Open-Source-Pakets prüfen:

- [ ] Gibt es eine Lizenzdatei?
- [ ] Welche Lizenz wird verwendet?
- [ ] Ist kommerzielle Nutzung erlaubt?
- [ ] Muss der Autor genannt werden?
- [ ] Muss die Lizenz mit ausgeliefert werden?
- [ ] Gibt es Copyleft-Pflichten?
- [ ] Ist das Paket aktiv gepflegt?
- [ ] Gibt es bekannte Sicherheitsprobleme?
- [ ] Passt die Lizenz zum Projekt oder Kundenauftrag?



## 12. Kurzes Quiz

### Frage 1

Was bedeutet Open Source?

??? success "Antwort"
    Der Quellcode ist öffentlich einsehbar und darf je nach Lizenz genutzt, verändert und weitergegeben werden.

---

### Frage 2

Ist Freeware automatisch Open Source?

??? success "Antwort"
    Nein. Freeware ist kostenlos, aber der Quellcode ist meistens nicht offen.

---

### Frage 3

Was regelt eine Softwarelizenz?

??? success "Antwort"
    Sie regelt, was man mit der Software machen darf und welche Pflichten man hat.

---

### Frage 4

Welche Lizenz ist eher frei und unkompliziert?

??? success "Antwort"
    Die MIT-Lizenz.

---

### Frage 5

Was bedeutet Copyleft?

??? success "Antwort"
    Veränderte oder weitergegebene Versionen müssen ebenfalls unter ähnlichen freien Bedingungen veröffentlicht werden.

---




