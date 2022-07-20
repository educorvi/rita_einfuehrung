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

## Konfigurieren des Zugriffs
Für die Zwecke dieses Tutorials ist es sinnvoll, dem anonymen Nutzer alle Rechte einzuräumen, damit kein API Key eingegeben werden muss. 
!!! warning
    Für einen produktiven oder öffentlichen Einsatz ist das offensichtlich NICHT empfehlenswert.

=== "Docker"
    ```bash
    docker exec -it rita-http /bin/sh
    ```
=== "Manuelle Installation"
    In das Arbeitsverzeichnis zu wechseln.

Anschließend `node . --config` ausführen, um den Konfigurationsassistenten zu starten. Dann "API Key Management" auswählen, dann "Edit" und dann "Public Access (*)". Den Namen unverändert lassen und einfach "enter" drücken, dann alle Berechtigungen gewähren, indem man entweder "y" oder "enter" drückt. Anschließend kann der Konfigurator wieder geschlossen werden.

In diesem Konfigurator können auch eigene API Keys erstellt/verwaltet/gelöscht werden.
