#Benutzerhandbuch - Inhalt auf ein / B-Tests

##Voraussetzung

![](./UM-Prerequisite.png)
- Führen Sie den Schritt [Verknüpfen Sie die Microsoft-GitHub-Organisation](http://https://opensourcehub.microsoft.com/articles/how-to-join-microsoft-github-org-self-service) Ihres GitHub-Kontos mit Microsoft-Organisation zu verknüpfen.
- Lesen die Anweisung CSI zu verstehen, wie den Prozess zum **Erstellen** / **Bearbeiten** /**COMMIT** Markdown-Datei in GitHub. In diesem Handbuch wirklich nicht berücksichtigen Content Erstellung/Überarbeitung.
- Mit **arbeiten** Zweig vor dem Zusammenführen in Live-Umgebung immer einen **BEST Practices**.

##Schritt für Schritt

###Erstellen eines neuen Experiments

![](./UM-New-Content-Experiment.png)

####Teil I: Einrichten experimentellen Dateien in Ihrer arbeitsverzweigung.

- A / B-Tests erfordert zwei separate markdowndateien, die eine Variante und die B-Variante. Möglicherweise haben Sie bereits eine A-Variante als eine veröffentlichte Seite.

1. Wechseln Sie zu Ihrem **arbeiten** Zweig:
    - Wenn Sie lokal arbeiten, wechseln Sie zu Ihrer lokalen staging-Verzweigung. Die staging-Verzweigung ist unabhängig davon, welche Verzweigung, die Sie verwenden, um die Änderungen zu übernehmen, die veröffentlicht wird [Phase Endpunkt](https://stage.docs.microsoft.com).

2. Bearbeiten Sie die Variante einer Seite:
    - Die Quelldatei (Seite A) bearbeiten, indem Sie die folgende Metadaten hinzufügen:
        > `experiment:true`
        >`experiment_id:`,

        `experiment_id` ist eine eindeutige Id für Ihr Experiment. Es wird empfohlen, Ihre Experiment-Id im Format &lt;Youralias&gt;-&lt;Experimentname&gt;-&lt;Datum&gt;

3. Variant-B-Seite zu erstellen:
    - Erstellen Sie eine Variante B-Seite für das Thema im gleichen Ordner alle Metadaten der ursprünglichen Seite A verwenden. Hinzufügen der `experiment_id` Feld und verwenden Sie dieselbe Experiment-ID, die Sie erstellt haben, für die eine Variante.
    - Verwenden Sie die folgende Struktur des Dateinamens beim Speichern der Seite Variant B: &lt;Sourcefilename&gt;`.experimental.md`. Beispiel:
        - Wenn ein Variant CSI demo.md ist, müssen B Variant CSI demo.experimental.md.

4. Hinzufügen, und die Änderungen zu übernehmen:
    - Wenn Sie lokal arbeiten, müssen Sie diese lokalen Änderungen mit der staging-Verzweigung auf GitHub mit eine Pull-Anforderung zusammengeführt. Wenn Sie auf GitHub arbeiten, einfach Änderungen Sie die. Nachdem die Dateien in die staging-Verzweigung auf GitHub ein Commit ausgeführt werden, wird es automatisch den OP Build für die staging-Verzweigung ausgelöst.

5. Vorschau auf das Ergebnis vom Portal:
    - OP-Portal geöffnet ist, warten Sie, bis der Build abgeschlossen ist, ohne dass Fehlermeldung angezeigt.

    ![](./UM-OP-Portal.png)

    - Phase-Website öffnen, und das Ergebnis der Vorschau anzeigen.

6. Die Variante A und Variant B mit Live-Verzweigung zusammenführen
    - Nachdem Sie bestätigt haben, dass die Varianten A und B auf dem staging-Server verfügbar sind, verbinden Sie die Variante A und B Variant-Dateien auf der **Live** Zweig für die Veröffentlichung der Produktionswebsite.


####Teil II: Erstellen eines Experiments auf A / B-Tests Portal für die Konfiguration.

1. Erstellen Sie ein Experiment:

    - Öffnen Sie [ein / Portal für die Konfiguration von B](https://abtestingportal.azurewebsites.net/#/experiments), und klicken Sie auf **EXPERIMENTIEREN hinzufügen** ein neues Experiment erstellt.

    ![](./UM-AB-Portal-Experiments.png)

        - Experiment id fields can be either `document_id` or `experiment_id` in the Variant A page. For now, please enter the `experiment_id` you created for your experiment.

    ![](./UM-AB-Portal-Experiment-New.png)

        - Select the percentage of users who will see Variant B. The percentage can be from 0% to 100%, we recommend 50% as a starting point. Enter the percentage *without* a percent sign.
        - Select the maximum number of users who will see the B variant. Note that at the moment this is not enforced (the experimentation framework *will* keep track of how many users see the B variant, but it will *NOT* yet automatically shut off the experiment when that number is reached). A good number to start with is in the range of 500 – 1000.
    - Speichern Sie das Experiment. Sie werden auf der Titelseite experimentieren Portal zurückgegeben werden.
    - Das Ergebnis in der Vorschau anzeigen, indem das Präfix `https://stage.docs.microsoft.com/_chrome/experiment.htm#` Wechseln zwischen Ihrer Seite A und B.

2. Der Setup-Metriken:
    - Erweitern Sie das Experiment von [A / B-Konfiguration Portal](https://abtestingportal.azurewebsites.net/#/experiments).

    ![](./UM-AB-Portal-Metrics.png)

    - Klicken Sie auf **Bearbeiten** von **METRIK CONFIG** Registerkarte.

    ![](./UM-AB-Portal-Metrics-Config.png)

3. Starten Sie das Experiment:
    - Klicken Sie auf die **START** Schaltfläche, um das Experiment zu starten.

    ![](./UM-AB-Portal-Experiments-Action.png)

4. Überwachen Sie die metrische Ergebnis:
    - Klicken Sie auf **METRIK Ergebnis** um das Ergebnis anzuzeigen. (Beachten Sie, wird es dauert zu 4 bis 6 Stunden zum Anzeigen des Ergebnisses aufgrund der Wartezeit von WEDCS)

    ![](./UM-AB-Portal-Metrics-Result.png)

###Bereinigen Sie A / B-Tests sobald er abgeschlossen ist.

![](./UM-Cleanup-Content-Experiment.png)

1. Backup das Ergebnis das Ergebnis von METRIK Ergebnis in Excel exportieren:
    - Öffnen Sie A / B-Konfiguration-Portal, und wählen Sie das Experiment.
    - Wählen Sie die metrische, klicken Sie auf **METRIK Ergebnis** Registerkarte, und klicken Sie dann auf **EXCEL EXPORTIEREN** So exportieren Sie das Ergebnis.
    - Wiederholen Sie die **EXCEL EXPORTIEREN** für alle zugehörigen Metriken.

    ![](./UM-AB-Portal-Metrics-Result.png)

2. Beenden Sie das Experiment:
    - Klicken Sie auf die **Beenden** Schaltfläche, um das Experiment zu beenden.

    ![](./UM-AB-Portal-Experiments-Action.png)

3. Löschen Sie das Experiment von [A / B-Konfiguration Portal](https://abtestingportal.azurewebsites.net/#/experiments):
    - Klicken Sie auf **Löschen** Schaltfläche, um das Experiment aus der Liste zu entfernen.

4. Bereinigen Sie unnötiger Variant-Version.
    - Nach dem Abschluss des Experiments sollten Sie die endgültige Version behalten und unnötige Version von Dokument-Repository löschen.
        - Wenn eine Variante wählen, löschen Sie den Variant b.
        - Wenn Variant B auswählen und kopieren Sie den Inhalt aus Variant B Variante a Variant b löschen

5. Bereinigen von Metadaten aus Markdown-Datei
    - Entfernen Sie `experiment:true` und `experiment_id` aus endgültige Markdown-Datei

6. Die Änderungen.

## Weitere Ressourcen
- Umgebung: [Umgebungen - Content-Ebene](http://onenote:#Environments%20-%20Content%20Level&section-id={7011B86A-3C76-4C37-8F41-C26A380ADAEC}&page-id={B1125C68-7C08-49DA-A45C-8ADE3A315520}&end&base-path=https://microsoft.sharepoint.com/teams/Visual_Studio_China/Shared%20Documents/Open%20Publishing/AB%20Testing.)

<!--HONumber=May16_HO4-->


