# Nextcloud-on-Linux

### Einleitung:

Willkommen zu unserem Schulprojekt im Modul 239 (Internetserver in Betrieb nehmen), in dem wir eine Nextcloud-Umgebung in Linux aufbauen! Das Projekt wird mit Robin Kraft und Samuel Nick durchgeführt. Nextcloud ist eine beliebte Cloud-Speicherlösung, die uns ermöglicht, Dateien sicher auszutauschen und zu speichern. In diesem Projekt werden wir unsere Linux-Kenntnisse erweitern, indem wir eine Nextcloud-Instanz aufsetzen und konfigurieren. Dabei lernen wir wichtige Aspekte wie die Auswahl der Linux-Distribution, die Installation von Webservern und Datenbanken sowie die Benutzerverwaltung und das Datei-Sharing. 

### Was wird alles benötigt?

- 2x Ubuntu Clients (ubuntu-22.04.2 - grafische Oberfläche)
- Windows Client


### Unser Vorgehen:


#### Konfiguration Netzwerk:

Vorrausgesetzt sind alle oben aufgeführten Clients komplett installiert und im selben Netz.

Als erstes führt man den Befehl "sudo apt-get update" aus, um sicherzustellen das die neusten Updates installiert werden.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/3477f769-fdb8-40dd-a8b0-5b0c6958379b)

Mit dem Befehl "ifconfig" können wir die aktuelle IP-Adresse herausfinden.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/f2564de8-06b3-49ad-8511-3235d6f70814)

Danach tragen wir eine statische IP-Adresse im IP-Range ein sowie den DNS-Server von Google (8.8.8.8).

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/efda2cd0-e044-43e4-8851-464cd7bd9c2d)

#### Installation NextCloud:

Nun kann man  das Terminal öffnen.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/4a81e710-0b6d-4004-91e8-7de90d8ba3a9)

Danach kann man die Installation von Nextcloud mit "sudo snap install nextcloud" starten. Dies erfordert das Passwort von einem Admin (alpha).

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/38458dda-86c3-450e-9751-dbf3a38a657f)
![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/03723eef-b741-4375-92ae-cb6101343ef5)

Es gibt verschiedene Möglichkeiten, wie man den Nextcloud-Snap konfigurieren kann. In dieser Anleitung werden wir jedoch keinen Administrator-Benutzer über die Web-Oberfläche erstellen, sondern dies über die Befehlszeile tun, um ein kleines Zeitfenster zu vermeiden, in dem die Administrationsseite für jeden zugänglich wäre, der die IP-Adresse oder den Domainnamen deines Servers besucht. 

Um Nextcloud mit einem neuen Administrator-Account zu konfigurieren, verwende den Befehl "nextcloud.manual-install". Du musst Benutzernamen und Passwort als Argumente übergeben. Nun wird mit dem Befehl sudo nextcloud.manualinstall "user" "password"

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/183c322d-b787-486a-95b6-02f5369c7ada)

#### Whitelisten von Domains oder IP-Adressen:

Anschliessend überprüfen wir mit dem Befehl "sudo nextcloud.occ config:system:get trusted_domains" von wo aus eine Verbindung möglich ist.
In unserem Fall wäre das der localhost.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/86505973-3a4a-4bef-a743-b8b2b436639d)

Hier fügen wir dann eine neue Verbindung hinzu und überprüfen diese am Schluss wieder mit "sudo nextcloud.occ config:system:get trusted_domains".

Wir fügen den folgenden IP-Range 192.168.0.* hinzu, damit alle Computer in diesem Range zugreifen können. Ebenfalls definieren wir eine Domain, damit der Ubuntu-Client über den Domainnamen zugreifen kann. (nextcloud.kranic.com)

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/1379eff9-88f6-4863-968f-6465c1888759)

#### Zertifikat einrichten:

Im Anschluss richten wir ein SSL-Zertifikat mit "sudo nextcloud.enable-https self-signed" ein.

Da es kein verifiziertes Zertifikat ist, werden wir eine Zertifaktsmeldung erhalten, wenn wir auf Nextcloud zugreifen möchten. Dies kann jedoch ignoriert werden. 

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/d68a6567-a937-4fdc-b9be-c137ae7bc229)

Damit nun die Verbindungen möglich sind, müssen wir die TCP-Ports 80 & 443 auf der Firewall erlauben. Dazu nutzen wir den Befehl "sudo ufw allow 80,443/tcp".

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/206bf00d-a09f-4dd1-8aab-f7c8285a2003)

### Anmeldung auf Windows:

Nun haben wir Nextcloud eingerichtet. Jetzt können wir dies auf dem Windows-Client ausprobieren. Dazu öffnen wir einen Browser und gibt die IP-Adresse vom Linux-Client ein. In unserem Beispiel https://192.168.0.5.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/fee2557b-d3d4-47a8-ae83-48074b1d6ecb)

Nun kann man sich mit dem erstellten User (alpha) anmelden:

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/1dab9774-30d1-48f2-9e3a-d720a448d948)

Jetzt ist man angemeldet und kann seine Daten hochladen und verfügbar machen. 

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/9f4af6d3-8722-42e8-8c8e-fae916514436)


### Anmeldung auf Linux:

#### Freiwillig: Zugriff über Domainnamen:

Das Terminal öffnen und den Befehl sudo nano /etc/hosts eingeben, um das Hostfile zu bearbeiten.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/0239d633-f5c1-4966-bf42-200aecdac2a0)

An dieser Stelle fügen wir die IP-Adresse des Nextcloud-Servers ein und den gewünschten Domänennamen. Es muss jedoch beachtet werden, dass der Zugriff nur erlaubt wird, wenn die sich die Domain auf der Whitelist befindet. In unserem Fall wäre das die Domäne: nextcloud.kranic.com

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/184deca7-c582-44b8-9a7d-03486e4e1679)


Danach können wir den Speicher unter der obigen eingegebenen Adresse erreichen (nextcloud.kranic.com). Hier wird dann wieder das selbe Login benötigt wie auf Windows.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/daa8b3e8-a4b5-45bb-9f4b-b34fe089eeb3)

Wie Sie sehen können, haben wir die gleiche Benutzeroberfläche wie auf Windows.

![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/fdbd2118-2855-4a88-8367-ba072a80e949)

### Test:
Wir laden nun eine Datei vom Windows Client auf unseeren NextCloud Speicher und möchten schauen, ob dieser ebenfalls im Linux System verfügbar ist. In unserem Fall ist es das Bild Testbild.jpg

#### Windows:
![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/1758419d-22f3-4907-98f0-753051e8952d)

#### Linux:
![image](https://github.com/samuelnickk/Nextcloud-on-Linux/assets/132668785/6325486d-3302-4818-a32e-0460812ff96a)
