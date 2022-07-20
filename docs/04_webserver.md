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
Für die Zwecke dieses Tutorials ist es sinnvoll, dem anonymen Nutzer alle Rechte einzuräumen, damit kein API Key eingegeben werden muss. Für einen produktiven oder öffentlichen Einsatz ist das offensichtlich NICHT empfehlenswert.

Falls der Server mit Docker gestartet wurde, muss zunächst ein Terminal im Container geöffnet werden:
```bash
docker exec -it rita-http /bin/sh
```
Wenn das Projekt lokal läuft, reicht es, in das Arbeitsverzeichnis zu wechseln.

In beiden Fällen anschließend `node . --config` ausführen, um den Konfigurationsassistenten zu starten. Dann "API Key Management" auswählen, dann "Edit" und dann "Public Access (*)". Den Namen unverändert lassen und einfach "enter" drücken, dann alle Berechtigungen gewähren, indem man entweder "y" oder "enter" drückt. Anschließend kann der Konfigurator wieder geschlossen werden.

In diesem Konfigurator können auch eigene API Keys erstellt/verwaltet/gelöscht werden.
