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
            "path": "hatComputer"
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

## Ruleset speichern
Um ein Ruleset zu speichern, müssen wir es gegen den Endpunkt `/rulesets/{id}` posten. Die ID ist hierbei frei wählbar, sollte aber unbelegt sein, da ein etwaiges anderes Ruleset mit derselben ID dann überschreiben würden.
=== "Swagger UI"
    Wir können zum Testen der Endpunkte die Swagger UI verwenden. Einmal geöffnet klicken wir den gewünschten Endpunkt (`POST /rulesets/{rulesetID}`) an. In dem sich öffnenden Bereich wählen wir nun "Try it out". Anschließend muss im Feld `rulesetID` die oben beschriebene ID eingegeben werden, in den Request Body wird das Ruleset selbst kopiert. Dann nur noch auf "Execute" klicken. Als Antwort sollte der Server den Statuscode 201 liefern.

=== "Curl"
    Zunächst speichern wir das Ruleset in eine Datei, z.B. `ruleset.json`. Anschließend kann das Ruleset gepostet werden. Als frei wählbare ID nimmt dieses Beispiel den Wert 0.
    ```bash
    curl -X POST -H "Content-Type: application/json" -d @ruleset.json http://localhost:3000/rulesets/0
    ```

## Rulesets ansehen
Nun können wir überprüfen, ob unser Ruleset wirklich gespeichert wurde.
=== "Swagger UI"
    Den Endpunkt (`GET /rulesets`) auswählen, dann "Try it out", dann "Execute". 

=== "Curl"
    ```bash
    curl http://localhost:3000/rulesets
    ```
Im Ergebnis sollten alle bis jetzt erstellten Rulesets enthalten sein.

Probiere auch gerne auf dieselbe Art und Weise die anderen Endpunkte aus. Ihre Funktion ist in der Swagger UI dokumentiert.

## Evaluieren
Jetzt, wo wir ein Ruleset auf dem Server erstellt haben, können wir endlich das machen, wofür Rita eigentlich gedacht ist: Daten auf diesen Regeln auswerten. Dafür müssen wir die Daten an den Endpunkt `/evaluate/{id}` posten, wobei die Daten im Body übergeben werden und die id in der URL der ID der Regel (in unserem Fall 0) entspricht, die wir auswerten wollen.
Die Daten sind frei wählbar, hier ein Beispiel, das zu wahr auswertet:

```json
{
  "hatComputer": true,
  "mitarbeiter": false
}
```
=== "Swagger UI"
    Den Endpunkt (`GET /rulesets`) auswählen, dann "Try it out", dann bei rulesetID die ID (in unserem Fall 0) und beim Request body die Daten eingeben und "Execute" drücken. 

=== "Curl"
    ```bash
    curl -X POST -H "Content-Type: application/json" -d "{\"hatComputer\": true,\"mitarbeiter\": false}" http://localhost:3000/evaluate/0
    ```

Dabei sollte folgendes Ergebnis zurückkommen:
```json
{
  "result": true, // (1)
  "details": [ // (2)
    {
      "id": "example1",
      "result": true
    }
  ],
  "counts": { // (3)
    "true": 1,
    "false": 0
  }
}
```

1. Ist das Gesamtergebnis des Rulesets. Nur dann `true`, wenn auch alle Regeln in diesem Ruleset `true` sind.
2. Gibt für jede Regel das individuelle Ergebnis an.
3. Anzahl der erfüllten und Anzahl der unerfüllten Regeln.

## API Keys
Bereits im letzten Kapitel wurde gezeigt, wie API Keys erstellt, verändert und gelöscht werden können. Der API Key kann dann anschließend in der Swagger UI verwendet werden, indem man auf Authorize drückt und ihn dort eingibt. Ab dann werden Requests mit diesem API Key gestellt. Bei Curl muss der Header `X-API-KEY` mit dem API Key als Wert gesetzt werden.
