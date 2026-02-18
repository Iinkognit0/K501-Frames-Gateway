# Mapping YAML ↔ SQL  

## Trigger-System iInkognit0

  

Status: ✔ kanonisch · ✔ abgeschlossen · ✔ auf Ewigkeit gültig

  

---

  

## Zweck dieses Dokuments

  

Dieses Dokument beschreibt die **eindeutige Zuordnung (Mapping)**  

zwischen der **YAML-Referenz** des Trigger-Systems  

und dem **SQL-Schema** desselben Systems.

  

Ziel:

- Konsistenz

- Prüfbarkeit

- Automatisierbarkeit

- Architekturtreue zum „ewigen Archiv“

  

Die YAML-Datei ist **deklarativ**.  

Das SQL-Schema ist **strukturell-persistierend**.

  

Beide beschreiben **dieselbe Wahrheit** auf unterschiedlichen Ebenen.

  

---

  

## 1. Grundlogik des Mappings

  

| Ebene | Funktion | Rolle |

|-----|---------|------|

| YAML | semantische Definition | Mensch & Stimme |

| SQL  | technische Persistenz | System & Validierung |

  

YAML **definiert**,  

SQL **speichert**.

  

YAML ist Quelle der Bedeutung.  

SQL ist Träger der Ordnung.

  

---

  

## 2. Zentrale Entitäten

  

### YAML

```yaml

trigger:

  id: projektanalyse

  name: Vollständige Projektanalyse

  prioritaet: 1

  traeger_pruefung: true

  outputs:

    - analyse_output_1

    - analyse_output_2

    - analyse_output_3

  

SQL

  

INSERT INTO trigger (

  trigger_id,

  name,

  priority,

  requires_carrier_check

) VALUES (

  'projektanalyse',

  'Vollständige Projektanalyse',

  1,

  TRUE

);

  

  

  

  

3. Feld-Mapping (Detail)

  

|   |   |   |
|---|---|---|
|YAML-Feld|SQL-Spalte|Bedeutung|
|trigger.id|trigger.trigger_id|eindeutiger Schlüssel|
|trigger.name|trigger.name|Klarname|
|trigger.prioritaet|trigger.priority|Ausführungsrang|
|traeger_pruefung|requires_carrier_check|Pflichtprüfung|
|outputs[]|trigger_outputs.output_id|Output-Referenzen|

  

  

  

  

4. Mapping Outputs

  

  

  

YAML

  

outputs:

  - id: analyse_output_1

    typ: text

    position: 1

  

SQL

  

INSERT INTO trigger_outputs (

  output_id,

  trigger_id,

  output_type,

  output_position

) VALUES (

  'analyse_output_1',

  'projektanalyse',

  'text',

  1

);

  

  

  

  

5. Mapping Prioritäten

  

  

  

YAML

  

prioritaet: 2

  

SQL

  

priority INTEGER NOT NULL

Regel:

Je niedriger die Zahl, desto höher die Priorität.

  

1 = systemisch

2 = strategisch

3 = operativ

4 = erläuternd

  

  

  

  

6. Träger-Prüfung (kritisch)

  

  

  

YAML

  

traeger_pruefung: true

  

SQL

  

requires_carrier_check BOOLEAN DEFAULT TRUE

Bedeutung:

  

- Kein Trigger darf Inhalte erzeugen,  
    bevor alle betroffenen Träger geprüft wurden.
- Die Stimme fungiert als Wächter.

  

  

  

  

  

7. Konsistenz-Regel

  

  

Jede gültige YAML-Definition MUSS:

  

- vollständig in SQL abbildbar sein
- ohne Informationsverlust persistierbar sein

  

  

Jede SQL-Instanz MUSS:

  

- auf eine gültige YAML-Quelle zurückführbar sein

  

  

Kein Drift.

Keine impliziten Felder.

Keine Schattenlogik.

  

  

  

  

8. Rolle der Stimme Iinkognit0

  

  

Die Stimme:

  

- liest YAML
- prüft SQL-Status
- verweigert Trigger bei Inkonsistenz
- meldet Abweichungen

  

  

Die Stimme entscheidet nicht.

Sie bewahrt Ordnung.

  

  

  

  

9. Abschluss

  

  

Dieses Mapping stellt sicher, dass:

  

- Bedeutung (YAML)
- Struktur (SQL)
- Gedächtnis (Vault)

  

  

in kohärenter Einheit existieren.

  

Es ist keine Implementierung.

Es ist eine Architekturreferenz.

  

  

  

As I State iInkognit0.