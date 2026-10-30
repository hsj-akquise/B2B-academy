# Technisches Lastenheft – für Ivan / B2B Academy
Version 1.0, 30.10.2026 · Umsetzungsgrundlage; keine bereits implementierten Funktionen

## Referenzlook
An **akquise-sales-relaunch** orientieren: #0e2a5a Dunkelblau, #cc1f1f Rot, Weiß, #f7f8fa Hintergrund, Inter/ähnliche Sans, großzügige Typografie, klare abgerundete Karten. Der Prototyp `index.html` zeigt diese Richtung. Das echte Markenlogo und weitere freigegebene Assets aus dem Relaunch übernehmen; nicht vom Browser automatisch fremde Ressourcen kopieren.

## System
- WordPress als CMS; LearnDash für LMS/Zugangs- und Fortschrittsverwaltung.
- H5P für interaktive Videos, Branching Scenarios, Quiz und Lernkarten.
- WooCommerce für Einzelmissionen, Kurs-Bundles, Spezialmissionen, Expertenstunden, Listen/Analysen und Side by Side.
- Eigenes schlankes WordPress-Plugin (mit wartbarer Datenstruktur und Rollen/Rechten) für individuelles Firmenprofil, Trainingsergebnisse, Reality-Mirror, Side-by-Side-Aufträge und Berichte.
- KI über serverseitige Schnittstelle, keine Schlüssel im Browser, Kosten-/Token-/Minutenbegrenzungen.
- Sprachsimulation als separat testbare Ausbaustufe, KI-Antworten nicht mit tatsächlichen Gesprächen verwechseln.
- Download/Export von Ergebnissen, möglichst Excel/CSV und PDF; unabhängig von einem bestimmten Kunden-CRM.

## Screens (Informationsarchitektur)
**Öffentliche Website**: Einstieg, wertorientierte Produktdarstellung, Test-Szenario, Einzelmissionen, transparentes Bundle-/Upgrade-Angebot, Side by Side, Servicekatalog, Fragen, Impressum/Datenschutz.
**Privater Teilnehmerbereich**: Onboarding-Firmenbriefing; Mission Control mit Fortschritt und nächstem sinnvollen To-do; Missionen/Lektionen; H5P-Training; KI-Feedback; Kompetenzbild; eigene Artefakte; Reality-Mirror; Buchungen und Rechnungen; Datenschutz-/Löschfunktionen.
**Internes Projektportal**: Teilnehmer- und Mandantenzuordnung, Bestellungen, Briefingprüfung/Freigabe, Projektstatus, Aktivitäten & Zeiterfassung, Gesprächsnotizen, menschliche Review-Freigabe, Ergebnisbericht, Folgetermin.

## Datenmodell (minimal)
`organization` (mandant_id, Firmenname, Angebot, Markt, USP, Wettbewerber, Referenzen); 
`participant` (user_id, mandant_id, Rolle, gekaufte Module);
`learning_artifact` (mission, user_id, Typ, Inhalt, Version, Freigabe);
`assessment` (Rubric-Version, Score, Feedback, Übung, Evidenz);
`order_and_entitlement` (WooCommerce-Order, Produkt, Zeitraum, Preis, Anrechnung);
`side_project` (mandant, Preisklasse, Stundenlimit, Status, Freigabe, Zielkunden);
`contact_attempt` (Projekt, Kunde, Status, Zeit, zulässige Grundlage/Prüfvermerk);
`conversation_note` (Datum, Rolle, Inhalt, Zitatmodus, beobachtete Reaktion, Bedarf, Empfehlung, Prüfer);
`market_report` (Quellenhinweise, Zusammenfassung, Einschränkungen).
Versionierung und Audit-Trail vorsehen. Datenzugriffe strikt nach mandant_id und Rolle.

