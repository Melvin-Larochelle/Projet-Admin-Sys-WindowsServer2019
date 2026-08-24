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

!Création-d'un-compte-Utilisateur](../Images/Gestion-Objet-AD/Creation-compte-utilisateur.png)

Saisissez un "Prénom" et un "Nom" cela remplira automatiquement la champ "Nom Complet".

Remplissez le champ "Nom d'ouverture de session de l'utilisateur".

Saisissez ensuite son mot de passe.

Vous pouvez ensuite sélectionner les options de votre choix
