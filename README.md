#  RSScrawler - Version 1.5.6f
Projekt von https://github.com/rix1337

## Enthaltener Code:
https://github.com/dmitryint (im Auftrag von https://github.com/rix1337)

https://github.com/zapp-brannigan/own-pyload-plugins/blob/master/hooks/MovieblogFeed.py

https://github.com/Gutz-Pilz/pyLoad-stuff/blob/master/SJ.py

https://github.com/bharnett/Infringer/blob/master/LinkRetrieve.py

## Beschreibung:

RSScrawler durchsucht MB/SJ nach in .txt Listen hinterlegten Titeln und reicht diese im .crawljob Format an JDownloader weiter.

Diese Version ist final (bekannte Fehler sind behoben/keine vom Author gewünschten Features fehlen).

Den JDownloader betreffende Probleme (ReCaptcha benötigt Browserfenster, etc.) müssen in dessen Entwicklerforum gelöst werden.

**Um ein Problem zu lösen, oder das Projekt zu erweitern muss ein entsprechender Pull Request (mit Code) eröffnet werden! Issues dienen nur der Fehlermeldung.**

## TLDR:

1. Aktiviere Ordnerüberwachung im JDownloader 2
2. Installiere Python 2.7 und die Zusatzpakete: docopt, feedparser, BeautifulSoup, pycurl, lxml, requests (Alternativ stehen ein docker-image, sowie ein Synology-Paket zur Verfügung)
3. Starte RSScrawler einmalig, dies erstellt die RSScrawler.ini im Einstellungen-Ordner
4. Passe die ```Einstellungen.ini``` und die .txt Listen komplett an.
5. Nutze RSScrawler!

## RSScrawler starten:

```python RSScrawler.py``` führt RSScrawler aus

## Startparameter:

  ```--testlauf```                  Einmalige Ausführung von RSScrawler
  
  ```--jd-pfad=<JDPFAD>```        Legt den Pfad von JDownloader fest (nützlich bei headless-Systemen)

  ```--log-level=<LOGLEVEL>```    Legt fest, wie genau geloggt wird (CRITICAL, ERROR, WARNING, INFO, DEBUG, NOTSET )

## Einstellungen:
*Die RSScrawler.ini liegt im ```Einstellungen``` Ordner und wird (inklusive der Listen) beim ersten Start automatisch generiert*

**Der JDownloader-Pfad muss korrekt hinterlegt werden! Beachte den [Hinweis zu Windows](#wichtiger-hinweis-für-den-windows-build)**

Alle weiteren Einstellungen können nach Belieben angepasst werden und sind hinreichend erklärt. Im Folgenden nur einige wichtige Hinweise:

### Die Listen (MB_Filme, MB_Serien, SJ_Serien, SJ_Serien_Regex:

1. MB_Filme enthält pro Zeile den Titel eines Films (Film Titel), um auf MB nach Filmen zu suchen
2. MB_Staffeln enthält pro Zeile den Titel einer Serie (Serien Titel), um auf MB nach kompletten Staffeln zu suchen
3. SJ_Serien enthält pro Zeile den Titel einer Serie (Serien Titel), um auf SJ nach Serien zu suchen
4. SJ_Serien_Regex enthält pro Zeile den Titel einer Serie in einem speziellen Format, wobei die Filter ignoriert werden:

```
DEUTSCH.*Serien.Titel.*.S01.*.720p.*-GROUP sucht nach Releases der Gruppe GROUP von Staffel 1 der Serien Titel in 720p auf Deutsch

Serien.Titel.* sucht nach allen Releases von Serien Titel (nützlich, wenn man sonst HDTV aussortiert)

Serien.Titel.*.DL.*.720p.* sucht nach zweisprachigen Releases in 720p von Serien Titel

ENGLISCH.*Serien.Titel.*.1080p.* sucht nach englischen Releases in Full-HD von Serien Titel
```

Generell sollten keine Sonderzeichen in den Listen hinterlegt werden!

**Die Listen werden automatisch mit Platzhalterzeilen generiert und sind danach anzupassen. Platzhalter verhindern, dass unerwünschte Releases beim ersten Start hinzugefügt werden.**

### crawl3d:

Wenn aktiviert sucht das Script nach 3D Releases (in 1080p), unabhängig von der oben gesetzten Qualität. Standartmäßig werden HOU-Releases aussortiert (ignore).

### enforcedl:

Wenn aktiviert sucht das Script zu jedem nicht-zweisprachigen Release (kein DL-Tag im Titel) ein passendes Release in 1080p mit DL Tag.
Findet das Script kein Release wird dies im Log vermerkt. Bei der nächsten Ausführung versucht das Script dann erneut ein passendes Release zu finden. Diese Funktion ist nützlich um (durch späteres Remuxen) eine zweisprachige Bibliothek in 720p zu halten.

### crawlseasons:

Komplette Staffeln von Serien landen zuverlässiger auf MB als auf SJ. Diese Option erlaubt die entsprechende Suche.

### regex:

Wenn aktiviert werden die Serien aus der SJ_Serien_Regex.txt gesucht

### Wichtiger Hinweis für den Windows Build:

Der Pfad zum JDownloader muss Python-kompatibel vergeben werden: nur `/`-Schrägstriche sind erlaubt!

### Windows Build:
https://github.com/rix1337/RSScrawler/releases

### Docker Container:
https://github.com/rix1337/docker-rsscrawler

### Synology Addon-Paket:
http://www.synology-forum.de/showthread.html?76211-RSScrawler-(noarch)-Paketzentrum-(JDownloader-Add-on)
