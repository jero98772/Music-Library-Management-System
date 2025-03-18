# Musikbibliotheksverwaltungssystem (Übersetzung nicht überprüft)

Eine Clojure-Webanwendung zur Verwaltung von Musikpartituren mit Redis als Speicher. Bietet RESTful API-Endpunkte und eine einfache Frontend-Oberfläche.

## Beschreibung

**Für Künstler & Musikbewahrer:**  
Stellen Sie sich einen Ort vor, an dem Ihre Noten sofort lebendig werden – ohne Downloads oder umständliche Software. Dies ist ein digitaler Zufluchtsort für Ihre Partituren, geschaffen, um Ihre Werke direkt im Browser erstrahlen zu lassen. Ob Sie eine nächtliche Melodie auf zerknittertem Papier skizzieren, ein vergessenes klassisches Stück wiederbeleben oder mit elektronischen Beats experimentieren – Ihre Kompositionen werden nicht nur gespeichert, sondern erlebt. Verabschieden Sie sich von statischen PDFs und unlesbaren Dateien: Hier werden Partituren auf jedem Gerät perfekt dargestellt, sodass Mitarbeiter Ihre Vision sofort sehen, spielen und fühlen können. Keine verlorenen Manuskripte mehr oder Formatkämpfe – nur Ihre Kunst, die frei online atmet und schneller als je zuvor Herzen erreicht.

**Warum Open Source? Weil Musik allen gehört.**  
Dieses Projekt ist nicht hinter Corporate Walls oder Paywalls versteckt – es wurde von und für Menschen geschaffen, die Musik leben. Open Source bedeutet, dass jede Codezeile ein gemeinsamer Gesang ist, ein kollektiver Einsatz zum Schutz der Kreativität. Wie eine Jam-Session, bei der jeder ein Instrument ergreifen kann, können Entwickler, Musiker und Träumer weltweit dieses Tool anpassen, verbessern und umgestalten. Wollen Sie eine Funktion zur Transkription handgeschriebener Noten? Fügen Sie sie hinzu. Träumen Sie von Tags nach Stimmung oder kulturellen Wurzeln? Bauen Sie es. Transparenz ist hier kein Buzzword – es ist ein Versprechen. Keine versteckten Agenden, nur eine Community, die Technologie und Leidenschaft zu etwas verbindet, das uns alle überdauert. Gemeinsam archivieren wir nicht nur Noten – wir bewahren die Geschichten, Kämpfe und Funken, die Musik zur universellen Sprache der Menschheit machen. Machen Sie mit und verwandeln Sie Bewahrung in einen Akt der Liebe.

## Verfügbare Übersetzungen:

<center>

