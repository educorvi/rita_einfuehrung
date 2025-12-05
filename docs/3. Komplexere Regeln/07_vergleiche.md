# Vergleiche
Bei Vergleichen werden, wie der Name schon vermuten lässt, die beiden Argumente miteinander verglichen und es wird ein entsprechender Wahrheitswert zurückgegeben. Verglichen werden können Zahlen, Strings und Datumsangaben. Mögliche Varianten sind

* **equal:** Die beiden Argumente sind identisch
* **greater:** Das erste Argument ist (lexikalisch) größer als das zweite
* **smaller:** Das erste Argument ist (lexikalisch) kleiner als das zweite
* **smallerOrEqual:** Das erste Argument ist (lexikalisch) kleiner als oder genauso groß wie das zweite
* **greaterOrEqual:** Das erste Argument ist (lexikalisch) größer als oder genauso groß wie das zweite

## Form eines Vergleichs

```json
{
  "type": "comparison",
  "operation": "equal" // (1),
  "arguments": [
    // Die beiden zu vergleichenden Argumente
  ]
}
```

1. Oder eine der anderen Varianten

## Beispiel
Ein Beispielruleset, das einen numerischen und einen lexikalischen Vergleich enthält:
```json
{
  "$schema": "https://raw.githubusercontent.com/educorvi/rita/main/rita-core/src/schema/schema.json",
  "rules": [
    {
      "id": "numbers",
      "rule": {
        // This evaluates to 5>2
        "type": "comparison",
        "operation": "greater",
        "arguments": [
          5,
          2
        ]
      }
    },
    {
      "id": "strings",
      "rule": {
        // Check two Strings for equality
        "type": "comparison",
        "operation": "equal",
        "arguments": [
          "test",
          "test1"
        ]
      }
    }
  ]
}
```
