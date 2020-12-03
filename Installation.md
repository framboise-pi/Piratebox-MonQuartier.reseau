# Info
Je travail avec des versions Desktop de Raspbian, l'installation est faite en ce sens : Raspbian Desktop + VNC

# 1. Installation d'une Raspbian fraiche
rien de particulier (Etcher + .img + microSD)

# 2. Installation de RaspAp
wiki : https://github.com/billz/raspap-webgui/wiki/FAQs

<code>sudo wget -q https://git.io/voEUQ -O /tmp/raspap && bash /tmp/raspap</code>

pour un serveur HTTPS : 
<code>sudo wget -q https://git.io/voEUQ -O /tmp/raspap && bash /tmp/raspap --cert</code>

<br><code>httponly : yes</code>
<br><code>php Opcache : Yes</code>

# 3. Connexion au Wifi : SSID
<br><code>SSID : raspi-webgui</code>
<br><code>mot de passe : ChangeMe</code>

# 4. Backend
<br><code>http://10.3.141.1</code>
<br><code>login:admin</code>
<br><code>password:secret</code>

# A. APACHE
<br><code>sudo apt install apache2</code></code>
<br><code>sudo chown -R pi:www-data /var/www/html/</code>
<br><code>sudo chmod -R 770 /var/www/html/</code>
<br>Apache utilise le répertoire /var/www/html comme racine pour votre site. Cela signifie que quand vous appelez votre Raspberry sur le port 80 (http), Apache cherche le fichier dans /var/www/html.

# B. PHP
<br><code>sudo apt install php php-mbstring</code>

# C. MARIADB
<br><code>sudo apt install mariadb-server php-mysql</code>

<br>connexion root
<br><code>sudo mysql --user=root</code>

- Supprimer l’ancien utilisateur root et en créer un nouveau :
<br>
<br><code>DROP USER 'root'@'localhost';</code>
<br><code>CREATE USER 'root'@'localhost' IDENTIFIED BY 'password';</code>
<br><code>GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;</code>

# D. PHPmyadmin
sudo apt install phpmyadmin
 choisissez no à la question concernant l’utilisation de dbconfig-common.
 sudo phpenmod mysqli
sudo /etc/init.d/apache2 restart
Si jamais vous avez une erreur, cela peut venir du fait que PHPMyAdmin se soit installé dans un autre dossier. Dans ce cas, essayez la commande

sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

# A. CHAT

<code>sudo apt update && sudo apt install snapd</code>
sudo snap install rocketchat-server

ss -ant

Ca doit renvoyer:
LISTEN 0 128   *:3000        *:*

Voilà il ne reste plus qu’à tester l’url de tchat dans votre navigateur:

https://IpRaspberry:3000

Il ne reste plus qu’à créer les utilisateurs, paramétrer un peu notre serveur puis installer un client sur notre téléphone ou pc.

pour gérer démarrage et arrêt du service;

service snap.rocketchat-server.rocketchat-server stop
 Create the first user, which will become the server's adminsitrator

https://docs.rocket.chat/guides/administrator-guides#administrator-guides





PirateBox Raspberry Pi DIY

PirateBox is an anonymous offline mobile file-sharing and communications system built with free software and inexpensive off-the-shelf hardware. You can use it to transform any space into a free and open offline communications and file sharing network. Learn more about PirateBox on our FAQ page!

We are providing a custom Raspberry Pi image, which is built on top of ArchLinux. You can learn more about it on our RapsberryPi Operating System Adjustments page. If you prefer building the PirateBox on Raspbian or Armbian you can find a manual setup page here. This is useful, if you want to use other one-chip computers, like the OrangePi. There are separate instructions available for: ChiPirate-BOX: the chipest and cheapest Pirate-BOX ever.

For support, be sure to check out the PirateBox Raspberry Pi page and the Raspberry Pi(rate)Box discussion board on our PirateBox Forum.

The following instructions are for installing PirateBox on a Raspberry Pi.
Stuff you will need

1. Raspberry Pi, learn about the different models. Pimoroni provides pretty nice sets including cases, psu and SDCards.

    Version A/B (Amazon)
    Version B+ (Amazon)
    Version Zero Pimoroni
    Version Zero-W (since 1.1.3) Pimoroni
    Version 2 (Amazon)
    Version 3 (Amazon) (Farnell) Pimoroni
    Version 3+ (Amazon) (Farnell) Pimoroni

Disclaimer: Buying this article through amazon.com gives as some affiliate money.

2. SD Card, Class 10 SDHC 8GB Card (Amazon)

3. USB Wi-Fi Adapter (compatible devices) - Note: RPi3 & Zero-W contains a built in wifi card.

4. 5V micro USB power supply (Amazon)

5. USB Flash Drive (single partition, FAT32 formatted) The Kingston DT 16GB works well (Amazon) (Newegg)

6. Ethernet cable (Amazon)

7. Computer with ethernet port - Note: Model A, RPi Zero and RPi Zero-W do not have an ethernet port.

8. 5V USB Battery (optional) (Amazon)
Using Monitor & Keyboard

All steps (setting alarm password, post installation steps) can be done via an attached keyboard and monitor. On early versions of the RaspberryPi you encountered USB power issues with a WiFi adapter attached, which is the reason the complete manual based on using SSH. In addition, it is teaching you how to use a remote shell. There is no GUI pre-installed on the PirateBox-archlinux images, so you will have a CLI as well, but in some cases it might be easier to use a keyboard & monitor then a network connection.
Installation

