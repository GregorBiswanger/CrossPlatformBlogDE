---
layout: post
title: "Interview mit webpack Gründer Tobias Koppers"
description: "Webpack wird weltweit von mehreren Millionen Entwicklern eingesetzt. Wir bekamen die Chance, ein Exklusivinterview mit Tobias Koppers, dem Autor von webpack, zu führen."
modified: 2017-03-04
tags: [webpack, interview, tooling, javascript, grunt, gulp]
categories: [Tools]
image:
    feature: /webpack-cover.jpg
---

Tobias Koppers ist freiberuflicher Software-Entwickler und Berater aus Nürnberg. Bekannt wurde er als Autor von webpack, das weltweit von mehreren Millionen Entwicklern eingesetzt wird. Seine Schwerpunkte liegen bei der JavaScript Entwicklung und Open-Source Projekten. Ich konnte ein Exklusivinterview mit Tobias führen, das ich euch nicht vorenthalten möchte. Viel Spaß beim Lesen.  

<!-- more -->  

**Gregor: Hallo Tobias, die ganze JavaScript-Welt spricht über webpack. Sogar Google setzt darauf und hat es direkt bei der Angular CLI integriert. Ich bin auch ganz besonders stolz darauf, dass webpack aus Nürnberg, der Nähe meiner Heimatstadt Ingolstadt stammt. Erzähl uns doch mal die Geschichte, wie du auf die Idee gekommen bist und wie webpack sich so schnell verbreiten konnte.**  
  
**Tobias:** Hi Gregor. Tatsächlich war Google in der Entstehung auch involviert, wenn auch nur indirekt. Bevor ich süchtig nach JavaScript wurde habe ich auch mal mit Java gearbeitet. Hier gibt es ein Tool von Google welches es ermöglicht eine clientseitige Web-Anwendung in Java zu entwickeln: Google Web Toolkit (GWT). Das ist ein Java-zu-JavaScript Compiler für SPAs, welcher auch Basis von einigen Google Anwendungen ist.  
  
Beim GWT hat mir besonders ein Feature besonders gefallen: Code Splitting. Dies ermöglicht unter anderem selten benutzten Code erst später nachzuladen. Diese Feature ist besonders wichtig für große Anwendungen um die initiale Ladezeit klein zu halten. Mir hat dieses Feature in existierenden JavaScript-Tooling gefehlt (2012) und daraus ist letztlich webpack entstanden.  
  
Das heißt webpack ist mit dem Fokus auf Code Splitting entstanden, und meiner Meinung nach war das auch der Grund warum es sich so verbreitet hat. Mit wachsender Größe von Webanwendungen und gleichzeitigen verstärkten Gebrauch von mobilen Geräten (mit schwacher Netzanbindung) sie die Relevanz von Code Splitting mit der Zeit gewachsen. Ansonsten lässt sich die gewünschte Performance nur schwer umsetzen.  
  
**Gregor: Viele vergleichen webpack mit Task-Tools wie NPM-Scripts, Grunt und Gulp. Einige haben mit webpack auch wirklich ihren Ersatz gefunden. Ich selbst nutze zukünftig auch nur noch NPM-Scripts und webpack. Wie stehst du zu diesem Thema und nutzt du ein Task-Tool zusätzlich zu webpack?**  
  
**Tobias:** Mir selbst reichen NPM Skripte auch aus. Tatsächlich ist aber eigentlich nicht richtig webpack als Ersatz für Grunt/Gulp zu bezeichnen. Grunt und Gulp fallen in eine andere Kategorie von Tools wie webpack. Grunt, Gulp und NPM Skripte sind Task Runner.  
  
Webpack ist ein Module Bundler. Dies sind Werkzeuge mit unterschiedlichen Zielen. Es ist aber richtig, dass webpack die notwendigen "Tasks" zum Bauen einer Web-Anwendung soweit vereinfacht, dass es eventuell ein Overkill ist Task Runner wie Grunt und Gulp zu verwenden und NPM Skripte ausreichen. NPM ist also der Ersatz für Grunt und Gulp.  
  
Allerdings haben Task Runner immer noch ihre Daseinsberechtigung für andere Aufgaben neben vom reinen Bauen der Web-Anwendung: Deployment, Linting, Versionsmanagement, etc.  
  
