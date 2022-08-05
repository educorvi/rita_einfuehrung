# Plugins
Rita unterstützt auch Plugins. Diese sind nicht Teil der Standardfunktionalität und müssen hinzugefügt werden. Aktuell sind im Rita HTTP Server, alle verfügbaren Plugins installiert, wenn man den Server aufruft steht in der Willkommensnachricht auch eine Liste aller installierten Plugins, z.B.:
```json
{
  "version": "3.1.2",
  "message": "Welcome to the RITA API. A documentation is available under ./docs.",
  "ritaVersion": "4.0.0",
  "plugins": [
    {
      "name": "http",
      "version": "1.1.0"
    }
  ]
}
```
Eine Liste der verfügbaren Plugins findet sich unter [https://github.com/educorvi/rita/tree/develop/plugins/](https://github.com/educorvi/rita/tree/develop/plugins/). Nutzer können auch eigene Plugins entwickeln, ds Konzept hinter Plugins ist simpel: Sie bekommen über die Regel eine Liste von Optionen, sowie die aktuellen Daten, können mit diesen dann beliebige Aktionen ausführen und das Ergebnis dieser Aktionen nutzen, um die Daten für die im Pluginblock angegebene Regel anzureichern. Die Optionen können sind vom Plugin beliebig festlegbar. Im Folgenden wird das am Beispiel des [HTTP Plugins](https://github.com/educorvi/rita/tree/develop/plugins/http), das während der Auswertung einer Regel einen HTTP-Request ausführt, demonstriert.

Angenommen wir wollen bei der Auswertung der Daten die Daten an die URL `https://example.com/api1` posten, und die Antwort, die vom Server im JSON-Format gesendet wird, in unseren Datensatz einspeisen.

Angenommen, die API liefert folgende Antwort: 
```json
{
    "message": "super",
    "number": 27
}
```

Wir können nun in der Regel, die innerhalb des Plugins definiert ist, diese beiden Werte verwenden, auch wenn sie nicht von Anfang an in den übergebenen Daten waren:
```json
{
    "$schema": "https://raw.githubusercontent.com/educorvi/rita/main/rita-core/src/schema/schema.json",
    "rules": [
        {
            "id": "beispiel",
            "rule": {
                "type": "and",
                "arguments": [
                    {
                        "type": "atom",
                        "path": "irgendwasDasSchonInDenDatenIst"
                    },
                    {
                        "type": "plugin",
                        "name": "http",
                        "options": {
                            "url": "https://example.com/api1",
                            "method": "POST"
                        },
                        "formula" : {
                            "comment": "Hier können wir jetzt message und number verwenden",
                            "type": "comparison",
                            "operation": "equal",
                            "arguments": [
                                {
                                    "type": "atom",
                                    "path": "number"
                                },
                                27
                            ]
                        }
                    }
                ]
            }
        }
    ]
}
```