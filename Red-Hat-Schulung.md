# Red Hat Schulung 
-- TOC


## Tag 1


### Was ist Linux, Red Hat und Rocky

TMux CSSH -> Tool um sich auf mehreren Maschinen gleichzeitig anzumelden.

### shelltux ###

`shelltux stautus --all` 
`shelltux start 8`

**TASK**

Shelltux mit Übung
- 9 `cd, ls -rtl`
- 10 `cd ../`
- 11 `find . -maxdepth 3`
- 13 `rm /PFad/*`
- 14 `rm struktur/v3/*[ABC]*`
- 16 `rm -Rv f`
- 19 `echo $HOSTNAME > Rechner`
- 27 `grep -n meist wiki2`
- 29 `grep -rni "gute nacht" (wie ergebnismenge zählen lassen) Lösung : | wc -l (Word Count)`
- 


- 20: 
   echo -e "Hallo, mein Name ist \e[35mRobin\e[0m \e[44mHeydkamp\e[0m und mein Benutzername ist \e[4mnutzer41\e[0m."
- 34 
- 


### Shell und Platzhalter

Beispiel: `$ echo 27*5`.
Die "SHELL" interpretiert den Befehl zuerst. Platzhalter werden also zuerst übersetzt und interpretiert. In dem Fall werden also 27*5 durch alle DATEINAMEN und ORDNER ersetzt die auf dieses "Pattern" passen. durch z.B. `\` werden Platzhalter "deaktiviert". 

`find /usr -name *.png`

Sucht durch alle Ordner /usr durch und gibt .pngs aus.
Wenn aber im aktuellen Ordner ein png vorhanden ist, ersetzt die Shell das Sternchen in dem Befehl durch diese Dateinamen. Es werden dann z.B. nur noch Dateien gefunden die den selben namen wie im aktuellen Ordner haben.

## Verzeichnisstruktur

| Ordner | Verwendung |
| -------- | ------- |
| /boot | Dateien zum Starten des Systemes |
| /dev | |
| /etc | Konfigrationsdateien |
| /home| Home Verzeichnisse der User |
| /media| Einhängepunkte für Wechseldatenträger |
| /mnt| temporäre Einhängepunkte für Dateisysteme |
| /opt|  |
| /proc| |
| /root| |
| /run|  |
| /root | Home vom Root User |
| /srv| Nutzdaten von Serverdiensten |
| /sys| Gerätedateien und Hardwareparameter |
| /tmp| temporäre Dateien die nacht dem neubooten wahrscheinlich gelöscht werden.|
| /usr | hier sollte wirklich nur die Paketverwalung rein - "unix static resources"|
| /usr/bin |grundlegende Befehle (für alle Benutzer) |
| /usr/lib | Libarys, Programm-Komponenten |
| /usr/lib/modules | |
| /usr/local/bin | Wie bin, aber nicht aus Paketverwaltung |
| /usr/local/sbin | |
| /usr/sbin | Systemverwaltungskommandos |
| /var|  |
| /var/log | Logdateien  |
| /var/tmp | temporäre Dateien die nicht nach einem neuboot gelöscht werden.x |


Dateitypen

Unter Windows kennen wir Dateiendungen, z.b. .pdf, .txt usw. 
Unter Linux (wo "alles" eine Datei ist) sind damit andere Typen gemeint:

| Zeichen | Bezeichnung |
| --------| --------|
| - | regular file |
| d | directory |
| c | character device |
| b | block device |
| l | symlink |
| s | Sockets |
| p | named pipes |


| Befehl / Datei | Funktion |
| --------| --------|
| getent passwd | User auflisten |
| getent group | Gruppen auflisten |
| /etc/passwd | User |
| /etc/shadow | Passwörter |
| /etc/group | Gruppen |
| /etc/gshadow | Gruppenpasswörter |
| /etc/nsswitch.conf | Quellen für Namensdatenbanken |

### Benutzerverwaltung

2 Ordner
2 Dateien erstellen

ALLE Rechte löschen

- mv file 2 dir1
- mv file1 dir 1

mv:
`dir1` braucht w damit wir in dem Verzeichniss schreiben dürfen und X damit wir in das Verzeichniss wechseln dürfen.

cp: `file1` braucht READ damit wir wissen was wir schreiben sollen.

ALLE zum löschen von Ordner

### Benutzer & Gruppen anlegen

1. Alle Gruppen anlegen
    `for g in ops pr rnd fpo controlling intern bar; do groupadd $g; done`
2. Alle User anlegen, so dass..
     - das Homeverzeichnis in /home liegt
     - der User eine eigene, private Gruppe
     - der User Mitglied in den Gruppen seiner Abteilung/en= ist
    `useradd -d /home/robert -m -U -G pr,ops robert`

    -d = Wo soll das Home-Verzeichniss angelegt werden
    -m = es SOLL ein Home-Ordner angelegt werden 
    -U = User soll eine User-Gruppe erhalten
    -G = Benutzer soll folgenden Gruppen zugewiesen werden




### ACL

`setfacl` & `getfacl`
- Der Gruppe Controlling lesezugriff auf alle Ornder geben:
`setfacl -R -m g:controlling:rX *`
- Default ACLs einstellen: `setfacl -d -m u::rwX -m g::rwX -m o::- -m g:controlling:rX -R *`

sssd wenn Linux User an ein Windows Benutzerverwaltung hinterlegt werden sollen. 
samba wenn Windows User an eine Linux Benutzerverwaltung hinterlegt werden sollen.

userdbctl
yum -> dnf -> 

### Dateiattribute

`chattr` & `lsattr` 

Attribute für Dateien vergeben. Spezielle attribute können z.B. eine Datei unveränderlich (i = immutable) machen.
Inhalt, Name, Metadaten selbst Berechtigungen lassen sich dann z.b. nicht mehr ändern.


### DNF und Paketmanager

dnf search thunderbird
dnf info thunderbird

Beim dnf install thunderbird:
Metadaten validierung
Paket, Architektur, Version, Quelle, Größe,

Größe, Installationsgröße


Download, Validierung, Ausführung, Summary:

### Third Party Repo einbinden:

Installiert Postgresql 18.

```
# Install the repository RPM:
sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-10-x86_64/pgdg-redhat-repo-latest.noarch.rpm

