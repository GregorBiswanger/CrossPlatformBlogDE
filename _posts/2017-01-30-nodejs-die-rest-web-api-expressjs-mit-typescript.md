---
layout: post
title: "Node.js: Die REST Web-API Express.js mit TypeScript"
description: "Bei Node.js hat sich ein Web Application Framework stark durchgesetzt: Express.js."
modified: 2017-27-01
tags: [VSCode, TypeScript, Nodejs, Expressjs, REST, Web-Service]
categories: [Nodejs, TypeScript]
image:
    feature: /Nodejs-cover.jpg
---

Bei Node.js hat sich ein Web Application Framework stark durchgesetzt: Express.js. Dieses wurde vom Sinatra-Framework aus der Ruby-Welt inspiriert. Es erweitert das vorhandene Build-In Modul `http` von Node.js, damit das Entwickeln moderner Webanwendungen einfacher gestaltet wird:  
- Vergleichbar mit der Microsoft Web-API (Nur besser :))  
- Kommunikation mit REST (HTTP) per Standard  
- Request/Response-Handling  
- Routing  
- View Templating  
- Session Support  
- Static Files Support  
- Middleware  
..- Zum Beispiel Funktionen, die sich zwischen Request und Response hängen können (Logger etc.)  
-	Und vieles mehr…  
<!-- more -->  
  
## Die Installation
Zuerst wird ein neues Node.js-Projekt mit einer TypeScript Compiler-Konfiguration benötigt. Passend dazu die Visual Studio Code Build- und Debugging-Konfiguration. Diese Schritte wurden bereits im folgenden Artikel ausführlich erklärt:  
  
  **[Visual Studio Code: Node.js mit TypeScript und Debugging](http://www.cross-platform-blog.de/tools/nodejs/typescript/visual-studio-code-nodejs-mit-typescript-und-debugging "Visual Studio Code: Node.js mit TypeScript und Debugging"){:target="_blank"}**

Zusätzlich wird jetzt Express.js und die TypeScript Deklaration für Express.js benötigt. Dazu innerhalb des Projekts im Terminal folgendes eintippen:  
`npm install express –save`  
`npm install @types/express –save-dev`  
  
## Das erste Express.js „Hello World“
Wir legen eine neue **index.ts**-Datei an oder ersetzen die vorhandene Datei mit dem Inhalt des folgenden Codes:  
  
{% highlight javascript %}
import express = require('express');
let app = express();

app.get('/', function (request, response) {
    response.send('Hello World');
});

app.listen(3000);
{% endhighlight %}
  
Der Code ist sehr ähnlich aus dem gewohnten „Hello World“-Beispiel für Node.js. Die Unterschiede: Express.js erstellt automatisch im Hintergrund bei der `listen`-Funktion einen Web-Server. Die Abfrage für REST wird explizit vergeben, wie hier zum Beispiel mit `get`. Das Routing wird daraufhin mit einem String-Wert festgelegt. Bei der Verarbeitung der Anfrage wird wie gewohnt eine anonyme Funktion ausgeführt, allerdings muss hier kein Stream explizit beendet werden. Darum kümmert sich Express.js automatisch.  
  
## Die GET-Aktion mit Parameter
Eine REST GET-Aktion wird mittels `get`-Funktion hinterlegt. Das Routing wird per String festgelegt und Parameter werden zusätzlich mit Doppelpunkt und Variablenamen gekennzeichnet. Wie folgendes Beispiel zeigt:  
  
{% highlight javascript %}
app.get('/api/sayhello/:name', (request, response) => {
    let name = request.params.name;

    if (!isNaN(name)) {
        response
            .status(400)
            .send('No string as name');
    } else {
        response.json({
            "message": name
        });
    }
});
{% endhighlight %}
  
In Visual Studio Code den TypeScript-Compiler starten `[strg] + [shift] + [b]`, falls dieser noch nicht läuft. Als nächsten die Anwendung mit `[F5]` ausführen. Anschließend im Browser **http://localhost:3000/api/sayhello/John** eingeben.
Der Web-Service sollte nun folgenden JSON-Wert zurückliefern:  
  
{% highlight json %}
{
    "message": "John"
}
{% endhighlight %}
    
Folgende Rückgabe-Funktionen sind mit der Get-Funktion möglich:  
- `render` für HTML-Inhalt mit View Engine  
- `send` für Text-Inhalt  
- `json` für JSON-Inhalt  
- `redirect` zur Weiterleitung  
  
## Queries
Gewöhnliche Query-Parameter können ebenfalls abgefragt werden. Diese befinden sich unter `request.query.PARAMETERNAME`. Ein zusätzliches Festlegen im Routing ist nicht notwendig.  
  
{% highlight javascript %}
app.get('/api/sayhello/', (request, response) => {
    let name = request.query.name;

    let result = {
        message: name
    };

    if (!isNaN(name)) {
        response
            .status(400)
            .send('No string as name');
    } else {
        response.json(result);
    }
});
{% endhighlight %}
  
Als nächsten die Anwendung mit `[F5]` ausführen. Anschließend im Browser **http://localhost:3000/api/sayhello?name=NodeJS** eingeben.
  
## Die Post-Aktion
POST-Aktion mittels `post`-Funktion hinterlegen. Damit allerdings reguläre Form-Submit POST-Anfragen verarbeitet werden können, sind noch zwei weitere Pakete zur Installation notwendig:    
  
`npm install body-parser multer --save`  
   
Diese sind relevant zum Parsen von *multipart/form-data* und *application/x-www-form-urlencoded*. Als Single-Middleware wird `upload.array()` zusätzlich bei der Post-Funktion eingebunden. Forms gesendete Daten werden über `request.body.VARIABLENAME` abgefragt.  
  
{% highlight javascript %}
import express = require('express');
let app = express();

// For POST-Support
let bodyParser = require('body-parser');
let multer = require('multer');
let upload = multer();

app.use(bodyParser.urlencoded({
    extended: true
}));

app.post('/api/sayHello', upload.array(), (request, response) => {
    let name = request.body.name;

    if (!isNaN(name)) {
        response
            .status(400)
            .send('No string as name');
    } else {
        console.log('Hello ' + name);
    }

    response.send('POST request to homepage');
});

app.listen(3000);
{% endhighlight %}
  
Zum Testen eignet sich das Tool [Postman](https://www.getpostman.com "Postman"){:target="_blank"}. Bei Postman an erster Stelle „POST“ auswählen und in das URL-Feld **http://localhost:3000/api/sayhello/** eintippen. Folgende Abfrage kommt dann direkt darunter:  
  
<figure>
	<a href="/images/03/postman-post.jpg"><img src="/images/03/postman-post.jpg" alt="Post-Anfrage mit Postman"></a>
</figure>
  
Jetzt auf den Send-Button klicken und direkt darunter erscheinen die Response-Daten.  
  
<figure>
	<a href="/images/03/vscode-expressjs-debugging.jpg"><img src="/images/03/vscode-expressjs-debugging.jpg" alt="Post-Anfrage mit Visual Studio Code debuggen"></a>
</figure>
  
## Fazit
Mit Express.js kann man schnell und einfach Web-Services bereitstellen und noch viel mehr. In weiteren Artikeln werde ich noch tiefer und weiter auf das tolle Web Application Framework eingehen.
Der Source-Code für die Beispiele liegt auf GitHub:  
    
  <div markdown="0"><a href="https://github.com/GregorBiswanger/VSCodeExpressjsTypeScriptSample" target="_blank" class="btn btn-success">Code on GitHub</a></div>
  
Wie gefällt dir Express.js? Ich bin auf deine Meinung im Kommentar gespannt.
