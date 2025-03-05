---
layout: post
title: 'Lernpaket Experimente mit USB: 22 spannende USB-Experimente (DE)'
date: 2016-08-21 15:52:00 +0200
last_updated: 2023-04-12
categories: experiments
author: 'Daria Graf'
lang: de
---

# Lernpaket Experimente mit USB: 22 spannende USB-Experimente - mit Java

Im Jahr 2008 habe ich mir das "Lernpaket Experimente mit USB" in einer Buchhandlung in Hamburg gekauft. Leider hatte ich keine Zeit, um das Ding auszuprobieren. Erst im August 2016 habe ich das Lernpaket in einem Bücherschrank beim Aufräumen gefunden und es endlich ausprobiert.

Als Erstes habe ich festgestellt, dass die Experemente für einen Windows-Rechner gedacht sind, ich hatte selber aber einen Mac-Rechner benutzt. Zweites waren alle Experimente für Visual Basic 6.0 gedacht, um den FT232R-USB-Controller zu steuern. Da ich zu dem Zeitpunkt mit Visual Studio noch nie gearbeitet habe und meine kostenlose Visual Studio Code Version den Beispiel-Code nicht aufmachen wollte, habe ich mich dafür entschieden die Beispiele in Java zum Laufen zu kriegen.

Um den USB-Controller auf meinem Mac ansprechen zu können, habe ich einen D2XX-Treiber nach der [Anleitung](https://learn.sparkfun.com/tutorials/how-to-install-ftdi-drivers/all) installiert. Für andere OS-Versionen kann der Treiber hier heruntergeladen werden [FTDI Chip Drivers](https://ftdichip.com/drivers/d2xx-drivers/)

Um die Beispeiele mit Java zum Laufen zu kriegen, muss man eine Library für den FTD2XX-Treiber installieren. Zum Glück konnte ich eine Bibliothek von https://kenai.com/projects/javaftd2xx/downloads finden. Ich habe die Version 0.2.6 benutzt. (! UPDATE von 16.04.2023 - Die Seite ist leider nicht mehr aktiv. Es gibt aber ein [Git-Repository](https://github.com/pkocsis/JavaFTD2XX), wo der Source-Code liegt). Auf der https://kenai.com/projects/javaftd2xx/pages/Home gab es ein Beispiel-Code. Den habe ich etwas angepasst:

```java
public static void main(String[] args) {
    try {
        ArrayList<FTDevice> fTDevices = (ArrayList<FTDevice>) FTDevice.getDevices();
        for (FTDevice fTDevice : fTDevices) {
            System.out.println(fTDevice);
            System.out.println("Device type: "+ fTDevice.getDevType());
            System.out.println("Device ID: "+ fTDevice.getDevID());
            System.out.println("Device location: "+ fTDevice.getDevLocationID());
            System.out.println("Device serial number: "+fTDevice.getDevSerialNumber());
            fTDevice.open();
            System.out.println("Geraet wurde geoffnet!");
            fTDevice.setDtr(true); //hier kann man den DTR manipulieren: 5V-false/aus oder 0V-true/an
            fTDevice.close();
            System.out.println("Geraet wurde geschlossen!");
        }
    } catch (FTD2XXException ex) {
        Logger.getLogger(TestUSB.class.getName()).log(Level.SEVERE, null, ex);
    }
}
```

Beim Ausführen von close()-Methode habe ich immer wieder eine `com.ftdi.FTD2XXException: D2XX error, ftStatus:INVALID_HANDLE Exception` bekommen. Dazu konnte ich im Internet einen Hinweis finden, dass es an der Hardware von meinem Mac liegen könnte. Deswegen, bin ich doch auf einen Windows-Rechner umgestiegen. Dies hat ohne Probleme funktionert. So konnte ich die ersten Beispiele aus dem Handbuch vom Lernpaket erfolgreich in Java umsetzen.
