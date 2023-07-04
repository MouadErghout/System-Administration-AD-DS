# System-Administration-AD-DS

https://drive.google.com/file/d/1DC5J3Y7ww-mBvTlUmLxZmovtfjMkII1e/view?usp=sharing

Deployer l’AD sur windows server

1) il faut d’abord installer Windows Server 2012 R2
-Il faut l’affecter une adresse IP Statique
2) installer le DC a l’aide du AD DS:
Sur le 2012 R2:
- Menu Demarrer > Outils d’administration > Gestionnaire de serveur >
ajouter des roles et des finctionnalités
- Installation basée sur un rôle ou une fonctionnalité
- Selectionner un serveur de pool de serveurs
- Cocher service AD DS, et ajouter la fonctionnalité
- Promouvoir le serveur en contrôleur de domaine
- Ajouter une nouvelle forét, et donner le nom du domaine racine
- Installer le serveur DNS
3) Ajouter une machine au domaine
Sur le serveur :
- Il faut créer un utilisateur dans une OU
Sur la machine cliente
- Menu Demarrer > ordinateur>proprietés > parametres systeme avacé
- Changer le nom du domaine auquel on veut l’ajouter
- Se connecter avec le compte créer par le serveur

Strategies de mot de passe :
En utilisant le centre d’administration d’AD:
- Passer en mode arborescence et accédez au dossier système
- Choisir Password Settings Container
- Créer nouveau paramétre de mot de passe
- Une GUI s’apparaisse pour choisir les differents proprieté du PSO
- Appliquer la PSO sur un ou plusieurs groupes

Les profils :
1) créer un profil utilisateur itinérant :
C’est un profile créer par l’administrateur systéme puis stocké sur un serveur.
Tt maj est stocké sur le serveur
- Créer un dossier partagé sur le serveur qui va contenir toutes les profiles, et
donner au toutes les utilisateur le controle total sur ce derniere
- Atteigner l’objet utilisateur de la personne sur Utilisateurs et ordinateur de
l’AD
- Dans les proprietés de l’utilisateur, definir le chemin du profil à ce du
dossier partagé deja créer et ajouter un repertoire portant le nom
d’utilisateur
2) créer un profil d’utilisateur obligatoire :
C’est un profile intinérant utilisé pour spécifier des paramétres particuliers pour des
utilisateurs, seuls les admins peuvent modifier ces profils, tt modification par
l’utilisateur sera supprimer apres un redemarage.
- Ouvrir les prorietés d’un utilisateur et definir le chemin d’accés au fichier
partagé en terminant par l’extension .man
Configurer DHCP :
If fault possedé un controleur du domaine et un serveur DNS
- Assurer que le serveur posséde une IP fixe
- Ajouter le rôle DHCP sur l’AD
- Indiquer le domaine DNS
- Configurer l’etendue DHCP c a d la plage d’@ IP et les options DHCP
données aux clients
Configurer WDS :
C’est pour l’installation des OS via réseau
Il faut avoir un serveur DHCP configuré sur le serveur
- Installer le role WDS à partir du PowerShell ou l’interface de l’AD
- Copier le fichier ISO d’OS epecefique à n’impore quel emplacement sur le
serveur

- Ouvrir le WDS et selectionner l’option à integrer à AD ensuite choisir les
options convenable à l’environement
- Ajouter le fichier d’image d’installation (install.wim)
- Ajouter l’image de demarrage (boot.wim)
- Comme le serveur DHCP est deja mis en place, on peut demarrer les
machine clients directement sur le serveur PXE/WDS

Configurer la GPO :
C’est pour installer une application sur un client via le reseau
- Stocker l’application sur un partage reseau qui soit accessible au utilisateurs
- Aller sur l’OU ou l’utilisateur que vous voulez installer l’application exist
- Créer un Objet GPO dans ce domaine
- Fair modifier la GPO pour créer un nouveau package
- Idniquer l’emplacement de l’executable (.msi,.exe...)
- Dans des cas il faut executer la commande gpupdate //force sur le client
pour avoir la GPO
