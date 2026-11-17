# Gamehearth-Katalog

Der Katalog der Spiele für [Gamehearth](https://github.com/weilers-git/gamehearth), eine selbst hostbare Spieleplattform. Das Repo enthält nur den Index `catalog.json`: pro Spiel Name, Beschreibung, Link zum Quelltext und pro Version Spielerzahl, Rollen, Lizenz, Größe, Download-Adresse und SHA-256-Prüfsumme. Der Spielcode liegt im Repo des jeweiligen Spiels, die Pakete hängen an dessen Releases.

## Auf einem Server nutzen

In der Verwaltung des Gamehearth-Servers unter „Kataloge“ die Adresse eintragen (oder den Vorschlag „Gamehearth-Katalog hinzufügen“ nehmen):

```
https://raw.githubusercontent.com/weilers-git/gamehearth-catalog/main/catalog.json
```

Wer einen Katalog hinzufügt, vertraut ihm: Spiele daraus laufen auf dem Server und in den Browsern der Mitspieler. Der Server prüft jedes Paket gegen die Prüfsumme im Katalog, entpackt es streng, lädt es in seine Sandbox und spielt eine Probepartie, bevor er es installiert. Er lädt den Katalog einmal am Tag neu und zeigt neue Versionen in der Verwaltung an; installiert wird erst auf Klick.

## Spiele

| Spiel | Repo |
|---|---|
| Mau-Mau | [weilers-git/gamehearth-mau-mau](https://github.com/weilers-git/gamehearth-mau-mau) |

## Eine Version eintragen

Voraussetzung ist Node 22. Das Paket muss schon als Release-Anhang im Repo des Spiels liegen (die CI dort baut es mit `gamehearth pack`).

```bash
npm install
npm run add -- https://github.com/weilers-git/gamehearth-mau-mau/releases/download/v0.1.0/mau-mau-0.1.0.zip
npm run check
```

`npm run add` lädt das Paket, prüft es wie der Server und trägt Version, Größe und Prüfsumme ein; Name, Beschreibung und Repo-Link kommen aus dem Manifest der neuesten Version. Eine schon eingetragene Version mit anderer Prüfsumme wird nur mit `--replace` überschrieben, besser ist eine neue Versionsnummer. `npm run check` prüft die Form der Datei und lädt jedes eingetragene Paket einmal (das macht auch die CI bei jedem Push und einmal pro Woche).

Ältere Versionen bleiben stehen, damit ein Server ein kaputtes Update zurücknehmen kann.

## Lizenz

Der Index steht unter CC0 (siehe [LICENSE](LICENSE)). Jedes Spiel hat seine eigene Lizenz; sie steht im Katalog und im Manifest des Spiels.
