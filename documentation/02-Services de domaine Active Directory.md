# **Ajout du role AD-DS sur AD1**
Pour commencer nous allons ajouter le role AD-DS sur AD1 :

![Ajout du service AD-DS](../Screenshot/AjoutduserviceAD-DS.png)

Cela va nous permette de pouvoir :
- Stocker les comptes utilisateurs, les groupes, les machines
- Gèrer la sécurité, les stratégies de groupe (GPO), l’authentification Kerberos
- Et de créer une forêt, un domaine, des OU

Une fois la fonctionnalité ajouter, nous pouvons cliquer sur le drapeau et sur "Promouvoir ce serveur en controleur de domaine"
Nous allons ensuite crée une nouvelle foret que nous appelrons Formation.local :

![Création d'une forêt](../Screenshot/ajoutnouvelleforet.png)

Ensuite suiver les etape suivant et a la fin  de l'installation le serveur rédmarrera

# **Installation d'un RODC sur AD2**
Dans Site et service Active directory, j'ai renommé le site par defaut par le nom "Marseille" et j'ai crée un autre site avec le nom de "Paris" (ce site sera attribué au serveur AD2 qui sera en lecture seul)

![Nouveau site Paris](../Screenshot/nouveau-site-Paris-RODC.png)

Sur AD1 dans Utilisateur et Ordinateur Active Directory, j'ai crée au préalable un compte de côntroleur de domaine en lecture seul :

![Configuration-serveur-RODCdepuisAD1](../Screenshot/Configuration-serveur-RODCdepuisAD1.png)

Ensuite sur AD2, j'ai ajouter le role AD-DS et j'ai ajouter lecontroleur de domaine au domaine existant "Formation.local"

![AD2-RODC](../Screenshot/AD2-RODC.png)

Puis j'ai verifier dans "Utilisateur et Ordinateur Active Directory" que AD2 etait bien lecteur seul 

![VerificationAD2-RODC](../Screenshot/VerificationAD2-RODC.png)

# **Verification a réaliser apres l'installtion d'uun contrôleur de domaine**

L'installation d'un controleur de domaine terminée, il peut être utile de vérifier les points suivants :
- la bonne configuration des sites AD.
- La configuration de la réplication intersites.
- La bonne configuration de la zone DNS.
- L'association des sous-réseaux IP avec les bon sites.

![Verification-association des sous réseauIP avec les bon sites](../Screenshot/Verification-association-des-sous-réseauIP-avec-les-bon-sites.png)

Verifier la présence des enregistrement de type SRV dans le DNS :

![verification-enregistrement type SRV](../Screenshot/verification-enregistrement-type-SRV.png)

On peut aussi executer la commande dcdiag /test:replication afin de s'assurer de la bonne replication entre AD1 et AD2

![commande-verif-bonne-replication](../Screenshot/commande-verif-bonne-replication.png)


