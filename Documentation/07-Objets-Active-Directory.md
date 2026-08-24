# **Le compte utilisateur**

Active Directory contient différents types d’objets, dont le compte utilisateur. Généralement rattaché à une personne 
physique, ce type d’objet permet d’être authentifié par un contrôleur de domaine. L’utilisateur doit pour cela saisir un 
login et mot de passe afin de prouver son identité. 

Ainsi, si la saisie de l’utilisateur est valide l’authentification est réussie, un jeton est attribué à la personne, qui 
contient notamment le SID (Security IDentifier) du compte utilisateur, unique dans le domaine AD, ainsi que l’ensemble 
des SID des groupes dont il est membre. 

Les comptes utilisateur peuvent être locaux à un poste de travail ou un serveur (ils sont dans ce cas stockés dans 
une base SAM  Security Account Manager) ou de domaine (stockés dans Active Directory). 

Pour crée un compte utilisateur, il suffit de lancer la console "Utilisateurs et ordinateurs Active Directory" et de faire un clic droit sur le dossier système Users puis, dans le menu contextuel, de sélectionnez Nouveau - Utilisateur

![Création-d'un-compte-Utilisateur](../Images/Gestion-Objet-AD/Creation-compte-utilisateur.png)

Saisissez un "Prénom" et un "Nom" cela remplira automatiquement la champ "Nom Complet".

Remplissez le champ "Nom d'ouverture de session de l'utilisateur".

Saisissez ensuite son mot de passe.

Vous pouvez ensuite sélectionner les options de votre choix

Après l’étape de création de l’utilisateur, il convient de paramétrer ses propriétés.

Effectuez un clic droit sur l’utilisateur Jean BAK puis sélectionnez Propriétés.

Certains onglets nécessitent l’affichage des fonctionnalités avancées. Dans la console Utilisateurs et ordinateurs 
Active Directory, cliquez sur le menu Affichage puis sur Fonctionnalités avancées. 
Seuls les onglets et propriétés les plus utilisés sont détaillés ci dessous. 

L’onglet Général reprend les informations saisies lors de la création de l’objet. Il est possible de les compléter en 
saisissant la page web, le numéro de téléphone… 

L’onglet Compte permet de modifier le nom d’utilisateur mais également les différentes options de compte telles que : 
- l’utilisateur doit changer le mot de passe, 
- le mot de passe n’expire jamais. 

Il est également possible de choisir une date d’expiration pour le compte (très utile pour des personnes en CDD ou 
des stagiaires) ; lorsque la date est passée, le compte est automatiquement désactivé. 

Le déverrouillage du compte peut également être effectué suite à un nombre de tentatives de connexion 
infructueuses égal à celui configuré dans la stratégie de mot de passe. 

Enfin, la configuration des horaires d’accès, qui permet d’autoriser l’ouverture de session sur le domaine dans une 
fourchette de temps (par exemple, 9h  18h), et la limitation des postes sur lesquels l’utilisateur a le droit de se 
connecter sont également deux propriétés configurables dans cet onglet. 

L’onglet Profil permet de configurer le chemin du profil de l’utilisateur. Lors de l’ouverture de session, le système 
d’exploitation vient récupérer le profil stocké dans le partage réseau. Par la suite, il est copié sur le poste sur lequel 
l’utilisateur a ouvert une session. Les modifications sont copiées dans le profil stocké sur le serveur lors de la 
fermeture de session. Le champ Script d’ouverture de session permet l’exécution d’un script lors d’une ouverture 
de session sur un poste de travail ou un serveur. Il est possible de réaliser la même opération lorsqu’un poste 
démarre ou s’arrête. Dans ce cas, l’exécution du script doit être configurée par une stratégie de groupe. 

L'onglet Éditeur d’attributs permet la visualisation et/ou la modification des attributs LDAP de l’objet.

Les fonctionnalités avancées doivent être activées pour accéder à cet onglet. 
- L’onglet Membre de permet de visualiser les groupes dont l’objet est membre. Il est de même possible d’ajouter de 
nouveaux groupes.
- L’onglet Réplication de mot de passe est utilisé avec un serveur RODC (Read Only Domain Controller), il permet de 
s’assurer que le mot de passe du compte utilisateur a bien été mis en cache sur le serveur en lecture seule. Et ainsi 
permettre à l’utilisateur de se connecter même en cas de coupure de la ligne Wan. Par défaut, la fonctionnalité de 
mise en cache est désactivée. 
- L’onglet Objet permet d’obtenir le nom canonique de l’objet. Ce dernier est composé du nom complet de l’objet 
précédé par son conteneur. Si ce dernier est enfant d’un autre conteneur, celui ci apparaîtra et ainsi de suite jusqu’à 
la racine du domaine. On peut également visualiser la classe de l’objet ainsi que les date et heure de création et 
dernière modification. Le nombre de séquences de mise à jour (Update Sequence Numbers  USNs), qui s’incrémente 
à chaque modification, est également présent. Enfin la protection contre la suppression accidentelle peut également 
être activée. Par défaut, cette fonctionnalité est désactivée. 
