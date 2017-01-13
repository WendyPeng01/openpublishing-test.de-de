---
description: Na
experiment: true
keywords: na
pagetitle: Install ATA
search: na
ms.custom: 
  - ATA
ms.date: na
ms.prod: identity-ata
ms.technology: 
  - security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.author: 5f6e9ed0-302d-496f-873c-7a2b94e50410
---
# ATA installieren
Im folgenden sind die erforderlichen Schritte zum Abrufen der ATA bereitgestellt, konfiguriert und ausgeführt wird.
[!INCLUDE[ATA](./token/ATA.md)]

Gehen Sie folgendermaßen vor, um ATA zu konfigurieren:

- [Schritte der Vorinstallation](#Preinstallsteps)

- [Schritt 1: Herunterladen und Installieren von ATA Center](#InstallATACtr)

- [Schritt 3: ATA-Gateway-Domänenverbindungseinstellungen konfigurieren](#ConfigConSettings)

- [Schritt 4. Die ATA-Gateway-Setup-Paket herunterladen](#DownloadATA)

- [Schritt 5. ATA-Gateway-installation](#InstallATAGW)

- [Schritt 6. Konfigurieren Sie die Einstellungen für die ATA-Gateway](#ConfigATAGW)

- [Schritt 7 fort. Konfigurieren von VPN-Subnetze und Honeytoken-Benutzer](#ATAvpnHoneytokensetting)

## <a name="Preinstallsteps"></a>Schritte vor der installation

1. Wenn Sie die ATA-public Preview-Version installiert haben, finden Sie unter [ATA-Versionshinweise](./small.md) Hilfestellung bei der Deinstallation der ATA-Preview-Version.

2. KB2934520 auf dem ATA Center-Server installieren und die ATA-Gateway-Server vor der Installation beginnen, andernfalls die ATA-Installation wird dieses Update zu installieren und erfordert einen Neustart in der Mitte der ATA-Installation.

## <a name="InstallATACtr"></a>Schritt 1: Herunterladen und Installieren von ATA Center
Nachdem Sie überprüft haben, dass der Server die Anforderungen erfüllt, können Sie mit der Installation von ATA Center fortfahren.

Führen Sie die folgenden Schritte aus, auf dem ATA Center-Server.

1. Herunterladen von ATA aus der [TechNet Evaluation Center](http://www.microsoft.com/en-us/evalcenter/).

2. Melden Sie sich ein Benutzer, der Mitglied der lokalen Administratorgruppe ist.

3. Führen Sie Setup.EXE von Microsoft ATA Center ein Eingabeaufforderungsfenster mit erhöhten Rechten und führen Sie den Setupassistenten.

4. Auf der **Willkommen** Seite, wählen Sie Ihre Sprache aus, und klicken Sie auf **Weiter**.

5. Lesen Sie den Endbenutzer-Lizenzvertrag, und wenn Sie zustimmen, klicken Sie auf **Weiter**.

6. Auf der **Center Configuration** Seite, geben Sie die folgende Informationen auf der Grundlage Ihrer Umgebung:

   |Feld <br /> <br />|Beschreibung <br /> <br />|Kommentare <br /> <br />|
   |---------|---------------|------------|
   |Installationspfad <br /> <br />|Dies ist der Speicherort, in dem ATA Center installiert werden. Standardmäßig ist dies %programfiles%\Microsoft Advanced Threat Analytics\Center <br /> <br />|Übernehmen Sie den Standardwert <br /> <br />|
   |Pfad der Datenbank-Daten <br /> <br />|Dies ist der Speicherort, in dem die MongoDB-Datenbankdateien gespeichert werden sollen. Standardmäßig ist dies %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data <br /> <br />|Ändern Sie den Speicherort, an eine Stelle, wo Sie Platz basierend auf Ihrer Größe vergrößert haben. **Anmerkung:** <ul><li>In produktionsumgebungen sollten Sie ein Laufwerk verwenden, die anhand der Capacity planning genügend Speicherplatz verfügt. </li><li>Für große Bereitstellungen sollte die Datenbank auf einem separaten physischen Datenträger sein. </li> </ul>Finden Sie unter [ATA Capacity Planning](./small.md) zum Anpassen von Informationen. <br />|
   |Pfad zur Erfassung <br /> <br />|Dies ist der Speicherort, in dem Protokolldateien der Datenbank gespeichert werden sollen. Standardmäßig ist dies %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data\journal <br /> <br />|Für große Bereitstellungen sollte das Journal-Datenbank auf einem separaten physischen Datenträger aus der Datenbank und das Systemlaufwerk. Ändern Sie den Speicherort, an eine Stelle, wenn ausreichend Platz für Ihre Datenbank-Erfassung verwendet. <br /> <br />|
   |ATA Center-Dienst-IP-Adresse: Port <br /> <br />|Dies ist die IP-Adresse, die Kommunikation zwischen dem ATA-Gateways auf die ATA Center-Dienst überwacht. <br /> <br />**Standardport:** 443 <br /> <br />|Klicken Sie auf den Pfeil nach unten, markieren Sie die IP-Adresse, die von den ATA Center-Dienst verwendet werden. <br /> <br />Die IP-Adresse und Port des ATA Center-Diensts nicht identisch mit der IP-Adresse und Port die ATA-Konsole. Stellen Sie sicher, dass den Port der ATA-Konsole. <br /> <br />|
   |SSL-Zertifikat für ATA Center des Diensts <br /> <br />|Dies ist das Zertifikat, das von den ATA Center-Dienst verwendet wird. <br /> <br />|Klicken Sie auf das Symbol zum Wählen ein Zertifikat installiert ist, oder selbst signiertes Zertifikat überprüfen, wenn Sie in einer Lab-Umgebung bereitstellen. <br /> <br />|
   |ATA-Konsole IP-Adresse <br /> <br />|Dies ist die IP-Adresse, die von IIS für die ATA-Konsole verwendet werden. <br /> <br />|Klicken Sie auf den Pfeil nach unten, um die IP-Adresse verwendet, die für die ATA-Konsole auswählen. **Hinweis:** Notieren Sie sich diese IP-Adresse aus dem ATA-Gateway auf die ATA-Konsole erleichtern. <br />|
   |ATA-Konsole SSL-Zertifikat <br /> <br />|Dies ist das Zertifikat von IIS verwendet werden. <br /> <br />|Klicken Sie auf das Symbol zum Wählen ein Zertifikat installiert ist, oder selbst signiertes Zertifikat überprüfen, wenn Sie in einer Lab-Umgebung bereitstellen. <br /> <br />|
   ![](./Image/ATA_Center_Configuration.JPG)

7. Klicken Sie auf **Installieren** ATA und seine Komponenten zu installieren und die Verbindung zwischen dem ATA Center und ATA-Konsole erstellen.

8. Wenn die Installation abgeschlossen ist, klicken Sie auf **Starten**  zur Verbindung mit der ATA-Konsole.

   Die folgenden Komponenten sind installiert und konfiguriert werden, während der Installation des ATA Center:

   - Internetinformationsdienste (IIS)

   - MongoDB

   - ATA Center und ATA-Konsole IIS-Website

   - Benutzerdefinierten Systemmonitor Datensammlungssatz

   - Selbstsignierte Zertifikate (sofern während der Installation)

> [!NOTE]
> Zur Problembehandlung und Produkt-Erweiterung zu erleichtern, wird empfohlen, dass Sie MongoVue und alle anderen MongoDB-add-in oder jedem anderen Drittanbieter-Tool Ihrer Wahl installieren. MongoVue erfordert, dass .net Framework 3.5 installiert sein.

### Überprüfen der installation

1. Überprüfen, ob der Microsoft Advanced Threat Analytics Center-Dienst ausgeführt wird.

2. Klicken Sie auf dem Desktop auf die Verknüpfung Microsoft Advanced Threat Analytics für die ATA-Konsole die Verbindung. Melden Sie sich mit den gleichen Anmeldeinformationen, mit der ATA Center installieren. Beim ersten melden Sie die ATA-Konsole gelangen Sie automatisch an die **domänenverbindungseinstellungen** Seite, um die Konfiguration und die Bereitstellung von den ATA-Gateways fortzufahren.

3. Überprüfen Sie die Fehlerdatei, in der **Microsoft.Tri.Center-"c:\tests"** Datei am folgenden Standardspeicherort gefunden werden kann: %programfiles%\Microsoft Advanced Threat Analytics\Center\Logs.

## <a name="ConfigConSettings"></a>Schritt 2. ATA-Gateway-domänenverbindungseinstellungen konfigurieren
Die Einstellungen im Abschnitt Einstellungen Konnektivität Domäne gelten für alle ATA-Gateways, die von ATA Center verwaltet werden.

Um die Domäne konfigurieren, führen Sie die folgenden auf dem Server ATA Center Konnektivitätseinstellungen.

1. Öffnen Sie die ATA-Konsole, und melden Sie sich. Weitere Informationen finden Sie unter [Arbeiten mit der ATA-Konsole](./small.md).

2. Beim ersten die ATA-Konsole anmelden nach dem ATA Center installiert wurde, werden Sie automatisch zur Seite Konfiguration ATA-Gateways weitergeleitet. Wenn Sie die Einstellungen später ändern möchten, klicken Sie auf das Symbol "Einstellungen", und wählen **Konfiguration**.

   ![](./Image/ATA_config_icon.JPG)

3. Auf der **Gateways** Seite, klicken Sie auf **domänenverbindungseinstellungen**, geben Sie Folgendes ein, und klicken Sie auf **Speichern**.

   |Feld <br /> <br />|Kommentare <br /> <br />|
   |---------|------------|
   |**Benutzername** (erforderlich) <br /> <br />|Geben Sie nur-Lese Benutzernamen ein, z. B.: **user1**. <br /> <br />|
   |**Kennwort** (erforderlich) <br /> <br />|Geben Sie das Kennwort für den Benutzer schreibgeschützt, z. B.: **Pencil1**. **Hinweis:** Stellen Sie sicher, dass das Kennwort richtig ist. Wenn Sie das falsche Kennwort speichern, wird der ATA-Dienst beendet, die auf die ATA-Gateway-Server ausgeführt. <br />|
   |**Domäne** (erforderlich) <br /> <br />|Geben Sie die Domäne für den Benutzer schreibgeschützt, z. B. **contoso.com**. **Hinweis:** Es ist wichtig, dass Sie den vollständigen FQDN der Domäne eingeben, wo sich der Benutzer befindet. Wenn das Konto des Benutzers in der Domäne "corp.contoso.com" ist, müssen Sie eingeben `corp.contoso.com` nicht "contoso.com" <br />|
   ![](./Image/ATA_Domain_Connectivity_User.JPG)

## <a name="DownloadATA"></a>Schritt 3: Die ATA-Gateway-Setup-Paket herunterladen
Nach dem Konfigurieren der domänenverbindungseinstellungen können Sie die ATA-Gateway-Setup-Paket herunterladen.

Die ATA-Gateway-Paket herunterladen:

1. Klicken Sie auf dem Computer ATA-Gateway öffnen Sie einen Browser, und geben Sie die IP-Adresse, die Sie im ATA Center für die ATA-Konsole konfiguriert. Wenn die ATA-Konsole geöffnet wird, klicken Sie auf das Symbol "Einstellungen", und wählen Sie **Konfiguration**.

   ![](./Image/ATA_config_icon.JPG)

2. In der **ATA-Gateways** auf **ATA-Gatewaysetup herunterladen**.

3. Speichern Sie das Paket lokal.

Die Zip-Datei enthält Folgendes:

- ATA-Gateway-installer

- Einstellung der Konfigurationsdatei mit den erforderlichen Informationen zur Verbindung mit dem ATA Center

## <a name="InstallATAGW"></a>Schritt 4. Installieren Sie das ATA-Gateway
Überprüfen Sie vor der Installation der ATA-Gateways, Port-mirroring ordnungsgemäß konfiguriert ist und ob dem ATA-Gateway Datenverkehr zu und von den Domänencontrollern sehen können. Finden Sie unter [Portspiegelung überprüfen](./small.md) Weitere Informationen.

> [!IMPORTANT]
> Stellen Sie sicher, dass [KB2919355](http://support.microsoft.com/kb/2919355/) installiert wurde.  Führen Sie das folgende PowerShell-Cmdlet zu überprüfen, ob der Hotfix installiert ist:
> 
> `Get-HotFix -Id kb2919355`

Führen Sie die folgenden Schritte aus, auf dem ATA-Gateway-Server.

1. Extrahieren Sie die Dateien aus der Zipdatei.

2. Führen Sie Setup.exe von Microsoft ATA-Gateway ein Eingabeaufforderungsfenster mit erhöhten Rechten und führen Sie den Setupassistenten.

3. Auf der **Willkommen** Seite, wählen Sie Ihre Sprache aus, und klicken Sie auf **Weiter**.

4. Unter  **ATA-Gateway-Konfiguration**, geben Sie die folgende Informationen auf der Grundlage Ihrer Umgebung:

   ![](./Image/ATA_Gateway_Configuration.JPG)

   |Feld <br /> <br />|Beschreibung <br /> <br />|Kommentare <br /> <br />|
   |---------|---------------|------------|
   |Installationspfad <br /> <br />|Dies ist der Speicherort, auf dem ATA-Gateway installiert wird. Standardmäßig ist dies %programfiles%\Microsoft Advanced Threat Analytics\Gateway <br /> <br />|Übernehmen Sie den Standardwert <br /> <br />|
   |ATA-Gateway SSL-Zertifikat <br /> <br />|Dies ist das Zertifikat, das von den ATA-Gateway verwendet wird. <br /> <br />|Verwenden Sie ein selbstsigniertes Zertifikat für Lab-Umgebungen nur. <br /> <br />|
   |ATA-Gateway-Registrierung <br /> <br />|Geben Sie den Benutzernamen und das Kennwort des Administrators ATA. <br /> <br />|Geben Sie den Benutzernamen und das Kennwort des Benutzers, der dem ATA Center installiert, für die ATA-Gateway mit dem ATA Center registrieren. Dieser Benutzer muss Mitglied einer der folgenden lokalen Gruppen in ATA Center sein. <br /> <br /><ul><li>Administratoren </li><li>Microsoft Advanced Threat Analytics Administratoren </li> </ul> **Hinweis:** diese Anmeldeinformationen nur für die Registrierung verwendet und ATA nicht gespeichert werden. <br />|
   Die folgenden Komponenten sind installiert und konfiguriert werden, während der Installation des ATA-Gateways:

   - KB 3047154

      > [!IMPORTANT]
      > - Installieren Sie KB 3047154 nicht auf einem Virtualisierungshost. Dadurch kann portspiegelung nicht mehr ordnungsgemäß funktioniert.
      > - Installieren Sie Message Analyzer, Wireshark oder anderen Netzwerk Capture-Software nicht auf dem ATA-Gateway. Wenn Sie den Netzwerkverkehr erfassen müssen, installieren Sie, und verwenden Sie Microsoft Network Monitor 3.4.

   - ATA-Gatewaydienst

   - Microsoft Visual C++ 2013 Redistributable

   - Benutzerdefinierten Systemmonitor Datensammlungssatz

5. Nachdem die Installation abgeschlossen ist, klicken Sie auf **Starten**  Öffnen Ihren Browser, und melden Sie sich auf die ATA-Konsole.

### <a name="ConfigATAGW"></a>Schritt 5. Konfigurieren Sie die Einstellungen für die ATA-Gateway
Nach dem ATA-Gateway installiert wurde, führen Sie die folgenden Schritte aus, um die Einstellungen für die ATA-Gateway konfigurieren.

1. Klicken Sie auf der Maschine ATA-Gateway in der ATA-Konsole auf die **Konfiguration** und wählen Sie die **ATA-Gateways** Seite.

2. Geben Sie die folgende Informationen ein.

   |Feld <br /> <br />|Beschreibung <br /> <br />|Kommentare <br /> <br />|
   |---------|---------------|------------|
   |Beschreibung <br /> <br />|Geben Sie eine Beschreibung des ATA-Gateways (optional). <br /> <br />||
   |**Domänencontroller** (erforderlich) <br /> <br />Siehe unten für Weitere Informationen über die Liste der Controller. <br /> <br />|Geben Sie den vollständigen FQDN des Domänencontrollers, und klicken Sie auf das Pluszeichen, um es der Liste hinzuzufügen. Z. B.  **: dc01.contoso.com** <br /> <br />![](./Image/ATAGWDomainController.png) <br /> <br />|Die Objekte in den ersten Domänencontroller in der Liste werden über LDAP-Abfragen zu synchronisieren. Je nach Größe der Domäne kann dies einige Zeit dauern. **Anmerkung:** <ul><li>Stellen Sie sicher, dass der erste Domänencontroller ist **nicht** schreibgeschützt.   Lesen Sie nur die Domäne, den Controller erst nach Abschluss der ersten Synchronisierung hinzugefügt werden soll. </li> </ul> <br />|
   |**Erfassen von Netzwerkadaptern** (erforderlich) <br /> <br />|Wählen Sie die Netzwerkadapter, die mit dem Switch verbunden sind, die als Ziel Spiegelport zum Empfangen von Datenverkehr auf dem Domänencontroller konfiguriert sind. <br /> <br />|Wählen Sie den Netzwerkadapter für die Erfassung. <br /> <br />|
   ![](./Image/ATA_Config_GW_Settings.jpg)

3. Klicken Sie auf **Speichern**.

   > [!NOTE] Es dauert einige Minuten, bis der ATA-Gateway-Dienst zum ersten Mal starten, da es den Cache des Netzwerks Capture-Parser verwendet, die für die ATA-Gateway erstellt.

Die folgenden Informationen gelten für die Server aus, Sie in geben, der **Domänencontroller** Liste.

- Der erste Domänencontroller in der Liste wird vom ATA-Gateway verwendet werden, um die Objekte in der Domäne über LDAP-Abfragen zu synchronisieren. Je nach Größe der Domäne kann dies einige Zeit dauern.

- Müssen alle Domänencontroller, die von dem ATA-Gateway ist, für deren Datenverkehr über portspiegelung überwacht aufgeführt werden die **Domänencontroller** Liste. Wenn ein Domänencontroller nicht, in aufgeführt ist der **Domänencontroller** Liste Erkennung von verdächtigen Aktivitäten möglicherweise nicht wie erwartet funktionieren.

- Stellen Sie sicher, dass der erste Domänencontroller ist **nicht** einen schreibgeschützten Domänencontroller (RODC).

   Lesen Sie nur die Domäne, den Controller erst nach Abschluss der ersten Synchronisierung hinzugefügt werden soll.

- Mindestens ein Domänencontroller in der Liste wird ein globaler Katalogserver sein. Dadurch können ATA auf Computer- und Objekte in anderen Domänen in der Gesamtstruktur zu beheben.

Die geänderte Konfiguration werden auf dem ATA-Gateway auf die nächste geplante Synchronisierung zwischen dem ATA-Gateway und dem ATA Center angewendet werden.

### Überprüfen der Installation:
Um zu überprüfen, dass der ATA-Gateway erfolgreich bereitgestellt wurde, überprüfen Sie die folgenden Schritte aus:

1. Überprüfen Sie, dass der Microsoft Advanced Threat Analytics Gateway-Dienst ausgeführt wird. Nachdem Sie die ATA-Gateway-Einstellungen gespeichert haben, kann es einige Minuten, bis der Dienst gestartet werden.

2. Wenn der Dienst nicht gestartet wird, überprüfen Sie die Datei ""c:\tests Microsoft.Tri.Gateway-"" im folgenden Standardordner "%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs", suchen Sie nach Einträgen mit "Übertragung" bzw. "Dienst starten".

3. Überprüfen Sie die folgenden Leistungsindikatoren für den Microsoft-ATA-Gateway:

   - **NetworkListener erfasst Nachrichten / Sek.**: Dieser Leistungsindikator verfolgt, wie viele Nachrichten von den ATA pro Sekunde erfasst werden. Der Wert sollte mid Hunderte bis Tausende abhängig von der Anzahl der überwachten Domänencontroller und Auslastung jeder Domänencontroller ist. Einfache oder doppelte Ziffer Werte können ein Problem mit dem Port Spiegelungskonfiguration hinweisen.

   - **EntityTransfer Aktivität Übertragungen/s**: Dieser Wert muss im Bereich von ein paar Hundert alle paar Sekunden.

4. Wenn dies das erste ATA-Gateway installiert ist, nach ein paar Minuten, melden Sie sich die ATA-Konsole, und öffnen Sie die Benachrichtigung im Bereich durch streichen von der rechten Seite des Bildschirms geöffnet. Daraufhin sollte eine Liste der **Entitäten vor kurzem haben** in der Benachrichtigungsleiste auf der rechten Seite der Konsole.

5. So überprüfen Sie, dass die Installation erfolgreich abgeschlossen

   Suchen Sie in der Konsole für etwas in der Suchleiste, z. B. ein Benutzer oder eine Gruppe in Ihrer Domäne.

   Öffnen Sie den Systemmonitor. Klicken Sie in der Struktur der Leistung auf **Systemmonitor** und klicken Sie dann auf das Plussymbol, **einen Zähler hinzufügen**. Erweitern Sie **Microsoft ATA-Gateway** und einen Bildlauf nach unten zum **Network Listener erfasst Nachrichten pro Sekunde** und fügen Sie es hinzu. Stellen Sie dann sicher, dass eine Aktivität im Diagramm angezeigt werden.

   ![](./Image/ATA_performance_monitoring_add_counters.png)

### <a name="ATAvpnHoneytokensetting"></a>Schritt 6. Konfigurieren von kurzfristigen Lease Subnetze und Honeytoken-Benutzer
Kurzfristige Lease Subnetze werden Subnetze, in welche die IP-Adresszuweisung sehr schnell Änderungen - innerhalb von Sekunden oder Minuten. Beispielsweise verwendet IP-Adressen für Ihre VPNs und Wi-Fi-IP-Adressen. Um die Liste der kurzfristigen Lease Subnetze in Ihrer Organisation verwendeten einzugeben, gehen Sie folgendermaßen vor:

1. Der ATA-Konsole auf dem ATA-Gateway-Computer klicken Sie auf das Symbol "Einstellungen", und wählen Sie **Konfiguration**.

   ![](./Image/ATA_config_icon.JPG)

2. Unter **Erkennung**, geben Sie Folgendes für kurzfristige Lease Subnetze. Geben Sie die kurzfristigen Lease Subnetze Schrägstrich Notation Format, z. B. mit:  `192.168.0.0/24` und klicken Sie auf das Pluszeichen (+).

3. Geben Sie für das Honeytoken-Konto-SIDs die SID für das Benutzerkonto an, für die kein Netzwerk, Aktivität, und klicken Sie auf das Pluszeichen (+). Zum Beispiel: `S-1-5-21-72081277-1610778489-2625714895-10511`.

   > [!NOTE] Um die SID für einen Benutzer zu suchen, führen Sie das folgende Windows PowerShell-Cmdlet `Get-ADUser UserName`.

4. Konfigurieren von Ausschlüssen: Sie können konfigurieren, dass IP-Adressen, die von bestimmten verdächtige Aktivitäten ausgeschlossen werden. Finden Sie unter [Arbeiten mit Einstellungen für ATA-](./small.md) für Weitere Informationen.

5. Klicken Sie auf **Speichern**.

![](./Image/ATA_VPN_Subnets.JPG)

Herzlichen Glückwunsch, Sie haben Microsoft Advanced Threat Analytics erfolgreich bereitgestellt.

Überprüfen der Angriff Zeitachse anzeigen verdächtige Aktivitäten und suchen Sie nach Benutzern oder Computern erkannt und ihre Profile anzeigen.

Denken Sie daran, dass es dauert mindestens drei Wochen für ATA-Verhalten Profile erstellen, damit die ersten drei Wochen keine verdächtigen Aktivitäten angezeigt werden.

## Siehe auch
[Für die Unterstützung der Auschecken beantwortet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
[Konfigurieren der Ereignisauflistung](./small.md)
[ATA-erforderliche Komponenten](./small.md)



<!--HONumber=May16_HO4-->


