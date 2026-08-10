# **Clonage AD1**

Le clonage permet de créer rapidement un nouveau contrôleur de domaine à partir d'un contrôleur de domaine existant, au lieu de refaire toute l'installation et la promotion manuellement.

Par exemple :

Une entreprise possède un contrôleur de domaine virtuel nommé DC01.
Elle veut créer plusieurs contrôleurs de domaine supplémentaires.
Elle clone DC01.
Le nouveau serveur devient automatiquement un nouveau contrôleur de domaine avec une identité propre.

Cela permet donc 
- Un déploiement rapide qui évite de réinstaller Windows Server et de refaire toutes les étapes de promotion AD DS.
- Utile dans les environnements virtualisés, particulièrement adapté aux infrastructures utilisant des hyperviseurs compatibles.
- Facilite les extensions d'infrastructure, particulièrement intéressant lors de l'ouverture de nouveaux sites ou de l'ajout de capacité.
- Réduit les erreurs humaines car les paramètres validés du contrôleur existant servent de modèle.

Pour commencer il suffit d'ajouter le contrôleur de domaine dans le groupe "Contrôleur de domaine clonable" :

![Configuration-groupe-clonable](../Images/Clonage/Configuration-groupe-clonable.png)

Ensuite il est nécessaire de redémarrer le serveur afin que l'ajout au groupe soit prit en compte.

Puis il faut exécuter la commande "Get-ADDCCloningExcludedApplicationList" afin d'identifier toutes les programmes et services qui ne sont pas compatible avec le clonage

De notre coté aucun programme ou service ne posera problème donc nous pouvons ensuite utiliser la commande "New-ADDCCloneConfigFile" pour configurer ça création. Il est possible de lui attribuer directement une adresse IP fixe, un nom, une route par défaut et son nom de site :

![Clonage-verification](../Images/Clonage/Clonage-verification.png)