1. Using a BitTorrent client (Transmission for OS X and Linux) (Deluge for Windows, OS X or Linux) on your computer, download a copy of the

    For Raspberry Pi 1 A, B, B+, Zero & Zero-W : piratebox_rpi_1.1.4-27-02-2018.img.zip (SHA256 Checksum: 81635482b91c7464d24754615ea2e8c44be84f454dc0e8feaf1a4fa05753ca3c)
    <a href="magnet:?xt=urn:btih:ac3d307f5b777d6e36dfed1bb96ad2c29a0f55d5&dn=piratebox_rpi_1.1.4-27-02-2018.img.zip&tr=udp%3A%2F%2Ftracker.piratebox.cc%3A7070&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969"></a>    

For Rapsberry Pi 2 & 3, Rapsbperry Pi 3+: piratebox_rpi2_1.1.4-11-05-2018.img.zip (SHA256 Checksum: 2fc877040d4a46a0a5b229942c415a831ad16d7fea9ad6917448f76285280282).
<a href="magnet:?xt=urn:btih:ebeff1f5f1003f8c9147159355a783ea68b8d9c8&dn=piratebox_rpi2_1.1.4-11-05-2018.img.zip&tr=udp%3A%2F%2Ftracker.piratebox.cc%3A7070&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969"></a>

Note: Please help seed this file for other PirateBox downloaders!

Note: :!: If you encounter a slow starting of the torrent download using the magnet link, you may pick up the corresponding torrent file in this forum post. You can also use direct downloads via our Alternative download sources

Note: Our RPi images since 1.1.3 contain some customization which should treat the SDCard well. One of the consequences of these changes is, that you should shutdown the RPi properly. The Linux Kernel will write data on the disk on a 5 minute interval during being idle to preserve some SDCard cycles. You can learn more about it on our RapsberryPi Operating System Adjustments page.

2. Extract the piratebox_rpi*.zip file and follow the Raspberry Pi SD Card Setup instructions (OS X instructions) (Windows instructions) (Linux instructions) to install the image to your SD card.

3. Once you have finished copying the Raspberry Pi(rate)Box image to your SD card, insert it into the Raspberry Pi and connect it via ethernet cable to your home router. Be sure your USB Wi-Fi adapter and FAT32 formatted USB drive are both plugged in (see “Stuff You'll Need” section above for more info on compatible devices).

4. Wait 2-3 minutes for your Pi to fully boot and then open a terminal window (for OS X, go to Applications > Utilities > Terminal; for Windows, install and open PuTTY) and ssh into your PirateBox:

ssh alarm@alarmpi

The password is: alarm

Note: If you are using PuTTY, enter in the hostname field “alarm@alarmpi” or “alarm@192.168.77.1”

5. Once you have logged in, change your password (to something you'll remember!) by using the passwd command:

passwd 

You will be prompted to enter and then confirm your new password.

Root user is not allowed to login via remote, you do not need to set a password for root. Use sudo to invoke commands as root.

The default password for user root is root. It is strongly recommended to change this password as well. You can do this while being logged in as alarm running this command:

sudo passwd root

Note: At this point, the PirateBox AP should be available, if you have a supported WiFi stick attached. For problems see here this mod guide or post to the RPi forum mentioning the failed WiFi auto detection.

6. Optional: By default, the PirateBox stores the uploaded files into the root filesystem. This is sufficient for first tests, but for larger installations you should consider using a different partition or medium. The extracted image uses around 2GB of the SD Card, so you can use the remaining SD card storage, or your USB flash drive. This process is documented on the Raspberry Pi(rate)Box Mods page.

7. Your PirateBox ist started automatically as soon as a supported WiFi stick is detected.

8. You are now ready to activate the Kareha Image and Discussion Board, enable your USB drive as share and start the UPnP server. See the post-installation instructions below for details.
Post-Installation

Once you have installed or upgraded your PirateBox, follow these final steps to activate the Kareha Image and Discussion Board and configure and start the UPnP media server.

1. Power up your PirateBox (make sure it is not connected via ethernet cable) and join the SSID “PirateBox: Share freely” network. Open a terminal window (for OS X, go to Applications > Utilities > Terminal; for Windows, install and open PuTTY) and ssh into your PirateBox:

ssh alarm@192.168.77.1

2. Recommended: Activate the USB Stick (FAT32 only) sudo /opt/piratebox/rpi/bin/usb_share.sh or (since 1.1.3) the spare space on the SDCard as storage using the command sudo /opt/piratebox/rpi/bin/sdcard_share.sh.

3. Activate the Kareha Image and Discussion Board by using the board-autoconf tool:

sudo /opt/piratebox/bin/board-autoconf.sh

4. Activate the “timesave functionality” once:

 sudo /opt/piratebox/bin/timesave.sh /opt/piratebox/conf/piratebox.conf install
 sudo systemctl enable timesave 

5. Activate the UPnP Media Server by copying over the config file:

sudo cp /etc/minidlna.conf /etc/minidlna.conf.bkp
sudo cp /opt/piratebox/src/linux.example.minidlna.conf /etc/minidlna.conf

Note: Optionally, you can edit the config file (change the display name, etc) with:

sudo nano /etc/minidlna.conf

6. Finally, start the UPnP Media Server with:

sudo systemctl start minidlna
sudo systemctl enable minidlna

7. Your PirateBox should be ready to use! Be sure to also check out the Raspberry Pi(rate)Box discussion board on our PirateBox Forum.
