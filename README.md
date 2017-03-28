check_fuel_prices_tschechien
============================

Was macht das Plugin
--------------------

Der ARCD Auto- und Reiseclub Deutschland e. V. stellt [online die durchschnittlichen Spritpreise](ARCD Auto- und Reiseclub Deutschland e. V.) für Europäische Länder zur Verfügung. Das Plugin ruft diese Seite ab und analysiert den Inhalt. Aktuell extrahiert es nur die Preise für Tschechien, da nur diese für mich interessant sind.

Mit ein bisschen Aufwand kann ganz leicht ein anderes Land in der Tabelle ausgewählt werden.

Aktuell werden die Preise für Super, Super Plus und Diesel extrahiert. Ich kenne keinen, der noch Normalbenzin tankt.

Installation
------------

* Das Plugin auschecken
* Das Script am besten ins das Verzeichnis linken, in dem Icinga 2 es erwartet
* CheckCommand in Icinga 2 integrieren
* Service anlegen und Icinga 2 neu starten

CheckCommand für Icinga 2
-------------------------

Da das Script keine Argumente hat ist das CheckCommand sehr einfach:

```
object CheckCommand "fuel_prices_tschechien" {
   import "plugin-check-command"

   command = [ PluginDir + "/check_fuel_prices_tschechien" ]
}
```

Beim Service bitte aufpassen: Die Seite wird nicht oft aktualisiert. Ein Check Intervall von 5 Minuten ist also kontraproduktiv und belastet nur unnötig den Webserver des ARCD.

Ich würde sagen zwei mal täglich reicht vollkommen aus, damit man ein paar Punkte erhält. Gefühlt wird die Seite ein mal in der Woche aktualisiert.

Performance Daten & Warn- und Crit-Werte
----------------------------------------

Bei diesem Plugin handelt es sich nicht wirklich um ein Überwachungsplugin, sondern eher um die Performance Daten zu speichern und sie später in einem schönen Graphen auszugeben.

Das Plugin gibt die Preise in € als Performacen Daten aus.