**Gregor: Bei meinen JavaScript Schulungen bekomme ich bei meinen Teilnehmern immer wieder mit, wie schwer Ihnen der Einstieg mit webpack fällt. Hast du dazu auch schon Feedback bekommen? Wenn ja, hast du auch schon Ideen, wie man das verbessern kann?**  
  
**Tobias:** Ja tatsächlich kommt dieses Feedback auch an. Allerdings sagen auch viele Nutzer, dass sobald es erstmal "Klick" gemacht hat, ist es eigentlich recht einfach zu benutzen. Wer webpack "kann" sagt sogar, dass es einfacher ist als die vorherigen Tools.  
  
Ich glaube dieses Feedback ist darin begründet, dass die Konzepte von webpack deutlich von den Konzepten anderer Tools abweichen. Vor allem bei der Migration von Grunt/Gulp zu webpack. Task Runner haben eher eine imperative Konfiguration, d. h. man beschreibt die Schritte die vom Task Runner auszuführen sind. Webpack hingegen hat eine deklarative Konfiguration, d. h. man beschreibt nicht die Schritte die webpack ausführen soll, sondern beschreibt nur die Art und Weise wie diese Schritte auszuführen sind bzw. wie das Ergebnis auszusehen hat.  
  
**Gregor: Was steht noch auf deiner Agenda? Welche Features sind bei der nächsten webpack-Version geplant?**  
  
**Tobias:** Das ist noch nicht ganz klar. Es gibt so viele Dinge die möglich sind. Um nur einige spannende Punkte zu nennen:
* Scope Hoisting: kleine und performantere Art die Module zusammenzuhängen  
* WebAssembly: Unterstützung von binärem Code in der WebApp  
* Persistenter Cache: Schnelleres initiales Kompilieren  
* CSS (und HTML) als First-Class-Citizen: Schönere Unterstützung für Stylesheets (und HTML)  
* Und noch viele spannende Kleinigkeiten  
  
In welcher Reihenfolge diese angegangen werden entscheiden die Nutzer und Sponsoren. Wir haben eine Voting-Seite auf dieser für die nächsten Punkte abgestimmt werden kann. Jeder bekommt täglich einen Einflusspunkt und Sponsoren und Contributor bekommen für Spenden bzw. Contributions goldene Einflusspunkte. Das geschieht aus der Motivation heraus Sponsoren und Contributor etwas zurückgeben zu wollen. Außerdem ist es natürlich interessant was Nutzer am meisten wollen.  
  
**Gregor: Kannst du uns einen Top Best Practictes Tipp zu webpack verraten?**  
  
**Tobias:** On-Demand-Loading verwenden. Es ist super einfach zu verwenden und bringt unglaublich viel.  
  
**Gregor: Was sind deine persönlichen Ziele? Werden wir bald alle lesen, dass du bei Google in Mountain View arbeiten wirst? ;)**  
  
**Tobias:** Eher nicht. Ich werde demnächst als Freelancer arbeiten. Ich werde versuchen so viel wie möglich an Open Source zu arbeiten und das Ganze über Spenden zu finanzieren. Da Spenden allerdings meist nicht reichen, werde ich den Rest über Auftragsarbeiten oder Consulting finanzieren. Ich bin schon gespannt wie das läuft. Vielleicht findet sich ja ein Sponsor der mir ein paar zusätzliche Wochen Open Source finanziert (hey Google ;) ).  
  
Der Aufwand ein Open Source Projekt zu maintainen wird häufig unterschätzt. Aktuell verbrauchen Code Reviews und Issues 80% meiner Zeit. Ich komm kaum noch dazu selbst Code zu schreiben, geschweige denn zu Refactorn. Ich muss sogar teilweise Pull Requests erstmal eine Zeit liegen lassen bevor ich die Zeit finde sie im Detail anzuschauen. Das ist natürlich demotivierend für die Contributor. Ich denke, dass sich das ändern kann, wenn ich Vollzeit an webpack arbeite. Hoffentlich habe ich dann auch mehr Zeit um selbst mehr Code zu schreiben.  
  
**Gregor: Ganz vielen Dank, dass du dir die Zeit für uns und das Interview genommen hast! Danke auch für webpack, das uns JavaScript-Entwickler extrem unterstützt. Ich liebe dein Tool!**  
  
**Tobias:** Gerne. Mein Dank geht zurück an die Community. Webpack ist nicht "mein" Tool, es wird von mehr als 500 Contributoren gestaltet. Zu webpacks Erfolg zählt auch sein großes Ecosystem.

