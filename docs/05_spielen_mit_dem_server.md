# Den Server ausprobieren
Zum Ausprobieren des eignet sich die SwaggerUI. Diese findet sich, wie bereits im letzten Kapitel erwähnt, unter [http://localhost:3000/docs](http://localhost:3000/docs). Dort sind auch die Endpunkte dokumentiert. Eine kurze Zusammenfassung:

| Method | URL                   | Description                                                                                      |
|--------|-----------------------|--------------------------------------------------------------------------------------------------|
| GET    | /rulesets             | Gibt eine Liste aller Rulesets zurück                                                            |
| GET    | /rulesets/{rulesetID} | Gibt das Ruleset mit der übergebenen ID zurück                                                   |
| POST   | /rulesets/{rulesetID} | Speichert das gepostete Ruleset mit der übergebenen ID. Überschreibt, falls ID bereits existiert |
| DELETE | /rulesets/{rulesetID} | Löscht das Ruleset mit der übergebenen ID                                                        |
| POST   | /evaluate/{rulesetID} | Evaluiert die Regel, die die gegebene ID besitzt, mit den geposteten Daten aus                   |

## Ruleset speichern
Speichern wir zunächst das vorhin erstellte Ruleset.
```json
{
  "$schema": "https://raw.githubusercontent.com/educorvi/rita/main/rita-core/src/schema/schema.json",
  "rules": [
    {
      "id": "example1",
      "rule": {
        "type": "and",
        "arguments": [
          {
            "type": "atom",
            "path": "hatEinhorn"
          },
          {
            "type": "not",
            "arguments": [
              {
                "type": "atom",
                "path": "mitarbeiter"
              }
            ]
          }
        ]
      }
    }
  ]
}
```
