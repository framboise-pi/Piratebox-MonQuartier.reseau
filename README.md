# Piratebox-social

Après un essai de PirateBox, la décision est prise de fabriquer une box social qui corresponde à ce que j'ai en tête.

Peut être comme vous ?
Mettez une étoile et ce projet ira plus vite !


# L'idée
Complètement dans le sens de le PrateBox, mais tourné uniquement autour du Raspberry (3B utilisé pour ce projet)
Autour d'un serveur web et de Bootstrap, proposer quelque chose d'intéressant pour le quartier en terme d'échange 'local' !
Avec ce petit 'plus' de permettre aux artisans et commercants de faire leurs pubs par exemple.

# MonQuartier.reseau ?
SSID : "MonQuartier.reseau GRATUIT"

# Base
Après un tour d'horizon, le candidat pour monter un Hotspot semble être RaspAp.

- DNS
- DHCP
- MariaDB
- PHP
- mémoire externe
- Bootstrap (veiller à n'utiliser aucune dependance online) et vérifier si tentatives accès des .js ou autre (resolution dns)

# FRONTEND WAN

- Chat (mysql -> sécuriser) simple. si ajout -password au pseudo -> couleur .css admin
- Actualités (blog anonyme avec éditeur WYSIWYG) ENVOI - ok pour URL, image mais restrictions .jpg .png (voir pour permettre envoi image)
  - tinyMCE ? à voir cette histoire d upload
- Collection d'ebooks ENVOI .pdf
- Vidéos ENVOI .mov .mp4 .avi
- Audios ENVOI .mp3 .ogg
- Rassembler les envois sur un seul formulaire -> Tri des extensions fichiers vers les dossiers qui vont bien
- 'Searchbar' -> noms des fichiers. contenu blogs (titre et texte)
- Streaming pour dossier /Videos et /Audios

- OPTION portail accès internet (avec ratio et/ou autre). login/mdp.

# BACKEND accessible seulement sur le LAN
- connectés/log
- état mémoire etc info system
- vue du chat et purge

# FIREWALL.IPTABLE

# Pas d'accès internet
ou éventuellement proposer, sous forme de 'Portal' un accès internet avec login/mdp.
Exemple : un commerce qui n'a pas un accès internet rapide comme la fibre optique, mais un abonnement internet data via son téléphone (à noter que les abonnements data mettent des restrictions sur les ports, donc certains sites sont inaccessibles...)

# Sécurité

# Header/Présentation

Merci de poster les flyers des commercants du quartier que vous recommandez !
Aucun responsabilité sur le contenu envoyé sur ce réseau intranet.
Aucune modération, sauf exception, des fichiers et autres par l'administrateur.
Ne pas envoyer d'informations personnelles ou qui pourraient vous porter atteinte entre de mauvaises mains.

# Ne pas faire apparaître les informations
- garder l'anonymat du messager, de la personne/appareil qui envoies les données.

# Pour qui ? - ajouter exemples

Pour les
- Artistes
- Commerces
- Cours/écoles/prof

# Points
- automatisation du tri/renommage
- essais de portée avec un scanner Wifi mobile (WIFI intégré et dongle USB déporté)
- filtrer les insultes et envoyer alarme ? Anonymat de veut pas dire manque de respect. MACban à prévoir sur multiples.
- wiki sur comment envoyer etc ?
- 
