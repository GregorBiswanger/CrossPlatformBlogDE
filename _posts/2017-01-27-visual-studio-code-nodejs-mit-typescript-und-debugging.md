---
layout: post
title: "Visual Studio Code: Node.js mit TypeScript und Debugging"
description: "Ein neues Node.js Projekt mit VSCode und TypeScript anlegen."
modified: 2017-27-01
tags: [VSCode, TypeScript, Nodejs, Debugging, Debugger]
categories: [Tools, Nodejs, TypeScript]
image:
    feature: /VSCode-TypeScript-cover.jpg
---

Die kostenfreie Entwicklungsumgebung Visual Studio Code von Microsoft, bietet eine hervorragende Unterstützung von TypeScript und die Entwicklung von Node.js-Projekten. Dieser Blog-Post zeigt, wie einfach ein neues Node.js-Projekt mit TypeScript-Support erzeugt wird. Gegen Ende wird auch ein kleines „Hallo Welt“-Beispiel im Debug-Modus durchlaufen.  
  <!-- more -->
  
Für das Beispiel werden folgende Installationen benötigt:  
- [Node.js - http://www.nodejs.org](http://www.nodejs.org "www.nodejs.org"){:target="_blank"} (Läuft auf Windows, Mac und Linux)  
- TypeScript  
  In der Konsole `npm install typescript –g` eingeben  
- [Visual Studio Code - http://code.visualstudio.com](http://code.visualstudio.com "http://code.visualstudio.com"){:target="_blank"} (Läuft auf Windows, Mac und Linux)  
  
## Ein neues Projekt
Für ein neues Projekt wird nur ein neues Verzeichnis benötigt. In Visual Studio Code wird dieses im Menü über `File | Open Folder…` geöffnet. Als Projektdatei wird die packages.json-Datei benötigt. Dazu wird in der Konsole `npm init -y` eingetippt (In VSCode unter Windows `[Strg] + [ö]` die integrierte Konsole öffnen).

<figure>
	<a href="/images/02/vscode-npm-init.jpg"><img src="/images/02/vscode-npm-init.jpg" alt="Visual Studio Code"></a>
</figure>

## Node.js Deklaration-Dateien installieren
Damit Visual Studio Code die Funktionen von Node.js per IntelliSense auflösen kann, werden die TypeScript Deklaration-Dateien von Node.js benötigt. Diese installiert man ab TypeScript 2 über den Node Package Manager (NPM). Für Node.js wird dazu `npm install @types/node –save-dev` eingegeben. Für andere Pakete würde man dann zum Beispiel: `npm install @types/jquery –save-dev` aufrufen.

## TypeScript Compiler-Konfiguration
Für einen geeigneten Node.js-Support mit TypeScript, wird eine Compiler-Konfigurationsdatei benötigt. Diese legen wir im Root-Verzeichnis mit dem Namen `tsconfig.json` an. Dank dem JSON IntelliSense-Feature von Visual Studio Code, wird automatisch anhand des Dateinamens eine Autovervollständigung bereitgestellt. Dazu einfach die ersten geschweiften Klammern setzen und das IntelliSense mit der Tastenkombination `[Strg] + [.]` auslösen. Die Schema Informationen dazu bezieht sich Visual Studio Code direkt übers Internet. Sollte keine Verbindung möglich sein, entfällt leider der IntelliSense-Support. Tippe dazu die folgende Compiler-Konfiguration:  
    
{% highlight json %}
{
    "compilerOptions": {
        "module": "commonjs",
        "sourceMap": true,
        "watch": true
    }
}
{% endhighlight %}
  
**Module**: Bei einer klassischen Web-Anwendung bezieht sich der Browser über das Script-Tag die JavaScript Dateien. Bei Node.js wird der JavaScript code unabhängig einer Web-Seite ausgeführt. Daher wurde ein Modul-System mit dem Namen CommonJS ins Leben gerufen. Dieses ermöglicht das Laden von JavaScript-Dateien aus JavaScript-Code heraus. TypeScript benötigt daher die Information, welches Modul-System eingesetzt wird, um den passenden Code automatisch von „import“ und „export“ generieren zu können.    

**Source Map**: Wie der Name bereits sagt, werden hierbei Dateien generiert, die als Karte für den Debugger-Service dienen. Diese helfen dem Debugger dabei, eine Code-Stelle der TypeScript-Datei auf die generierte JavaScript-Datei aufzulösen. Dank diesem Konzept, wird das Debuggen direkt aus der TypeScript-Datei ermöglicht.    

**Watch**: Damit nicht vor jedem Debugging der TypeScript-Compiler gestartet werden muss, hilft die Watch-Option. Diese beobachtet alle TypeScript-Dateien auf Änderungen. Sollte sich eine Datei ändern, so wird automatisch der Compiler aktiv. So reicht es aus, dass nur einmalig der Compiler gestartet werden muss.  
  
## Das erste Node.js „Hello World“
Jetzt legen wir eine **index.ts**-Datei an. Dazu wird folgender Code für ein „Hello World“ Beispiel benötigt:  
  
{% highlight javascript %}
import http = require('http');

http.createServer((request, response) => {
    response.write('Hallo von Node.js!');
    response.end();
}).listen(3000);
{% endhighlight %}
  
Die erste Zeile beginnt mit einem TypeScript-Spezifischen Keyword `import`. Damit weiß TypeScript, dass es zu diesem Modul eine Deklaration existieren muss. Sollte keine Deklarations-Datei oder ein TypeScript-Code im Projekt vorhanden sein, wird wie gewöhnlich einfach `let` geschrieben. Dann greifen wir auf ein Node.js Build-In Modul `http` von Node.js zu. Die erste Zeile ist somit vergleichbar wie ein `using`, `import` oder `include` aus anderen Hochsprachen.  
  
Ab Zeile 3 wird bereits ein Web-Server erzeugt. Beim Aufruf wird die anonyme Funktion ausgelöst und ein Streaming zum Client ist aktiv. Hier erhalten wir alle Client Anfrageinformationen beim `request`-Parameter. Über den `response`-Parameter können wir Daten an den laufenden Stream hängen. Dazu wurde die einfache `write`-Funktion genutzt, um einen einfachen String-Wert zu senden. Um den laufenden Stream zu beenden, wird die `end`-Funktion benötigt.
Mit der `listen`-Funktion wird der aktuelle Web-Server für den definierten Port aktiv. Das war es auch schon.
  
## TypeScript Compiler starten über Visual Studio Code
Die TypeScript-Datei wurde geschrieben, allerdings wird ja eine JavaScript-Datei zum Ausführen benötigt. Mit der Tastenkombination `[Strg] + [Shift] + [b]` wird Visual Studio Code zum Builden aufgefordert. Alternativ kann auch die Command-Line mit `[F1]` geöffnet werden und man Tippt `Build` ein. Nun weiß Visual Studio Code nicht, was genau es machen soll. So erfolgt eine Anfrage, was genau man möchte. Hierbei wählen wir `TypeScript – tsconfig.json` aus.   
  
<figure>
	<a href="/images/02/vscode-no-task-runner-configured.jpg"><img src="/images/02/vscode-no-task-runner-configured.jpg" alt="Visual Studio Code - No task runner configured"></a>
</figure>

<figure>
	<a href="/images/02/vscode-select-a-task-runner-typescript.jpg"><img src="/images/02/vscode-select-a-task-runner-typescript.jpg" alt="Visual Studio Code - Select a task runner"></a>
</figure>


Es wird ein neues Verzeichnis mit `.vscode` erzeugt und eine tasks.json-Datei angelegt. Das angenehme an diesem Template ist, dass bereits alle relevanten Einstellungen hinterlegt sind. So können wir diese Datei wieder schließen und rufen wiederholt den Build-Vorgang mit `[Strg] + [Shift] + [b]` auf. Links unten sehen wir ein rotierendes Zeichen und im File-Explorer sehen wir zwei neue Dateien zu unserer TypeScript-Datei. Einmal die generierte JavaScript-Datei und die SourceMap-Datei, die für das Debuggen nötig ist.
  
## Debuggen der Node.js-Anwendung
Zum Ausführen der Anwendung gibt es unterschiedliche Möglichkeiten. Eine Möglichkeit ist es, unabhängig von Visual Studio Code über die Konsole mit `node index.js` zu starten. Nur haben wir hierbei keinen Debugging-Komfort. Deshalb nutzen wir die zweite Variante: In Visual Studio Code einfach die `[F5]`-Taste zum Debuggen drücken. Auch hier weiß Visual Studio Code erstmal nicht, was er Ausführen soll. Wir wählen hierbei das `node.js`-Template
 aus.   
  
<figure>
	<a href="/images/02/vscode-select-environment-nodejs.jpg"><img src="/images/02/vscode-select-environment-nodejs.jpg" alt="Visual Studio Code - Select environment node.js"></a>
</figure>
  
Hier wird im `.vscode`-Verzeichnis eine weitere JSON-Datei angelegt. Wichtig ist hierbei zu beachten, dass der JavaScript-Dateiname dem entspricht, was wir angelegt haben und das die Option Source Maps aktiviert ist. Ansonsten können wir nur innerhalb der JavaScript-Datei Debuggen. Anschließend drücken wir wieder die `[F5]`-Taste. Der Server wurde nun ausgeführt. Wenn wir in der `response.write`-Zeile die Taste `[F9]` drücken, oder alternativ neben der Zeilennummer klicken, erhalten wir einen roten Breakpoint. Geht jetzt in den Browser und ruft euren Web-Server mit http://localhost:3000 auf. Visual Studio Code stoppt dann beim Breakpoint und ihr könnt alle Parameter-Werte überprüfen, wie ihr es beim Debugging anderer Hochsprachen gewohnt seid.  
  
<figure>
	<a href="/images/02/vscode-nodejs-debugging.jpg"><img src="/images/02/vscode-nodejs-debugging.jpg" alt="Visual Studio Code - Node.js debugging"></a>
</figure>
  
Sollte es zu Problemen kommen, liegt es meistens daran, dass man vergessen hat einmalig den TypeScript-Compiler zu starten. Überprüft daher, ob auch eure JavaScript- und SourceMap-Dateien erzeugt wurden.
  
## Fazit
Visual Studio Code ist ein großartiges Tool für die Entwicklung mit Node.js und TypeScript. Mit nur wenigen Zeilen Code, haben wir einen Web-Server und ein REST Web-Service erzeugt. So ganz ohne IIS, Tomcat oder Apache HTTP Server.
Das Beispiel habe ich hier auf GitHub hinterlegt: 
  
  <div markdown="0"><a href="https://github.com/GregorBiswanger/VSCodeNodejsTypeScriptSample" target="_blank" class="btn btn-success">Code on GitHub</a></div>
  
Konnte dir der Artikel helfen? Hast du weitere Fragen? Dann schreib mir ein Kommentar!
