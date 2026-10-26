# **IPAM**

IPAM (IP Address Management) est une fonctionnalité intégrée dans les systèmes d’exploitation Microsoft depuis 
Windows Server 2012. Elle donne la possibilité de découvrir, surveiller, auditer et gérer une ou plusieurs plages 
d’adresses IP. De plus il est possible d’effectuer des tâches d’administration et de surveillance des serveurs DHCP et DNS.

Les composants suivants sont compris dans la fonctionnalité :  
- Découverte automatique de l’infrastructure des adresses IP : cela permet d’effectuer la découverte des contrôleurs de domaine, des serveurs DHCP et des serveurs DNS dans le domaine souhaité. 
- Affichage, création de rapports et gestion personnalisés de l’espace d’adressage IP : cela permet d’obtenir des informations sur le suivi et l’utilisation des adresses IP. Ainsi les espaces d’adressages IPv4 et IPv6 peuvent être 
organisés en blocs d’adresses IP, en plages d’adresses IP et en adresses IP individuelles. 
- Audit des modifications de configuration du serveur et suivi de l’utilisation des adresses IP : permet l’affichage des différents événements opérationnels du serveur IPAM et DHCP géré par la fonctionnalité. Un suivi des 
adresses IP, ID de client, nom d’hôte ou nom d’utilisateur est également effectué. De plus les événements de baux DHCP et les événements d’ouverture de session utilisateur sont collectés sur les serveurs NPS (Network Policy Server), 
sur les contrôleurs de domaine et sur les serveurs DHCP.  

Deux méthodes sont envisageables pour déployer des serveurs IPAM : 
- Distribuée : un serveur IPAM sur chaque site de l’entreprise.
- Centralisée : un serveur pour l’ensemble de l’entreprise. 

IPAM effectue des tentatives périodiques de localisation des contrôleurs de domaine, des serveurs DNS et DHCP. 
Cette opération concerne évidemment les serveurs qui se trouvent dans l’étendue (unité d’organisation, domaine ou site AD) des stratégies de groupe. Afin d’être gérés par IPAM et d’autoriser l’accès à ce dernier, les paramètres de 
sécurité et les ports du serveur doivent être configurés. 

La communication entre le serveur IPAM et les serveurs gérés se fait par le biais de WMI ou RPC. 

# **2 - Les spécifications d’IPAM**

L’étendue de la découverte pour les serveurs IPAM est limitée uniquement à une seule forêt Active Directory. Les 
serveurs pris en charge (NPS, DNS et DHCP) doivent exécuter Windows Server 2008 (ou versions ultérieures) et être 
joints à un domaine. Attention certains éléments réseau (WINS  Windows Internet Naming Service , proxys…) ne 
sont pas pris en charge par le serveur IPAM.  

Une base de données de type interne peut être utilisée, il est également possible d’utiliser SQL Server. 

Un serveur IPAM peut prendre en charge plusieurs centaines de serveurs DHCP et serveurs DNS.  

Néanmoins aucune stratégie consistant à nettoyer la base de données au bout d’un certain temps n’est présente. 
L’administrateur doit donc effectuer cette opération manuellement. 

Avec l’installation d’IPAM, les fonctionnalités suivantes sont également installées : 

- Outils d’administration de serveur distant : installation des outils DHCP, DNS et du client IPAM, ceci afin 
d’effectuer la gestion à distance des différents serveurs gérés.

- Base de données interne Windows : une base de données doit être utilisée, elle peut être de type interne (utilisable uniquement par certains rôles et fonctionnalités du système d’exploitation). Depuis Windows Server 2012 
R2, il est possible d’utiliser une base de données SQL Server (sur le serveur IPAM ou un autre serveur).

- Service d’activation des processus Windows : élimine la dépendance au protocole HTTP en généralisant le modèle de processus IIS.
  
- Gestion des stratégies de groupe : installe la console MMC permettant la gestion des stratégies de groupe.
  
- .NET Framework : installation de la fonctionnalité .NET Framework 4.5.

# **3. Installation d’IPAM**
