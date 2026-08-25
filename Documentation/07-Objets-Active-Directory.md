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
à chaque modification, est également présent.

Enfin la protection contre la suppression accidentelle peut également être activée. Par défaut, cette fonctionnalité est désactivée. 

Le jeton d'acces 
Lors de l’ouverture d’une session, Active Directory se charge de l’authentification des utilisateurs et ordinateurs. 
L’autorité de sécurité locale (LSA, Local Security Authority) traite les requêtes d’authentification effectuées, pour cela 
Kerberos v5 est utilisée. Le protocole NTLM / NTLMv2 peut également être utilisé. 
Après avoir authentifié un utilisateur, le contrôleur de domaine qui a effectué l’opération génère un jeton d’accès. Ce 
dernier contient le SID (Security Identifier) de l’utilisateur, ainsi que le SID des groupes dont l’utilisateur est membre. 
Lors de l’ajout dans un nouveau groupe (après la création du jeton), il est nécessaire de fermer puis rouvrir la 
session. Ceci permet d’effectuer une nouvelle fois l’étape de génération du jeton et de posséder le SID du nouveau 
groupe. Si la régénération n’est pas effectuée, l’utilisateur ne pourra pas accéder à la ressource partagée. 
Lors de la tentative d’accès à une ressource, les SID contenus dans le jeton de l’utilisateur sont comparés à ceux 
présents dans la DACL (Discretionary Access Control List). Si un SID est trouvé, l’utilisateur se voit accorder l’accès 
avec les droits configurés dans la liste de contrôle d’accès, sinon l’accès est refusé. 

Il est aussi possible de crée un utilisateur en PowerShell afin de l'automatisé. Cette rubrique sera expliqué dans le document "PowerShell"

# **Les groupes dans Active Directory**

Afin de faciliter l’administration, il est recommandé d’utiliser des groupes (comprenant des utilisateurs ou des 
ordinateurs). L’administration des accès à des ressources partagées au travers de groupes de sécurité est plus 
aisée. Une fois le groupe positionné, l’administration s’effectue depuis la console Utilisateurs et ordinateurs Active 
Directory et quasiment plus sur la ressource. Pour donner une autorisation, il suffit de rajouter l’utilisateur dans le 
groupe, pour lui ôter l’autorisation, il suffit d’enlever l’utilisateur du groupe.  

De plus, un groupe peut être positionné sur la liste de contrôle d’accès de plusieurs ressources. La création des 
groupes peut être réalisée de deux manières : 
- Par profil (un groupe Compta par exemple) ce qui permet de regrouper les personnes du service comptabilité. 
- Par ressources (Compta, IT…), ce qui permet de regrouper toutes les personnes souhaitant accéder à une ressource. 

Le nom du groupe doit, dans la mesure du possible, être le plus parlant possible. Prenons un exemple de 
nomenclature, cette dernière doit englober les composants suivants :  
- L’étendue, ce point est traité plus loin dans le chapitre (G pour globale, U pour universel ou DL pour domaine local).
- Le nom de la ressource (Compta, Fax, BALNicolas, RH…). 
- Le droit NTFS qui va être attribué au groupe (w pour écriture, m pour modifier, r pour lecture...). 

Ainsi, si le groupe se nomme G_Compta_w, on peut très vite en déduire que c’est un groupe global positionné sur le 
dossier partagé Compta et qui donne des droits d’écriture à ses membres.

Il existe dans Active Directory deux types de groupes : les groupes de sécurité et les groupes de distribution. 
Concernant le premier type, il consiste en une entité de sécurité et possède un SID. Il peut donc être positionné sur 
une liste de contrôle d’accès ou être utilisé comme groupe de diffusion par le serveur Exchange. Ce type de groupe 
possédant un SID, il est présent dans le jeton d’accès de l’utilisateur. Pour cette raison, il est conseillé, si le groupe 
est utilisé uniquement pour l’envoi de mail, de choisir un groupe de distribution. 

Ce dernier type de groupes est utilisé par les applications de messagerie comme groupe de diffusion. Ne possédant 
pas de SID, les groupes concernés ne peuvent pas être positionnés dans une liste de contrôle d’accès. Un mail 
envoyé à ce groupe est transféré à l’ensemble de ses membres. 

Un groupe peut contenir des utilisateurs, des ordinateurs ou d’autres groupes en fonction de son étendue. En effet, 
cette dernière a un impact sur les membres et sur la ressource sur laquelle il est positionné. Il existe quatre 
étendues de groupe : 

- Local : ce type de groupe se trouve dans la base locale (base SAM) de chaque machine ou serveur (à l’exception des 
contrôleurs de domaine qui n’en possèdent pas). Il peut contenir les utilisateurs ou les groupes locaux à la machine. 
Ces groupes locaux peuvent également contenir des objets Active Directory de type utilisateurs, ordinateurs ou 
groupes. Il est utilisé uniquement dans des ACL locales. 

Lors de la jonction au domaine d’une station de travail ou d’un serveur, les groupes admins du domaine et 
utilisateurs du domaine sont respectivement membres des groupes locaux Administrateurs et Utilisateurs de la 
machine.

- Domaine local : utilisé pour gérer les autorisations d’accès aux ressources du domaine, il peut compter comme 
membres des utilisateurs, ordinateurs ou groupes globaux et universels de la forêt. Les groupes de type domaine local 
membres de ce groupe doivent appartenir au même domaine. Ce type de groupe peut être positionné uniquement sur 
des ressources (répertoire partagé, imprimante,…) de son domaine.
- Globale : contrairement à l’étendue Domaine local, les groupes globaux peuvent contenir des utilisateurs, des 
ordinateurs ou d’autres groupes globaux du même domaine. Ils peuvent être positionnés sur n’importe quelle 
ressource de la forêt. 
- Universelle : les groupes universels peuvent contenir les utilisateurs, ordinateurs et groupes globaux et universels 
de n’importe quel domaine de la forêt. Il peut être membre d’un groupe de type Universelle ou Domaine local. Le 
groupe peut être positionné sur les ACL de toutes les ressources de la forêt. Il est préférable d’utiliser un nombre 
restreint de groupes universels. 

La stratégie de gestion des groupes (IGDLA) définie par Microsoft permet de comprendre le système d’imbrication. 
Cette stratégie consiste à ajouter des Identités (utilisateurs et ordinateurs) dans un groupe Global. Ce dernier est 
membre d’un groupe Domaine Local. Celui ci sera positionné dans une ACL. 

Ainsi, si un nouveau groupe appelé G_Tech_w doit avoir accès à la ressource partagée nommée Informatique, il 
n’est plus nécessaire d’accéder à l’ACL. Un ajout dans le groupe DL_IT_w (celui ci est bien sûr positionné sur la 
ressource) doit être effectué afin de procurer l’accès souhaité. 

# **Création d'un groupe**

Pour créer un groupe il suffit de lancer la console "Utilisateurs et ordinateurs Active Directory" et de séléctionner le dossier "User"
