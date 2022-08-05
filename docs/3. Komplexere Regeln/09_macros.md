# Macros
Es gibt zwei Arten von Macros: Das `now` Macro und das `length` Macro
## now
Dieses Macro gibt zum Zeitpunkt der Evaluation die aktuelle DateTime, also Datum und Uhrzeit zurück. Es kann zum Beispiel für Berechnungen mit Datumsangaben oder Vergleiche verwendet werden. Ein Beispiel dafür wäre eine Regel, die besagt, dass ein angegebenes Datum in der Zukunft liegen muss:
```json
{
    "$schema": "https://raw.githubusercontent.com/educorvi/rita/main/rita-core/src/schema/schema.json",
    "rules": [
        {
            "id": "beispiel",
            "rule": {
                "type": "comparison",
                "operation": "greater",
                "arguments": [
                    {
                        "type": "atom",
                        "path": "datumDasInDerZukunftSeinMuss"
                    },
                    {
                        "type": "macro",
                        "macro": {
                            "type": "now"
                        }
                    }
                ]
            }
        }
    ]
}
```

## length
Dieses Macro gibt die Länge eines Arrays als Zahl zurück. Nehmen wir an, wir bekommen bei der Evaluation eine Liste der Mitarbeiter übergeben:
```json
{
    "mitarbeiter": [
        "ma1",
        "ma2",
        "ma3",
        "ma4",
        "ma5",
    ]
}
```
Unsere Regel soll nun überprüfen, dass die Firma mehr als drei Mitarbeiter hat:
```json
{
    "$schema": "https://raw.githubusercontent.com/educorvi/rita/main/rita-core/src/schema/schema.json",
    "rules": [
        {
            "id": "beispiel",
            "rule": {
                "type": "comparison",
                "operation": "greater",
                "arguments": [
                    {
                        "type": "macro",
                        "macro": {
                            "type": "length",
                            "array": {
                                "type": "atom",
                                "path": "mitarbeiter"
                            }
                        }
                    },
                    3
                ]
            }
        }
    ]
}
```