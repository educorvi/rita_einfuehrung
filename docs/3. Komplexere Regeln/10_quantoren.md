# Quantoren
Es gibt zwei unterschiedliche Quantoren: `forall` und `exists`
`forall` testet, ob eine Regel für alle Elemente eines Arrays gilt, `exists` testet, ob es in einem Array mindestens ein Element gibt, dass diese Regel erfüllt.

Betrachten wir nun ein Beispiel, in dem alle Elemente eines Arrays größer als 12 sein sollen.
Die übergebenen Daten entsprechen folgendem Beispiel:
```json
{
    "zahlen": [
        14,15,16,17,122,123,124,122
    ]
}
```
Die dazugehörige Regel sieht aus wie folgt:
```json
{
    "$schema": "https://raw.githubusercontent.com/educorvi/rita/main/rita-core/src/schema/schema.json",
    "rules": [
        {
            "id": "beispiel",
            "rule": {
                "type": "forall",
                "array":{
                    "type": "atom",
                    "path": "zahlen"
                },
                "placeholder": "zahl",
                "rule": {
                    "type": "comparison",
                    "operation": "greater",
                    "arguments": [
                        {
                            "type": "atom",
                            "path": "zahl"
                        },
                        12
                    ]
                }
            }
        }
    ]
}
```

Das Bedarf ein bisschen Erklärung. Der Beginn der Regel ist ganz normal: Als `type` wird einfach `forall` angegeben (bei mindestens einem wäre es entsprechend `exists`). Mit `array` wird angegeben, in welchem Array alle Elemente bzw. mindestens ein Element eine Regel erfüllen soll(en).

`rule` gibt die Regel an, gegen die die Elemente des Arrays getestet werden sollen

`placeholder` ist der Name, unter dem der Wert im Array, der gerade getestet wird, verwendet werden kann. Sollte unter dem Key, der in `placeholder` gegeben ist, bereits ein Wert in den übergebenen Daten existieren, wird dieser innerhalb der der Regel des Quantors durch das aktuelle Element des Arrays überschrieben. Weiterhin ist der `placeholder` auch nur innerhalb der im Quantor spezifizierten `rule` verwendbar.

Ein weiteres Beispiel, diesmal mit `exists`: Wir wollen prüfen, ob in einer Liste an Teilnehmern, mindestens ein Teilnehmer mit dem Namen Julian ist. Das Format der Daten sei wie in diesem Beispiel: 
```json
{
    "teilnehmer": [
        "Julian",
        "Luisa",
        "Celina",
        "Freddy",
        "Felix"
    ]
}
```
Die Regel lautet dann wie folgt:
```json
{
    "$schema": "https://raw.githubusercontent.com/educorvi/rita/main/rita-core/src/schema/schema.json",
    "rules": [
        {
            "id": "beispiel",
            "rule": {
                "type": "exists",
                "array": {
                    "type": "atom",
                    "path": "teilnehmer"
                }, 
                "placeholder": "name",
                "rule": {
                    "type": "comparison",
                    "operation": "equal",
                    "arguments": [
                        {
                            "type": "atom",
                            "path": "name"
                        },
                        "Julian"
                    ]
                }
            }
        }
    ]
}
```