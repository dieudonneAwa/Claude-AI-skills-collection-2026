# PROGRESS – Claude Skills Collection

Diese Datei ist die Landkarte des Projekts. Sie zeigt jederzeit, wo wir stehen.
Sprache der README bleibt **Englisch** (Reichweite). Diese Fortschritts-Datei ist auf Deutsch.

## Geplant (das grosse Bild)
Die `README.md` ist ein kuratierter Katalog öffentlich verfügbarer Claude Skills.
Ziel: sauber, aktuell, ohne Dubletten, leicht erweiterbar – ein verlässliches Nachschlagewerk.

## Erledigt
- Repo mit voller Historie geklont (Branch `main`, Remote `origin`).
- Komplette README gelesen und analysiert.
- Schwachstellen identifiziert: ~16 Doppel-Einträge, kaputter `#categories`-Anker im TOC,
  veraltetes Intro (kein Hinweis auf Agent-Skills-Standard), Link-Inkonsistenzen (/tree/ vs /blob/).

## Erledigt (Fortsetzung)
- README-Neufassung: Dubletten zusammengeführt (115 → 99 Skills), TOC repariert,
  Skill-Zahlen pro Kategorie, aktualisiertes Intro.
- Flaggschiff-Sektion „Agentic Engineering Starter-Stack": Teaser-Block oben in der
  README (Pitch, 4-Phasen-Tabelle, Workflow-Baum, Link) + eigene Detaildatei
  `AGENTIC-STACK.md` (voller Guide, Englisch, ohne Star-Zahlen).
- Star-Zahlen gegen die GitHub-API geprüft (Doc war veraltet); im Repo bewusst
  weggelassen, stattdessen „actively maintained, MIT".

## Erledigt (Fortsetzung 2)
- Snyk-ToxicSkills-Zahlen per Web verifiziert (Stand 5.2.2026) und im Stack korrigiert:
  36 % = "mind. ein Sicherheitsproblem" (nicht Prompt Injection), 13,4 % kritisch, 76 Payloads.
- Neue Sektion „🛡️ Skill Safety & Auditing" in der README (Warnung + 3 Scanner + 5 Regeln):
  skill-security-auditor (alirezarezvani/claude-skills, MIT, aktiv), Cisco Skill Scanner
  (cisco-ai-defense/skill-scanner, open source), Snyk Agent Scan. Alle GitHub-Repos verifiziert.
- Vorschau-Artefakt des Stacks gebaut und veröffentlicht (Engineering-Runbook-Optik,
  Light/Dark): https://claude.ai/code/artifact/c35d981a-1cee-4901-8000-2ec5b5d16b02
- Deutsche Fassung verworfen (Entscheidung des Autors).

## Erledigt (Fortsetzung 3 – kompletter Link-Audit)
- ALLE Katalog-Links gegen die GitHub-API (authentifiziert via gh) geprüft. Ergebnis:
  die grossen Repos hatten Okt 2025–Jul 2026 umstrukturiert. Reparaturen:
  - anthropics/skills: 13 Skills → jetzt unter `skills/…` umgebogen.
  - K-Dense: Repo umbenannt (`scientific-agent-skills`) + Doku `docs/skills.md`.
  - zxkane/aws-skills: 4 Einträge → jetzt unter `plugins/…` (aws-iac, aws-cost-ops, serverless-eda).
  - obra/superpowers: 5 Skills sind jetzt Unterdateien (.md) → Pfade angepasst.
  - michalparkola: Repo umbenannt → `tapestry-skills`.
  - 5 komplett verschwundene Skills entfernt (artifacts-builder, template-skill,
    commands, sharing-skills, tapestry). Katalog: 99 → 94 Skills.
  - 10 archivierte (obra/superpowers-skills) mit ⚠️(archived) markiert.
  - 6 länger inaktive mit (updated 2025) markiert.
- Finale Prüfung: kein toter GitHub-Link mehr. Badges/Zähler/Datum aktualisiert.

## Offen (als Nächstes)
- FINAL: Review durch den Autor → dann committen & pushen (wartet auf Okay).
- Push erfolgt über gh-Konto „tonightlife" – prüfen, ob das Schreibrechte auf
  obviousworks/… hat (sonst Fork+PR oder anderes Konto nötig).

## Noch anzuschauen (offene Fragen)
- Externe Stats im Stack (Caveman-Benchmark 65 %, arXiv-Paper) noch NICHT unabhängig
  geprüft — sauber verlinkt, aber Autoren-Recherche. Bei Bedarf prüfen.
- Archivierte Problemlösungs-Skills: kein aktives neues Zuhause gefunden → vorerst
  markiert behalten. Später ersetzen?
