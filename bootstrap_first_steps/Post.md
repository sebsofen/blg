Bootstrap bringt ja bekanntlich responsive webdesign für alle.
Entwickeln in Bootstrap geht so:

Erstmal Abhängigkeiten installieren:
============

NodeJs installieren:

```
curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
sudo apt-get install nodejs
```

Grunt installieren

```
sudo npm install -g grunt-cli
```

Im Bootstrap root ordner, installiere:

```
npm install
```

Danach kann mit ``` grunt dist ``` alles installiert werden.
Und mit ``` grunt watch ``` kann man auf Änderungen der less files horchen und ggf neu kompilieren.

Der Bootstrap download kommt mit beispiel themes, die in
```
/docs/examples
```

zu finden sind.


Arbeiten mit Bootstrap
==============

Erstmal sollte man css in less schreiben [foot:http://www.helloerik.com/bootstrap-3-less-workflow-tutorial]

So und nu, Änderungen am Bootstrap template erstellen mit eigenem less "repository".
neuen ordner im bootstrap root erzeugen ```custom-less``` mit eigenem ```bootstrap.less```.
In diesem wird die existierende bootstrap less importiert, damit das template genauso funktioniert wie zuvor:

```
@import "../less/bootstrap";
```

analog gilt das gleiche für ```theme.less```

und dann noch ```Grunfile.js``` auf die neue less umlinken:

```
less: {
      compileCore: {
        options: {
          strictMath: true,
          sourceMap: true,
          outputSourceFiles: true,
          sourceMapURL: '<%= pkg.name %>.css.map',
          sourceMapFilename: 'dist/css/<%= pkg.name %>.css.map'
        },
        src: 'custom-less/bootstrap.less',
        dest: 'dist/css/<%= pkg.name %>.css'
      },
      compileTheme: {
        options: {
          strictMath: true,
          sourceMap: true,
          outputSourceFiles: true,
          sourceMapURL: '<%= pkg.name %>-theme.css.map',
          sourceMapFilename: 'dist/css/<%= pkg.name %>-theme.css.map'
        },
        src: 'custom-less/theme.less',
        dest: 'dist/css/<%= pkg.name %>-theme.css'
      }
    },
```

Dann einfach compilieren:

```
grunt dist
```

und später horchen und bei änderungen durchkompilieren:

```
grunt watch
```

jetzt können einfach die Dateien in ```custom-less``` geändert werden, ohne die Bootstrap Dateien anzufassen.
