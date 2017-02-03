---
layout: post
title: "JavaScript Coding Dojo: Der DictionaryReplacer Kata"
description: "Bei diesem Kata handelt es sich um einen einfachen String-Replacer."
modified: 2017-03-02
tags: [TDD, BDD, Jasmine, VSCode, TypeScript, Nodejs, Debugging]
categories: [Coding-Dojo-Katas]
image:
    feature: /JavaScript-Coding-Dojo-cover.jpg
---

Das Dojo ist die Übungshalle in den japanischen Kampfkünsten und die Übungen werden hierbei Kata genannt. Beim Coding Dojo geht es darum eine Übungsaufgabe (Kata) zu meistern. Ganz nach dem Motto „Learning by doing“. Der Cross-Platform-Blog wird jetzt regelmäßig JavaScript Katas veröffentlichen.  

## Der DictionaryReplacer Kata
Bei diesem Kata handelt es sich um einen einfachen String-Replacer. Die Inspiration zu diesem Kata entstand durch einen Vortrag von Cory Haines zum Thema Übungen. Erstelle eine Methode, die einen String und ein Dictionary erhält. Darin soll nun jeder Key des Dictionaries, welcher mit einem Dollarzeichen beginnt und endet, mit dem entsprechenden Wert des Dictionaries ersetzt werden. 

<!-- more -->  

**Tests:**  
input : "", dict empty, output:""  
input : "\$temp\$", dict ["temp", "temporary"], output: "temporary"  
input : "\$temp\$ here comes the name \$name\$", dict ["temp", "temporary"] ["name", "John Doe"], output : "temporary here comes the name John Doe"  

**Schwierigkeit:** Einfach  
**Dauer:** Ca. 5-20 Minuten  
**Quelle:** [http://codingdojo.org/kata/DictionaryReplacer/](http://codingdojo.org/kata/DictionaryReplacer/ "Der DictionaryReplacer Kata"){:target="_blank"}  
  
  
## Vorbereitungen für den Start
Für das Projekt wird folgendes benötigt:
- [Node.js](http://www.nodejs.org "www.nodejs.org"){:target="_blank"} (Läuft auf Windows, Mac und Linux)  
- TypeScript  
  In der Konsole `npm install typescript –g` eingeben  
- [Visual Studio Code](http://code.visualstudio.com "http://code.visualstudio.com"){:target="_blank"} (Läuft auf Windows, Mac und Linux)  
  
Für dich ist bereits ein fertiges Übungsprojekt auf GitHub hinterlegt:  
  
`git clone https://github.com/GregorBiswanger/KataDictionaryReplacer.git`  

Anschließend innerhalb des Projekts mit `npm install` alle nötigen Module installieren.  

> Du kannst kein TypeScript? Keine Sorge! TypeScript == JavaScript und du kannst dein bisheriges JavaScript Wissen ohne Probleme einsetzen. Die Vorteile? Spüre es selbst bei der Codeübung. ;) Ein wesentlicher Unterschied ist, dass die Dateiendung hierbei mit *.TS endet. Die TypeScript erstellten JavaScript und Source Map-Dateien habe ich für die Übung von Visual Studio Code ausblenden lassen. Das sorgt für eine bessere Übersicht. Im Dateisystem existieren diese allerdings.  
  
## Der Start
1.	Öffne das Projekt mit Visual Studio Code  
2.	Starte den TypeScript Compiler mit der Tastenkombination `[strg] + [shift] + [b]`  
3.	Beim Terminal gibst du innerhalb deines Projekts `npm test` ein  

Jetzt läuft der Testrunner Jasmine und bemerkt Dateiänderungen automatisch. Hast du einen zweiten Monitor, ist dort für den Terminal der ideale Platz. So kannst du während der Entwicklung den aktuellen Status beobachten.   
  
<figure>
	<a href="/images/04/vscode-npm-test.jpg"><img src="/images/04/vscode-npm-test.jpg" alt="npm start"></a>
</figure>
  
## Der Prozess
Wichtig bei Coding Dojo ist mit Babysteps die Lösung zu meistern. Löse jede Aufgabe Schritt für Schritt und nicht alles auf einmal. Dieses Prinzip ist für viele Entwickler nicht einfach, aber genau die Vorteile an dieser Herangehensweise lehrt uns ein Coding Dojo.  

Welche Aufgaben Schritt für Schritt erfüllt werden müssen, findest du im `spec`-Verzeichnis. Beim `src`-Ordner findet dann die eigentliche Programmierung statt.
  
## Debugging
Das Projekt hat bereits alle nötigen Visual Studio Code Einstellungen, so dass du ohne Probleme innerhalb der Tests oder beim eigenen Code debuggen kannst. Dazu einfach mit der `[F9]`-Taste einen Breakpoint setzen und mit `[F5]` das Debugging starten.

<figure>
	<a href="/images/04/vscode-jasmine-debugging.jpg"><img src="/images/04/vscode-jasmine-debugging.jpg" alt="Unit Test Debugging"></a>
</figure>

## Regeln
-	Löse das Kata bis alle Tests grün sind
-	Anschließend kopiere deine Lösung hier auf jsfiddle.net:
  **[https://jsfiddle.net/GregorBiswanger/n6zm9wz7/](https://jsfiddle.net/GregorBiswanger/n6zm9wz7/ "jsfiddle.net"){:target="_blank"}**
-	Klicke links oben auf den „Update“-Button und kommentiere deinen Link hier bei diesem Blog-Post
-	Erst dann, darfst du deine Lösung gerne mit bereits Kommentierten Lösungen vergleichen

<figure>
	<a href="/images/04/jsfiddle-typescript-jasmine.jpg"><img src="/images/04/jsfiddle-typescript-jasmine.jpg" alt="jsfiddle kata mit typescript und jasmine"></a>
</figure>

## Let's get ready to rumble!
Bei meinen JavaScript Schulungen mache ich immer wieder gerne Katas mit meinen Teilnehmern. Ich liebe es anschließend die unterschiedlichen Lösungen zu begutachten. Ich bin auch jetzt gespannt, wie du die Aufgabe meistern wirst. Und jetzt: Let's get ready to rumble!