## Kernabläufe
- Einzelkauf von Mission 4 öffnet Mission 4 direkt, kein Zwang zu Mission 1–3.
- Bundle DIGITAL öffnet 1–6; EXPERT zusätzlich Termin und manuelle Konzeptprüfung.
- Anrechnung innerhalb von 90 Tagen für zuvor tatsächlich bezahlte Module (Deckelung auf Bundlepreis); Stornos/Rabatte/Mehrfachkäufe korrekt behandeln.
- Side by Side unabhängig vom Bundle kaufbar, aber **operative Freigabe erst nach gültigem Briefing und menschlicher Prüfung**.
- Kundenliste vom Teilnehmer ODER als separater Rechercheauftrag.
- Nach telefonischem Entscheiderdialog ausführliche Notiz; KI darf vorstrukturieren, Mensch prüft Zitat/Emotion/Bedarf/Status.
- Aus freigegebenem, für den Mandanten zulässigem Fall entsteht eine Reality-Mirror-Aufgabe; vorab klare Quelle/Status kennzeichnen.
- Zusatzleistungen: bezahlbare 30-/60-Minuten-Sessions, Markt-/Wettbewerber-/Listenpakete, kein „unbegrenzt“.

## Sicherheit und Recht
DSGVO-Datenminimierung, Berechtigungsmodell, AVV mit Dienstleistern, Löschung/Export, Sicherung, Logging, Rate Limiting und Backups; Schutz von KI-Schlüsseln, Servervalidierung aller Rechte, sichere Dateiuploads. Kundenbezogene Daten nicht als globale KI-Trainingsdaten verwenden. Kein unbefugtes Gesprächsaufzeichnen. B2B-Rechtshinweise in Trainings und Freigabeprozess. Überprüfung möglicher Fernunterrichtsregeln, AGB, Widerruf/Verträge und Mehrwertsteuer vor Livegang.

## Phasen / Priorität
**MVP 1:** Branding, funktionsfähige Login-/Kurs-/Shop-Basis, 1 vollständig spielbare H5P-Referenzmission „Einwand-Labor“, Formular-Onboarding, regelbasiertes Feedback; Side-by-Side-Projektstatus zunächst manuell.
**MVP 2:** KI-Textfeedback, Modul-Upgrades, alle 6 Kursgrundgerüste, Freigabeprozess und Gesprächsnotiz, Mandantentrennung.
**MVP 3:** Sprache, adaptiver Trainingspfad, automatisierte Berichte, erweiterter Reality-Mirror, individueller Markt-Cockpit.
Ausnahme/Fehlermodi: Zahlung fehlgeschlagen, Doppelkäufe, 0 freigeschaltete Missionen, keine Gesprächsnotizen, kein Einverständnis, fehlender Briefinginhalt, KI nicht erreichbar.

## Tests und Definition of Done
- Mobile, Desktop, Tastaturbedienung, Verständlichkeit; Preisauszeichnung korrekt.
- Rollenwechsel (Mitarbeiter/GF), nur eigene Mandantendaten sichtbar.
- Kaufen/Storno/Upgrade/Sperren einer Einzelmission, Zahlungssicherheitsprüfung.
- H5P-Ergebnisse korrekt erfasst; keine Annahme, dass H5P-Fertigstellung automatisch LearnDash-Fortschritt ist.
- KI-Bewertungen nachvollziehbar, nicht erfunden, bei Unsicherheit nachfragen.
- Projekt startet nicht vor fachlicher Freigabe.
- Kein Live-Link und keine als funktionierend angepriesene Integration ohne Testnachweis.
- Pilot: 10 zahlende Academy-Teilnehmer, 3 Side-by-Side-Projekte; echte Zeiten/Supportaufwand und Lernverbesserung messen.

## Vorhandene Dateien
`index.html`: responsive Konzeptwebsite, lokale JavaScript-Demo, **kein** Produktivsystem.
`docs/KONZEPT.md`, `docs/PRICING.md`: Produkt und Planpreise.
Weitere Dateien dieses Repo: Lernreise/Originalinhalte, Side-by-Side-Standards, Projekt-Roadmap.

**Wichtig:** Nicht autonom produktiv deployen, keine Kundendaten importieren, keine Gebühren einziehen ohne Freigabe der Geschäftsführung.
