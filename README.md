# Nextcloud-on-Linux

### Einleitung:

Willkommen zu unserem Schulprojekt im Modul 239 (Internetserver in Betrieb nehmen), in dem wir eine Nextcloud-Umgebung in Linux aufbauen! Das Projekt wird mit Robin Kraft und Samuel Nick durchgeführt. Nextcloud ist eine beliebte Cloud-Speicherlösung, die uns ermöglicht, Dateien sicher auszutauschen und zu speichern. In diesem Projekt werden wir unsere Linux-Kenntnisse erweitern, indem wir eine Nextcloud-Instanz aufsetzen und konfigurieren. Dabei lernen wir wichtige Aspekte wie die Auswahl der Linux-Distribution, die Installation von Webservern und Datenbanken sowie die Benutzerverwaltung und das Datei-Sharing. 

### Was wird alles benötigt?

- 2x Ubuntu Clients (ubuntu-22.04.2 - grafische Oberfläche)
- Windows Client


### Unser Vorgehen:

Vorrausgesetzt sind alle oben aufgeführten Clients komplett installiert und im selben Netz.

Als erstes führt man den Befehl "sudo apt-get update" aus, um sicherzustellen das die neusten Updates installiert werden.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/3477f769-fdb8-40dd-a8b0-5b0c6958379b)

Mit dem Befehl "ifconfig" können wir die aktuelle IP-Adresse herausfinden.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/f2564de8-06b3-49ad-8511-3235d6f70814)

Danach tragen wir eine statische IP-Adresse im IP-Range ein sowie den DNS-Server von Google (8.8.8.8).

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/efda2cd0-e044-43e4-8851-464cd7bd9c2d)

Nun kann man  das Terminal öffnen.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/4a81e710-0b6d-4004-91e8-7de90d8ba3a9)

Danach kann man die Installation von Nextcloud mit "sudo snap install nextcloud" starten. Dies erfordert das Passwort von einem Admin (alpha).

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/38458dda-86c3-450e-9751-dbf3a38a657f)
![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/03723eef-b741-4375-92ae-cb6101343ef5)

Zus

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/183c322d-b787-486a-95b6-02f5369c7ada)

Anschliessend überprüfen wir mit dem Befehl "sudo nextcloud.occ config:system:get trusted_domains" von wo aus eine Verbindung möglich ist.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/86505973-3a4a-4bef-a743-b8b2b436639d)

Hier fügen wir dann eine neue Verbindung hinzu und überprüfen diese am Schluss wieder mit "sudo nextcloud.occ config:system:get trusted_domains".

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/1379eff9-88f6-4863-968f-6465c1888759)

Im Anschluss richten wir ein SSL-Zertifikat mit "sudo nextcloud.enable-https self-signed" ein.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/d68a6567-a937-4fdc-b9be-c137ae7bc229)

Damit nun die Verbindungen möglich sind, müssen wir die TCP-Ports 80 & 443 auf der Firewall erlauben. Dazu nutzen wir den Befehl "sudo ufw allow 80,443/tcp".

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/206bf00d-a09f-4dd1-8aab-f7c8285a2003)

### Anmeldung auf Windows

Nun haben wir Nextcloud eingerichtet. Jetzt können wir dies auf dem Windows-Client ausprobieren. Dazu öffnen wir einen Browser und gibt die IP-Adresse vom Linux-Client ein. In unserem Beispiel https://192.168.0.5.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/fee2557b-d3d4-47a8-ae83-48074b1d6ecb)

Nun kann man sich mit dem Linux-User anmelden:

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/1dab9774-30d1-48f2-9e3a-d720a448d948)

Jetzt ist man angemeldet und 

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/9f4af6d3-8722-42e8-8c8e-fae916514436)


### Anmeldung auf Linux

Als Vorbereitung öffnet man das Terminal und führt den Befehl  "sudo nano /etc/hosts".

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/0239d633-f5c1-4966-bf42-200aecdac2a0)

Text

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/647e3756-26ad-4bcf-acd4-bcf1a58b399f)

Danach können wir den Speicher unter der obigen eingegebenen Adresse erreichen (nextcloud.kranic.com). Hier wird dann wieder das selbe Login benötig wie auf Windows.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/daa8b3e8-a4b5-45bb-9f4b-b34fe089eeb3)

Text

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/fdbd2118-2855-4a88-8367-ba072a80e949)
![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/1758419d-22f3-4907-98f0-753051e8952d)
![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/6325486d-3302-4818-a32e-0460812ff96a)



