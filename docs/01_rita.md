# Was ist Rita?
## Das Problem
Das Ausgangsproblem ist, eine große Menge von Daten (z. B. Formulare) gegen festgelegte Regeln auszuwerten. In diesem Kontext stellt sich zunächst die Frage, wie man diese Regeln formulieren kann, um sie sowohl für den Nutzer als auch den Computer verständlich zu machen.

## Die Lösung
Hier kommt nun Rita ("**R**ule **it** **a**ll") ins Spiel. Das Projekt besteht aus mehreren Teilen:

- Die Sprache, in der die Regeln formuliert werden
- Ein Parser, der die in der Sprache geschriebenen Regeln parst und so für den Computer verwertbar macht
- Weitere Projekte, die auf diesen Bausteinen aufbauen, so zum Beispiel ein Webserver, der eine REST Api zur Verfügung stellt um Rita Regeln zu verwalten und mit Daten auszuwerten
