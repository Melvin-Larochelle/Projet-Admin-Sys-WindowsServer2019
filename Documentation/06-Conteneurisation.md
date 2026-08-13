Les conteneurs sont une nouvelle fonctionnalité apportée par Windows Server 2016 TP3. Avec cette fonctionnalité, 
le système d’exploitation est virtualisé. 

Lors de l’exécution d’une application présente dans un conteneur, cette dernière pense s’exécuter sur son propre 
système. Elle est réellement présente sur le même serveur que les autres applications. 

Les conteneurs sont donc différents de la virtualisation de machine. Dans ce dernier cas, il n’est pas possible d’isoler 
une application. Si la machine virtuelle héberge trois applications, elles utilisent toutes le même système 
d’exploitation. 

Avec les conteneurs, l’exécution d’une application s’effectue maintenant sans impacter le système d’exploitation, et 
inversement.  

Les concepts clés cidessous sont important à prendre en compte :  
- Container Host : serveur de type physique ou virtuel sur lequel la fonctionnalité Windows Server Container est 
installée. Il a pour fonction d’exécuter un ou plusieurs conteneurs Windows Server.
- Container OS Image : ce type d’image fournit un système d’exploitation. Il n’est pas possible de procéder à des 
modifications. 
- Container Image : une image Container contient des modifications apportées et non présentes dans l’image OS 
(Container Image OS). Cela peut être l’installation d’un logiciel, la modification de clés de registre… Une image est 
créée en convertissant une Sandbox en Container Image. 
- Sandbox : toutes les actions d’écriture telles que l’ajout d’une application, la modification d’une clé de registre, etc., 
sont présentes dans la Sandbox. Une fois le conteneur arrêté, il est possible de procéder à la suppression de ces 
modifications ou à la conversion d’une Sandbox en Container Image. 
- Container Repository : les images Container sont stockées dans un référentiel local. L’hôte a la possibilité d’utiliser 
ces images une multitude de fois. 
- Container Management Technology : la gestion des conteneurs peut s’effectuer par l’intermédiaire de PowerShell 
ou de Docker. 

L’administration s’effectue par l’intermédiaire du client Docker ou tout simplement en PowerShell. Le déploiement 
des applications dans le cloud va s’en trouver facilité. 