# Install PostgreSQL:
sudo dnf install -y postgresql18-server
```


in dem Repo haben wir
repomd.xml -> Liste mit SHA Keys der Dateien
repomd.xml.asc -> Public-Key des Repositorys mit dem die Dateien Prüfsummen ausgerechnet werden können.

Metadaten-Datei vertrauen weil Public Key
Public Key vertrauen weil HTTPS-Verbindung
HTTPS Vertrauen wegen Zertifikat
Zertifikat vertrauen wegen CA-Stelle
CA-Stelle vertrauen wegen RedHat Key


| Befehl | Funktion |
| --------| --------|
|rpm -qi postgresql18-server | Infos über installiertes Paket |
|rpm -ql postgresql18-server | Dateien aus Paket auflisten |
|rpm -qf /usr/pgsql-18/share/tsearch_data/italian.stop | Paket zu Datei finden |



csr Certificat Signing Request


CA Stelle hat private Key
Damit wird MEIN CSR zu einem Certificat

In dem Zertifikat steht dann mein (Der des Servers) public Key und die Verschlüsselung durch den privat-Key des CA. Der CA private Key kann dann nur mit dem Public Key entschlüsselt werden, welcher schon auf meinem Rechner ist, 

Bei Self-Signed bauen wir uns selbst ein CA.

CA erstellen dann 2 Keys. Also 2 Public und 2 Private keys. Einmal ein root-ca und ein Intermediate CA. Das Intermediate CA basiert dann auf dem root ca und kann im zweifel ausgetauscht werden. Der Public Key vom Intermediate cA kann dann verwendet werden um meine Server-Public-Keys zu zertifizieren.

self-Signed Certs sind dann einfach mit sich selbst Zertifiziert. Bei Signieren von Zertifikaten wird solange verifiziert bis 



Nutzt ihr selbst signierte Zertifikate, müsst ihr selbst das Zertifikat signieren und dies an die Clients ausspielen.
Dadurch das es von sich selbst signiert ist, wird es nicht von "höhere Stelle" valiidert und gilt quasi als Gültig.


`dig techkids.org caa`
ANSWER SECTION: 
    CAA -> "letsencrypt.org" 

Wir können im DNS eingeben welchen Zertifikaten wir vertrauen wollen. Also die CA-Stelle angeben von wo das Zertifikat stammen darf.


### Container

- `podman run -it bash`
- `podman run -d --name hello-httpd -p 8888:80 -v '/srv/podman/httpd/htdocs:/usr/local/apache2/htdocs' httpd:2.4`
- `podman run -d --name httpd_8001 -p 8888:8001 -v '/srv/podman/httpd/htdocs:/usr/local/apache2/htdocs/' -v '/srv/podman/httpd/httpd.conf:/usr/local/apache2/conf/httpd.conf' httpd:2.4`

`man podman-run` ergibt das -v für "volume" steht. 



https://vim-adventures.com/

## Storage
| Bezeichnung | Mount-Points |
| -------- | --------|

Lokaler Storage


- Magnetbänder
- SSDs
  - NVME    `/dev/nvme0`
  - SATA    `/dev/sda`
- Festplatten
  - SATA / SCSI `/dev/sda`
  - IDE         `/dev/hda`
- SD/MMD (USB-Sticks)
  - SCSI    `/dev/sda`
  - MMC     `/dev/mmc`
- CD/DVD
  - SCSI    `/dev/sr0`
  - IDE     `/dev/hda`
- Floppy



Annahme: Ich habe einen komplett neuen Festplattenspecher (SSD) eingebaut. Was mache ich zuerst?

- Paritionieren!

```
GPT
GUID Partition Table
Globally Unique Identifiert Partition Table
Ist das selbe wie eine UUID.

