---
description: Na
keywords: na
pagetitle: Conceptual UI Components
search: na
ms.custom:
  - ATA
ms.date: na
ms.prod: identity-ata
ms.technology:
  - security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f9ab356c-4c1c-444c-b221-2451aaebc14b
ms.author: 5f6e9ed0-302d-496f-873c-7a2b94e50410
---
# Grundlegende UI-Komponenten
Auf dieser Seite wird verwendet, um grundlegende Benutzeroberflächenkomponenten Rendern zu testen. Er bezieht sich auf den Entwurf minky Modell.

Im folgenden finden Sie der Link: http://weareminky.com/share/ms/docs/meta/conceptual-ui-components-preview.html

Finden Sie unter den Abzug für diese Datei [in Github](https://github.com/Microsoft/Azure-RMSDocs-pr/blob/master/Azure-RMSDocs/scratch.md); Siehe Abzug [Stilvorgaben des Pilotprojekts EM](https://worldready.cloudapp.net/Styleguide/Edit?id=2781&topicid=36931). 

## Überschrift der zweiten Ebene
### Überschrift der dritten Ebene
#### Überschrift der vierten Ebene
##### Überschrift der fünften Ebene
###### Überschrift der sechsten Ebene

## Textstil

*Fett*  

**Kursiv** 

~~durchgestrichen~~ 


# Links

[Link zu Markdown-Datei in dasselbe Repository](./small.md)
[Link zur externen Website](https://azure.microsoft.com) Bare URLS werden durch Klicken aktivierbaren: http://www.github.com/


## Listen

- Dies
- auf
- a
- Aufzählung
- Liste

1. Dies
2. auf
3. a
4. nummerierte
5. Liste


1. Listen
1. eingebettet
  1. eingebettet
  2. nummerierte
  3. Liste
1. in
1. andere
  - eingebettet
  - Aufzählung
  - Liste
1. Liste

## Prüflisten.

Handelt es sich um eine praktische? 
- [X] dies GFM, aber es auf docs.ms
- [X] Liste Syntax erforderlich (ungeordnete oder eine geordnete Liste unterstützt)
- [X] Dies ist ein Element
- [] Dies ist ein unvollständiges Element


## Horizontale Trennlinie
---

## Tabelle

| Tabellen        | Sind           | Cool  |
| ------------- |:-------------:| -----:|
| ist SP 3      | Rechtsbündig | $1600 |
| ist SP 2      | Zentriert      |   $12 |
| Zebra Streifen | praktisch sind      |    $1 |

## Head Sie eine Kopfzeile.

| Möchten Sie | wirklich benötigen || Damit eine | Kopfzeile.      |



## Code

### Codeblock

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### Inline-code

Dies ist ein Beispiel für `in-line code`.

## BLOCKQUOTE

> Die Trockenheit mussten nun zehn Millionen Jahre dauerte, und die Ringen von der schockierend Lizards hatte längst beendet. Hier auf den Äquator, in dem Kontinent einen Tag als bezeichnete Afrika werden würde der Schlacht um Vorhandensein hat erreicht eine neue Climax von Kämpfe, und die Victor wurde noch nicht im Blick. In diesem Land grobe und verdorrt ist konnte nur kleine oder die Swift der harter Schnörkel oder sogar hoffen überstehen.

## Abbilder

### Statisches Bild
![Dies ist der Alt-text](./image/ATA_config_icon.JPG)

### Verknüpfte Bild

[![aLt-Text für verknüpfte Bild](./image/ATA_Domain_Connectivity_User.JPG)](https://azure.microsoft.com) 

## Warnungen

> [!NOTE] Dies ist zu beachten

> [!WARNING] Diese Warnung ist

> [!TIP] Dies ist die QUICKINFO

> [!IMPORTANT] Dies ist wichtig

## Videos

### YouTube
<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

### Videos zu Azure

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe><br><br>

##docs.ms extentions
### Schaltfläche
> [! Div-Klasse = "button"] [Schaltflächenlinks](./index.md)

### Selektoren
Verwenden Sie einen Switch ermöglichen den Benutzer eine der beiden Optionen oder sogar eine Variation der Optionen auswählen.

Im folgenden sehen Sie Einzelauswahl:
> [! Div-Klasse "Op_single_selector" =]
- [ATA-Bereitstellungshandbuch](./small.md)
- [ATA installieren](./large.md)

Im folgenden sehen Sie mehrere Auswahlzeiger:
> [! Div-Klasse = 1 "Op_multi_selector" = "Platform" Titel2 = "Back-End"]
- [(iOS | .NET)](./small.md)
- [(iOS | JavaScript)](./large.md)

### Schritt für Schritt
Schrittweise Lernprogramme können Sie optional die schrittweise Benutzeroberflächenkomponente am unteren Rand der Artikel einschließen.
> [! Div-Klasse "schrittweise" =]
[vorherige](small.md)
[Weiter](large.md)


<!--HONumber=May16_HO4-->