[Español](https://github.com/jero98772/Music-Library-Management-System/blob/main/docs/readme_es.md)

[English](https://github.com/jero98772/Music-Library-Management-System/blob/main/README.md)

[Русский](https://github.com/jero98772/Music-Library-Management-System/blob/main/docs/readme_ru.md)

</center>

## Funktionen

- **CRUD-Operationen**: Erstellen, Lesen, Aktualisieren, Löschen von Partituren
- **Redis-Speicher**: Dauerhafte Datenspeicherung mit Redis
- **EDN-Serialisierung**: Speicherung komplexer Clojure-Datenstrukturen
- **REST-API**: JSON-basierte API für programmatischen Zugriff
- **Webinterface**: Einfache HTML-Seiten für manuelle Interaktionen

## Technologien

- **Clojure** (1.10+)
- **Ring/Compojure** (Webframework)
- **Carmine** (Redis-Client)
- **Redis** (5.0+)
- **Leiningen** (Build-Tool)

## Voraussetzungen

- Java JDK 8+
- Leiningen 2.9.8+
- Redis Server 5.0+

## Installation

1. Repository klonen:
   ```bash
   git clone https://github.com/yourusername/music-lib.git
   cd music-lib/src
   ```

2. Abhängigkeiten installieren:
   ```bash
   lein deps
   ```

3. Redis-Server starten:
   ```bash
   redis-server
   ```

4. Anwendung ausführen:
   ```bash
   lein ring server
   ```

Die Anwendung ist unter `http://localhost:3000` verfügbar.

## Screenshots

![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/2.png)
![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/3.png)
![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/4.png)
![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/5.png)

## API-Dokumentation

### Alle Partituren abrufen
```
GET /api/partiture
```
**Antwort:**
```json
{
  "count": 2,
  "partitureList": [
    {
      "id": "partiture:uuid1",
      "title": "Mondscheinsonate",
      "composer": "Beethoven",
      "created-at": "2023-09-20"
    }
  ]
}
```

### Neue Partitur erstellen
```
POST /api/partiture
```
**Parameter:**
- `title` (erforderlich)
- `composer` (erforderlich)
- `opus` (optional)
- `key` (optional)

**Beispielantwort:**
```json
{
  "id": "partiture:550e8400-e29b-41d4-a716-446655440000"
}
```

### Einzelne Partitur abrufen
```
GET /api/partiture/:id
```
**Antwort:**
```json
{
  "id": "partiture:uuid1",
  "title": "Claro de Luna",
  "composer": "Beethoven",
  "instrumenr": "piano",
  "abc": "
X:3
T:Simple Song
M:4/4
L:1/8
K:C
[C]C2 [F]F2 [G]G2 [C]C2 |
w: This is a sim-ple song, sing a-long with me.

  ",
}
```

### Partitur aktualisieren
```
PUT /api/partiture/:id
```
**Parameter:** Wie POST

### Partitur löschen
```
DELETE /api/partiture/:id
```

## Frontend-Routen

- `/` – Hauptübersicht
- `/add-partiture` – Formular zum Hinzufügen
- `/partiture/:id` – Partitur-Detailansicht
- `/edit/:id` – Bearbeitungsformular
- `/delete/:id` – Löschbestätigung

## Projektstruktur

```
├── src
│   └── music_lib
│       ├── core.clj    # Hauptanwendungsrouten
│       └── db.clj      # Redis-Datenbankoperationen
├── resources
│   └── public          # Statische Assets
│       ├── index.html
│       ├── add-partiture.html
│       └── ...weitere HTML-Dateien
├── project.clj         # Leiningen-Konfiguration
└── README.md
```

## Konfiguration

Redis-Verbindungseinstellungen (in `db.clj`):
```clojure
(def server-conn {
  :spec {
    :host "127.0.0.1"
    :port 6379
    :password nil
    :timeout-ms 3000}})
```

## API-Tests

Beispiele mit curl:
```bash
# Partitur erstellen
curl -X POST -d "title=Für Elise&composer=Beethoven" http://localhost:3000/api/partiture

# Alle Partituren abrufen
curl http://localhost:3000/api/partiture

# Partitur aktualisieren
curl -X PUT -d "opus=WoO59" http://localhost:3000/api/partiture/partiture:uuid1
```

## Fehlerbehandlung

Die API gibt HTTP-Statuscodes zurück:
- 200 OK
- 201 Created
- 404 Not Found
- 500 Internal Server Error

Fehler enthalten JSON mit Details:
```json
{
  "error": "Partitur nicht gefunden"
}
```

## Mögliche Verbesserungen

1. Authentifizierung hinzufügen
2. Datenvalidierung implementieren
3. Suchfunktion einbauen
4. Paginierung für große Datensätze
5. Übersichtliche Fehlermeldungen im Frontend
6. Testabdeckung erhöhen
7. Docker-Integration
8. Swagger/OpenAPI-Dokumentation

## Problembehebung

Häufige Probleme:
1. **Redis-Verbindungsfehler**
   - Stellen Sie sicher, dass der Redis-Server läuft
   - Überprüfen Sie die Verbindungseinstellungen in `db.clj`

2. **EDN-Parsingfehler**
   - Überprüfen Sie Daten mit `redis-cli`
   - Stellen Sie sicher, dass gespeicherte Werte gültiges EDN sind

3. **Fehlende Abhängigkeiten**
   - Führen Sie `lein deps` aus

## Lizenz

GPLv3-Lizenz. Sie dürfen dieses Projekt für jeden Zweck nutzen, müssen jedoch einen Verweis auf [https://github.com/jero98772/Music-Library-Management-System](https://github.com/jero98772/Music-Library-Management-System) setzen.

## Danksagung

Erstellt mit:
- [Compojure](https://github.com/weavejester/compojure)
- [Carmine](https://github.com/ptaoussanis/carmine)
- [Ring](https://github.com/ring-clojure/ring)