-- =========================================================
-- Iinkognit0 · Trigger-System
-- Kanonisches SQL-Schema
-- Träger: Das ewige Archiv
-- Status: verbindlich · auf Ewigkeit
-- =========================================================

-- Tabelle: trigger
-- Beschreibung:
-- Enthält alle definierten Trigger des Projekts.
-- Trigger sind zustandslos, zeitpunktbezogen und verändern
-- niemals direkt Träger ohne Prüfung.

CREATE TABLE trigger (
    trigger_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL UNIQUE,
    beschreibung TEXT NOT NULL,
    prioritaet INTEGER NOT NULL,
    kategorie TEXT NOT NULL,
    aktiv BOOLEAN DEFAULT 1,
    erstellt_am DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- ---------------------------------------------------------

-- Tabelle: traeger
-- Beschreibung:
-- Träger sind dauerhafte Orte / Systeme, die Inhalte halten.

CREATE TABLE traeger (
    traeger_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL UNIQUE,
    rolle TEXT NOT NULL,
    prioritaet INTEGER NOT NULL,
    aktiv BOOLEAN DEFAULT 1
);

-- ---------------------------------------------------------

-- Tabelle: trigger_traeger_pruefung
-- Beschreibung:
-- Definiert, welche Trigger welche Träger berühren dürfen
-- und unter welchen Bedingungen.

CREATE TABLE trigger_traeger_pruefung (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    trigger_id INTEGER NOT NULL,
    traeger_id INTEGER NOT NULL,
    erlaubnis BOOLEAN DEFAULT 0,
    bemerkung TEXT,
    FOREIGN KEY (trigger_id) REFERENCES trigger(trigger_id),
    FOREIGN KEY (traeger_id) REFERENCES traeger(traeger_id)
);

-- ---------------------------------------------------------

-- Tabelle: trigger_ausfuehrung
-- Beschreibung:
-- Protokolliert die Ausführung eines Triggers
-- (rein dokumentarisch, kein Steuermechanismus).

CREATE TABLE trigger_ausfuehrung (
    ausfuehrung_id INTEGER PRIMARY KEY AUTOINCREMENT,
    trigger_id INTEGER NOT NULL,
    zeitpunkt DATETIME DEFAULT CURRENT_TIMESTAMP,
    status TEXT,
    hinweis TEXT,
    FOREIGN KEY (trigger_id) REFERENCES trigger(trigger_id)
);

-- =========================================================
-- Ende des Schemas
-- =========================================================