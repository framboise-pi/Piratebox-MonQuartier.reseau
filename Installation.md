# Info
Je travail avec des versions Desktop de Raspbian, l'installation est faite en ce sens : Raspbian Desktop + VNC

# 1. Installation d'une Raspbian fraiche
rien de particulier (Etcher + .img + microSD)

# 2. Installation de RaspAp
wiki : https://github.com/billz/raspap-webgui/wiki/FAQs

<code>sudo wget -q https://git.io/voEUQ -O /tmp/raspap && bash /tmp/raspap</code>

<br>sudo apt-get install lighttpd git hostapd dnsmasq iptables-persistent vnstat qrencode php7.3-cgi

Enable PHP for lighttpd and restart it for the settings to take effect.

sudo lighttpd-enable-mod fastcgi-php    
sudo service lighttpd force-reload
sudo systemctl restart lighttpd.service


pour un serveur HTTPS : 
<code>curl -sL https://install.raspap.com | bash -s -- --cert</code>
<br>Open a browser and enter the address: http://raspberrypi.local/rootCA.pem (this URL may be your IP address or a different hostname, depending on your unique setup). Download the root certificate
<br>
<br>Copy your CA to dir /usr/local/share/ca-certificates/
<br>Use command: sudo cp foo.crt /usr/local/share/ca-certificates/foo.crt.
<br>Update the CA store: sudo update-ca-certificates.

<br><code>httponly : yes</code>
<br><code>php Opcache : Yes</code>

# 3. Connexion au Wifi : SSID
<br><code>SSID : raspi-webgui</code>
<br><code>mot de passe : ChangeMe</code>

# 4. Backend
- déplacer tout les fichiers du répertoire www/html/ vers www/html/raspap
<br>nous utiliserons un .htaccess pour restreindre l'accès à ce dossier, et donc au backend de RaspAp à une IP ou plusieurs du LAN et non du WAN
<br>
<br><code>http://10.3.141.1/raspap</code>
<br><code>login:admin</code>
<br><code>password:secret</code>

# 5.
<br>If you have trouble getting the hostapd service to start, add the following to /etc/rc.local just before exit 0:
<br>service hostapd stop
<br>sleep 5
<br>service hostapd start

# 6.DNS
<br>utilisation de dnsmasq
<br>sudo nano /etc/dnsmasq.conf
<br>address=/#/IP_WIFI_RASPAP
<br>domain-needed
<br>bogus-priv
<br>no-resolv
<br>cache-size=1000
<br>
<br>sudo systemctl restart dnsmasq

# A.LIGHTTPD
 Ce serveur web est installé automatiquement avec RaspAp. Pas besoin d'Apache sur ce coup.

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

- créer base de données 'monquartier'
-- créer table 'chat' à 4 colonnes

-- ID (type INT  ) auto_increment « Primaire »
-- DATE (type DATE)
-- PSEUDO (type VARCHAR 255 )
-- MSG (type TEXT)
???? -- MAC (type VARCHAR 255) à voir si besoin de Ban ????

# A.1. chat.php

<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Chat</title>
    </head>
    <style>
    form
    {
        text-align:center;
    }
    </style>
    <body>
    
    <?php
    if $_POST['pseudo']
     {
      $pseudo=$_POST['pseudo'];
      
     }
     else
     $pseudo="pseudo";
    ?>
    
    <form action="chat_post.php" method="post">
        <p>
        <label for="pseudo">Pseudo</label> : <input type="text" name="<?php echo $pseudo ?>" id="pseudo" /><br />
        <label for="message">Message</label> :  <input type="text" name="message" id="message" /><br />

        <input type="submit" value="Envoyer" />
	</p>
    </form>

<?php
// Connexion à la base de données
try
{
	$bdd = new PDO('mysql:host=localhost;dbname=chat;charset=utf8', 'root', 'motdepasse');
}
catch(Exception $e)
{
        die('Erreur : '.$e->getMessage());
}

// les 10 derniers messages
$reponse = $bdd->query('SELECT PSEUDO, message FROM chat ORDER BY ID DESC LIMIT 0, 10');

while ($donnees = $reponse->fetch())
{
	echo '<p><strong>' . htmlspecialchars($donnees['PSEUDO']) . '</strong> : ' . htmlspecialchars($donnees['MSG']) . '</p>';
}

$reponse->closeCursor();

?>
    </body>
</html>

# A.2
chat_post.php

<?php
// Connexion à la base de données
try
{
	$bdd = new PDO('mysql:host=localhost;dbname=chat;charset=utf8', 'root', 'motdepasse');
}
catch(Exception $e)
{
        die('Erreur : '.$e->getMessage());
}

// Insertion du message
$req = $bdd->prepare('INSERT INTO chat (PSEUDO, MSG) VALUES(?, ?)');
$req->execute(array($_POST['pseudo'], $_POST['message']));

header('Location: chat.php?pseudo=$_POST['pseudo']');
?>


# Désactiver dnsmasq
<br>sudo systemctl stop dnsmasq
<br>sudo systemctl restart dnsmasq

fichier /etc/resolv.conf
 fichier /etc/hosts
 

