# **Résolution problème rencontré pour l'acces a internet **

Ma machine SRV-Core ayant besoin d'accéder a internet pour installer le package NuGet. J'ai configurer AD1 pour qu'il permettes a mes machines de communiquer avec Internet en passant par lui, afin qu'il agisse comme un router/NAT)

On commence d'abord commencer par installer RRAS sur AD1 grâce a la commande : `Install-WindowsFeature -Name Routing -IncludeManagementTools`

Ensuite on lance RRAS `rrasmgmt.msc`

Ensuite on le configure en faisant AD1 -> clic droit -> Configurer et activer le routage et l'accès distant

Configuration personnalisée
NAT
On valide et ça démarre le service

Ensuite on va déclarer la carte internet

NAT -> Nouvelle interface -> Et on sélectionne la carte Ethernet qui accède a internet

	on choisi : "Interface publique connectée à Internet"
	et on coche "Activer NAT sur cette interface"

On déclare aussi la carte du LAB :
NAT -> Nouvelle interface -> on sélectionne la carte Ethernet du LAB
	
	on choisi : "Interface privée connectée au réseau privé"

On restart ensuite le service avec cette commande : `Restart-Service RemoteAccess`

Vous pouvez ensuite tester sur les serveurs la bonne connexion à Internet. 

Si le problème persiste vérifier si le DNS préférer est bien AD1, et vérifier qu'il n'y ai pas un conflit avec l'adresse IPv6. Au besoin faite passer l'IPV4 en priorité pour résoudre le probleme 

Ma machine SRV-Core ayant besoin d'accéder a internet pour installer le package NuGet. J'ai configurer AD1 pour qu'il permettes a mes machines de communiquer avec Internet en passant par lui, afin qu'il agisse comme un router/NAT)

On commence d'abord commencer par installer RRAS sur AD1 grâce a la commande : `Install-WindowsFeature -Name Routing -IncludeManagementTools`

Ensuite on lance RRAS `rrasmgmt.msc`

Ensuite on le configure en faisant AD1 -> clic droit -> Configurer et activer le routage et l'accès distant

Configuration personnalisée
NAT
On valide et ça démarre le service

Ensuite on va déclarer la carte internet

NAT -> Nouvelle interface -> Et on sélectionne la carte Ethernet qui accède a internet

	on choisi : "Interface publique connectée à Internet"
	et on coche "Activer NAT sur cette interface"

On déclare aussi la carte du LAB :
NAT -> Nouvelle interface -> on sélectionne la carte Ethernet du LAB
	
	on choisi : "Interface privée connectée au réseau privé"

On restart ensuite le service avec cette commande : `Restart-Service RemoteAccess`

Vous pouvez ensuite tester sur les serveurs la bonne connexion à Internet. 

Si le problème persiste vérifier si le DNS préférer est bien AD1, et vérifier qu'il n'y ai pas un conflit avec l'adresse IPv6. Au besoin faite passer l'IPV4 en priorité pour résoudre le probleme 
