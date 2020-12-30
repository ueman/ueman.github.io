---
title: "Release Strategien für mobile Anwendungen"
date: 2020-03-09T11:18:39+01:00
draft: true
---

Dieser Artikel ist über mobile Release Strategien aus der Sicht einer Agentur.


### Welche Release Strategien gibt es?
(Sortiert nach Benutzung absteigend)

- Release Zyklen (80%)
    - wöchentlich, monatlich, ...
- Durch Marketing bestimmt (40%)
    - Promotions, Events,..
- Qualitätsgetrieben (25%)
    - Jeder von der QS akzeptierte Build wird veröffentlicht
- Feature-Based (20%)
- Size-Based (10%)
- Willkür (5%)

### Vorteile von kurzen Release Zyklen
- Nur ca. 14% der Nutzer haben Auto-Updates deaktiviert
    - Wobei es hier auch [gegensätzliche](https://www.androidpolice.com/2020/01/05/weekend-poll-is-your-phone-set-to-update-apps-on-the-play-store-automatically/) Umfragen gibt 
- Nutzer erwarten häufige Updates
- Bei gleicher Funktionalität bevorzugen 61% der Nutzer die App die vor kurzem geupdatet wurde
- Spielt gut mit MVPs zusammen
- Design muss nicht feststehen und kann sich entwickeln
- Apps stehen und fallen mit der Usability & UX (und ihrem Mehrwert)
- Schnellere Reaktionen auf Produkte von Konkurrenten
- Schnellere Fehlerbehebungen möglich
- Apps mit häufigen Updates werden in den Stores höher geranked (->ASO)
- Kleinere Updates haben geringere Chancen Fehler zu beinhalten
- Wenn Fehler auftreten, können sie schneller gepatcht und ausgeliefert werden

### Möglichkeiten zur Minimierung von Risiken
- Je häufiger die Updates desto weniger Änderungen pro Update
geringeres Potential der Einführung von neuen Fehlern
- Canary Releases
    - Fehler sind auf wenige User beschränkt
    - Staged Rollouts (Android)
    - Phased Rollouts (iOS)
- Interne Quality-Gates
- Öffentliche Beta-Channel
- Sicherheitslücken können schneller gefixt werden
- Wichtig, da Software nicht in einem von uns kontrollierten Environment läuft

### Kritik
- Mehr Aufwand für Kunde, da er vorher vermutlich alles absegnen möchte
- Kunde könnte vermuten, dass mehr Updates = mehr Crashes
- “Kontrollverlust des Kunden über das Produkt”


##### Quellen
- [Release Practices for Mobile Apps -- What do Users and Developers Think?](https://ieeexplore.ieee.org/abstract/document/7476674/)