* UUID ist die Linux Bezeichnung der GUID. *

Die UUID gibt die eindeutige Bezeichnung der Festplatten-Partition.
Das Dateisystem bekommt allerdings auch eine UUID. 


pvcreate /dev/sda4 
pvs
vgcreate vg_data /dev/sda4
vgs


- PV = Physical Volume = Quelle
- VG = Virtual Group  = Virtuelles Ziel
- LV = Logical Volume = Nutz-Nießer
```

### Kernel 

`systemctl list-dependencies` - Listet alle Boot-Relevanten "" auf.

**Unit-Types**
- service
  - oneshots
- target
  - War quasi früher mal das "Runlevel"
- path
- socket
  - 
- moint
- 
- swap
- timer

Rausfinden, ob auf einen Port gelauscht wird...
`lsof -Pni :9090`

- `/lib/systemd/*` und `/usr/lib/systemd/*`: (niedrigste Priorität) aus der Paketverwaltung, nicht anfassen.
- `/run/systemd/*`: dynamisch von systemd erzeugt
- `/etc/systemd/*`: (höchste Priorität) Hier dürfen sich Admins austoben

trap "echo nö, heute nicht' TERM
echo $$
kill -term XXXX


`sysctl -a` - Alle Kernel Einstellungen anzeigen.
Repository für zusätzlche Treiber und aktuellere Kernel:
    - `dnf install epel-release.noarch`
    - `dnf install elrepo-release.noarch`

### Netzwerk
[Wiki](https://wiki.lab.linuxhotel.de/doku.php/admin_grundlagen:netzwerk#netzwerk_temporaer_einrichten)

Was brauche ich für ein "Netzwerk".
### Layer 1 / Betriebssystem
  - Treiber
  - Netzwerkkarte
  - Device (`pgre -la udev` - der UDEV-Deamon schaut nach neuer Hardware, bzw. neuen Devices)

#### Zugehörige Befehle:
- `ip link`
- `dmesg`
- `ethtool`
- `modinfo`
- `modprobe`
- `udevadm`
------

### Layer 2 / Ethernet, Wify, PPP
  - MACAdresse
  - Switch
  - Geschwindigkeit

#### Zugehörige Befehle:
- `ip -s link`
- `ethtool`
------

### Layer 3 / IPv6 / IPv4
  - IP-Adress
  - Router
  - Subnetz

#### Zugehörige Befehle:
- `ip -- br a s`
- `ip route`
- `ip address`
- `ip neighbor`

------

### Layer 4 / TCP - UPD
  - Port

#### Zugehörige Befehle:
- `ss -tuapn`
- `lsof -Pni`
- `nc -l 5000` - Nur zum LAUSCHEN, Pakete werden nicht weitergeleitet. 
- `strace` eignet sich eher zum "debuggen"
- `ping`


- `ls /etc/udev/rules.d/`
- `vim /etc/udev/rules.d/70-net.rules`
- `ACTION=="add", SUBSYSTEM=="net", KERNEL=="dummy0", NAME="intern0"`
- `modprobe -r dummy`
- `modprobe dummy numdummies=1`

Treiber rausfinden und alternative Treiber suchen bzw. installieren

`udevadm info -a /sys/class/net/wlp2s0`  (wlp2s0 ist in diesem Fall die WlanKarte)
- unter "DRIVERS" steht dann der Wert des installierten Treibers.
- Alternativ `ethtool -i wlp2s0` 
- `modinfo iwlwifi` - Zeigt uns verschiedene Firemwares an. Auch Alternativen. diese können z.B. mit 
- `dnf provides */iwlwifi-5000-5*`

---

net.ipv4.conf.all.forwarding
net.ipv4.ip_forward=1

### DNS

die Reihenfolge, wie DNS aufgelöst wird wird in der Datei "/etc/nsswitch.conf" definiert unter dem Parameter "hosts"
`grep hosts /etc/nsswitch.conf` -> hosts: files dns myhostname

- files werden z.B. die host-Datei sei (`/etc/hosts`).
- Der DNS ist in der `/etc/resolv.conf` definiert.
- myhostname ist quasi immer die "eigene"-IP Adresse, somit verscuht er sich notfalls selbst als DNS-Server zu verwenden.

- `getent hosts www.golem.de` - ist eine bessere Abfrage auf die IP-Adresse.