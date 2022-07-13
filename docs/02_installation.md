# Installation
Bevor wir nun praktisch versuchen erste Regeln zu schreiben und auszuwerten, müssen wir zunächst Rita aufsetzen. Dafür werden wir den bereits erwähnten Server installieren, der einer REST Api für Rita bereitstellt.

Dies kann entweder mit Docker oder mit einer manuellen Installation geschehen. Nach der Installation wird der Server unter der Adresse http://localohost:3000 aufrufbar sein.
## Docker
### Benötigte Software
- [Docker](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Setup
Erstellen Sie zunächst die Datei `docker-compose.yaml` mit folgendem Inhalt:
```yaml

version: '3'

services:
    mysql:
        image: mysql:8
        container_name: mysql
        environment:
            MYSQL_RANDOM_ROOT_PASSWORD: 1
            MYSQL_DATABASE: rita
            MYSQL_USER: rita
            MYSQL_PASSWORD: ${MYSQL_PASSWORD}

    rita-http:
        depends_on:
            - mysql
        image: ghcr.io/educorvi/rita-http:3-latest
        container_name: rita-http
        environment:
            WAIT_HOSTS: mysql:3306
            PORT: 3000
            LOGLEVEL: info
            DB_TYPE: MYSQL
            DB_HOST: mysql
            DB_PORT: 3306
            DB_USERNAME: rita
            DB_PASSWORD: ${MYSQL_PASSWORD}
            DB_DATABASE: rita
        ports:
            - '3000:3000'
```
Nun kann der Server ausgeführt werden, indem im selben Ordner, in dem auch die oben erwähnte Datei liegt, folgender Befehl ausgeführt wird:
```bash
MYSQL_PASSWORD=SOME_RANDOM_PASSWORD docker compose up
```

## Manuelle Installation
### Benötigte Software
- [Node.js](https://nodejs.org/)
- Rush.js (Install by running `npm install -g @microsoft/rush`)

### Source
Zunächst muss das Repository geklont werden:
```bash
git clone -b main https://github.com/educorvi/rita.git
cd rita
```

### Bauen und Starten der Software
```bash
# Installieren der Abhängigkeiten
rush install

# Bauen
rush build

# Wechsel in das rita-http Verzeichnis
cd rita-http

# Konfigurieren der .env Datei
cp .env.template .env

# In der .env Datei LOGLEVEL auf "info" und DB_TYPE auf "SQLITE" setzen 
# und bei Bedarf andere Einstellungen vornehmen

# HTTP Server starten
node .
```