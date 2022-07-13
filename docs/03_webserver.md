# Der Webserver
Der Webserver läuft nun unter dem Port 3000 (oder einem anderen Port, falls entsprechend geändert).
Ruft man nun den Server auf ([http://localhost:3000](http://localhost:3000)), erhält man ein JSON Objekt mit Informationen über selbigen:
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
Enthalten sind unter anderem die Versionsnummern des Servers, die installierte Rita-Version, sowie alle Plugins und deren Versionen.

## Swagger UI
Unter [http://localhost:3000/docs](http://localhost:3000/docs) befindet sich eine Dokumentation der aufrufbaren URLs. Außerdem bietet die Swagger UI eine Oberfläche, um diese Endpunkte auszuprobieren.
