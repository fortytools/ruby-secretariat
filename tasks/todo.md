# Schema-Update ZUGFeRD 2.5.2 / Factur-X 1.09.2 + Mustang 2.25.0

Plan: ~/.claude/plans/zugferd-2-5-2-released-hier-kind-dream.md

- [x] 1. Schemadateien in `schemas/zugferd_2/` austauschen (6 Dateien aus FeRD-Paket, unverändert)
- [x] 2. `lib/secretariat/validator.rb`: `SCHEMA_VERSION = "1.09.2"`, fester Schematron-Pfad `FACTUR-X_EN16931.sch`
- [x] 3. Neue Spec: `document()`-Referenzen im `.sch` → Dateien existieren; XSLT-2-Einschränkung dokumentiert
- [x] 4. Mustang-CLI 2.24.0 → 2.25.0 (JAR getauscht, `JAR_PATH`, README, CLAUDE.md)
- [x] 5. Doku & Version: version.rb 2.2.0, CHANGELOG, README, CLAUDE.md
- [x] 6. Verifikation: rspec, standardrb, XSD-Smoke-Test v3, Mustang-validate (v3 + XRechnung), Diff-Kontrolle gegen FeRD-Paket

## Review

- Alle 6 Schemadateien byte-identisch mit dem FeRD-Release-Paket übernommen (`cmp`-geprüft); `.sch`/codedb unter den neuen unversionierten FeRD-Originalnamen.
- validator.rb: nur `SCHEMA_VERSION` (jetzt "1.09.2", steuert XSDs) und der Schematron-Pfad geändert.
- Neue Specs sichern die `document()`-codedb-Verknüpfung statisch ab (voller Schematron-Lauf scheitert weiterhin an XSLT 2 — Spec dokumentiert die Einschränkung explizit).
- Mustang 2.25.0 (ZUGFeRD-2.5.2-Regeln, VeraPDF-CVE-Fixes); Download-Größe gegen GitHub-Release-Asset geprüft.
- Tests: 27 Beispiele, 0 Fehler, 3 bekannte Pendings (XSLT 2); standardrb sauber.
- Mustang-End-to-End: generiertes ZUGFeRD-v3-XML valide (90 Regeln, 0 Fehler), XRechnung-v3-XML valide (2 Warnungen: CII-SR-313 URIUniversalCommunication in ShipToTradeParty, BR-DE-21-Hinweis zur Spezifikations-Kennung — beides Generator-Verhalten, unabhängig vom Schema-Update, war mit 2.24.0-Regelwerk nicht gemeldet worden → ggf. separat anschauen).
- Follow-ups (bewusst außen vor): XSLT-2-Stylesheet aus dem FeRD-Paket zur Behebung der Schematron-Pendings; Upstream-PR an halfbyte; FeRD-Errata bis 1.9.2026 beobachten.
