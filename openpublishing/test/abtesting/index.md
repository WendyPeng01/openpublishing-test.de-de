# A / B-Tests

**Content-Stufe A / B-Tests:** A / B-Tests auf bestimmte Dokumente oder Ressourcen.

**Globale A / B-Tests:** A / B-Tests für einen breiten Bereich, für die Beispiel-Design und Seitenlayout, für alle Artikel in einem bestimmten Standort (oder ein bestimmtes Gebietsschema) gilt.

   ![](./iceberg.jpg)

## Content-Stufe A / B-Tests
*Content-Ebene / B-Tests* ermöglicht **Eigentümer von Inhalten** zum Self-Service, dass Varianten von Inhalt aus der gleichen URL, das aufteilungsverhältnis angeben und Abrufen von Statistiken BI übermittelt.

Autoren können z. B. **hello.md** und **hello.experimental.md**, und geben Sie, dass nur 10 % der Endbenutzer die Testversion des Dokuments angezeigt wird.

### Entwurfsprinzipien:

1. Aspekte **einfacher** möglichst über Design - vor allem anzusammeln Funktionen, die nicht verwendet werden.
2. Alle **Arten von Inhalt** sollten in der Lage, ein ausführen / B-Tests, einschließlich markdowndateien, einfache HTML-Dateien, Bilder und Audio-und Videodateien.
3. A / B-Tests **Granularität** sollte flexibel, entweder für ein einzelnes Dokument oder für eine große Gruppe von Ressourcen (z. B. Bilder).
4. Benutzer sollten sein **zugeordnet**, sobald einen Benutzer also auf Version A weitergeleitet wurde, sollte er ein Dokument immer angezeigt werden, wenn der Browser-Sitzungsinformationen, (z. B. STRG + UMSCHALT + ENTF oder InPrivate-Sitzung) explizit zurückgesetzt wurde.
5. Sollte **schnelle**, erstellen Sie einen neuen Test, aktivieren/deaktivieren ein A / B-Tests oder das aufteilungsverhältnis aktualisieren sollten wirksam **weniger als 30 Sekunden**.
6. **Ausnahmefällen sollte ordnungsgemäß behandelt werden**, / B-Tests in reibungslos funktionieren sollte eine **CDN Umgebung**. Außerdem sollten spezielle Logik eingerichtet, um sicherzustellen, dass nur die Standard-Variante werden *"das A-Version"* wird abgerufen, indem **Suchmaschinen suchen** wie Google und Bing.
7. Natürlich **integrierte** in BI und Erkenntnisse.

### Interne Flussdiagramm:

   ![](./content-ab-testing-flow.png)

## Globale Ebene A / B-Tests

*Globale Ebene A / B-Tests* ermöglicht zwei wichtige Szenarien:

- Es kann bestimmte Funktion Hypothese praktisch überprüft oder nachgewiesen, in der Regel über eine Zusammenarbeit von **der Funktion Projektbeteiligten, PM-Funktion und Entwickler**.
- Es ermöglicht **engineering-Team** um ein Feature reibungslos.

### Entwurfsprinzipien:

1. Aspekte **einfacher** nach Möglichkeit eine einzige API `Experiment.IsEnabledAsync` auf (JavaScript)-Client und Server (c#)-Seite verwendet werden kann.
2. Vereinfachen Sie Entwickler testen und ein-/ausschalten Side-by-Side-Funktionen angezeigt.
3. Benutzer sollten sein **zugeordnet**, sobald einen Benutzer also gesehen haben ein Feature X aktiviert, er sollte immer X angezeigt, es sei denn, der Browser-Sitzungsinformationen, (z. B. STRG + UMSCHALT + ENTF oder InPrivate-Sitzung) explizit zurückgesetzt wurde.
4. Sollte **schnelle**, einen neuen Test durchführen, aktivieren/deaktivieren ein A / B-Tests oder das aufteilungsverhältnis aktualisieren sollten wirksam **weniger als 30 Sekunden**.
5. Natürlich **integrierte** in BI und Erkenntnisse.

### Interne Flussdiagramm:

   ![](./global-ab-testing-flow.png)

### Beispielcode (ECMAScript)

```javascript
Experiment.IsEnabledAsync('your_cool_feature_name_or_id').done(function(fEnabled){
    if (fEnabled) {
        // do something, in case the experiment is ON for this specific session
    } else {
        // do something else, in case the experiment is OFF for this specific session
    }
});
```

#### Real World (Beispiel)

Bitte versuchen Sie es jetzt! Öffnen Sie die F12-Konsole, und führen Sie den folgenden Code:

```javascript
Experiment.IsEnabledAsync('use_super_large_font').done(function(fEnabled){
    document.body.style['font-size'] = fEnabled ? '300%' : '150%';
});
```


<!--HONumber=May16_HO4-->


