# **1-Création d’un utilisateur en PowerShell**

La création d’utilisateurs Active Directory en PowerShell permet d’automatiser la création de un ou plusieurs objets. 
Il est possible d’utiliser un fichier CSV avec un script PowerShell afin de créer un grand nombre d’utilisateur. 
La cmdlet permettant la création d’un objet utilisateur dans un annuaire AD est NewADUser.  
Les syntaxes ci dessous peuvent être utilisées afin de créer un utilisateur. 

Dans un premier temps, le module Active Directory doit être importé, cela permet l’utilisation de commandes liées à 
l’annuaire AD (récupération des attributs LDAP d’un compte, création d’un utilisateur…). Ce module est présent sur 
les contrôleurs de domaine. 

`Import-module ActiveDirectory`

Utilisons maintenant une variable nommée password, qui nous servira à stocker le mot de passe de 
l’utilisateur. Néanmoins avant d’être stocké dans la variable, le mot de passe est converti en chaîne de caractère 
sécurisée.

`$password = "P@ssw@rd" | ConvertTo-SecureString -AsPlainText -Force`

On peut maintenant utilisé `New-aduser` afin de procéder à la création du compte utilisateur. Le 
paramètre CannotChangePassword positionné à False autorise l’utilisateur à changer le mot de passe. 

`New-aduser -name "userTest" -AccountPassword $password   -CannotChangePassword $False -City "Marseille" -Company "ENI" -Department "IT"   -Description "Création à l’aide de Powershell" -DisplayName "Utilisateur Test"   -EmailAddress "Test@nibonnet.fr" -Enabled $True -GivenName "Utilisateur"   -HomePage "www.nibonnet.fr" -PasswordNeverExpires $True -SamAccountName "utest"  -UserPrincipalName "Test@Formation.local" `

# **2-Création d'un groupe en PowerShell**

Comme pour les utilisateurs, il est possible de créer des groupes Active Directory à l’aide de PowerShell. 

La cmdlet `NewADGroup` permet d’effectuer l’opération. La syntaxe à utiliser est la suivante :  
Dans un premier temps, l’importation du module Active Directory doit être effectuée. Ceci permettra l’utilisation des 
cmdlets nécessaires pour effectuer des opérations sur l’annuaire. 

`Import-Module ActiveDirectory`

L’opération de création peut maintenant être lancée. 

`New-ADGroup -GroupScope Global -Name G_PrintIT_W -Description "Groupe créé avec Powershell" -DisplayName G_PrintIT_W `

Le groupe est bien créé, néanmoins l’ajout d’utilisateur s’effectue à l’aide de la cmdlet Add-ADGroupMember. Le 
module Active Directory doit avoir été importé avant d’exécuter la commande suivante : 

`add-ADGroupMember -Identity ’G_PrintIT_W’ -Members ’jbak’`

Après avoir exécuté l’ensemble des opérations ci dessus, le groupe est bien créé et l’utilisateur ajouté. 

# **3-Gestion du DHCP en PowerShell**

L’installation du rôle est la première étape à effectuer. L’opération va consister à installer les consoles et fichiers 
nécessaires à l’exploitation quotidienne du service

Pour cela il faut utiliser cette commande :
`Install-WindowsFeature -Name DHCP -IncludeManagementTools`

Une fois installée, il est maintenant nécessaire de l’autoriser dans Active Directory. Pour cela, on tulise la commande :
`Add-DhcpServerInDC -DnsName NomServeurDHCP -IPAddress AdresseIpServeur`

L’installation du rôle est maintenant terminée. En accédant à la console Gestionnaire de serveur, on peut voir que 
l’étape de Post Installation est toujours présente. 

Pour supprimer cette notification à l’aide de PowerShell, exécutez l’instruction suivante : 
`Set-ItemProperty -Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 -Name ConfigurationState -Value 2`

Création de l’étendue

L’étendue va contenir la plage d’adresses pouvant être distribuées aux différents postes de travail. Elle peut 
également contenir d’autres paramètres (serveur DNS, Wins…). 
La création s’opère à l’aide de plusieurs cmdlets :  
- `AddDhcpServer4Scope` pour effectuer la création de l’étendue.
- `AddDhcpServer4ExclusionRange` permet l’exclusion de plusieurs adresses dans une étendue. 
- `SetDhcpServer4OptionDefinition` assure la configuration des options souhaitées. 
- `GetDhcpServer4Scope` donne la liste des étendues DHCP présentes dans le serveur interrogé. 

Il est nécessaire dans un premier temps d’effectuer la création de l’étendue. Pour cela la syntaxe ci-dessous peut 
être utilisée, la plage d’adresses sera de 192.168.10.110 à 192.168.10.200.
`Add-DhcpServerv4Scope -Name "Formation" -StartRange 192.168.10.110 -EndRange 192.168.10.200 -SubnetMask 255.255.255.0`

La plage d’adresses IP allant de 192.168.10.195 à 192.168.10.200 peut maintenant être exclue. La syntaxe ci
dessous est utilisée afin de procéder à l’opération d’exclusion.
`Add-DHCPServerV4ExclusionRange -ScopeId 192.168.10.0 -StartRange 192.168.10.195 -EndRange 192.168.10.20`

La passerelle doit également être configurée afin de pouvoir être distribuée avec les baux DHCP. 
`Set-DhcpServerv4OptionValue -OptionId 3 -Value 192.168.1.254 -ScopeID 192.168.1.0`

Les options portant l’ID 6 (Serveurs DNS) et 15 (Suffixe DNS) peuvent maintenant être configurées. 
Option numéro 6 : Serveur DNS
`Set-DhcpServerv4OptionValue -OptionId 6 -Value 192.168.1.10   -ScopeID 192.168.1.0`

`Set-DhcpServerv4OptionValue -OptionId 15 -Value Formation.local   -ScopeID 19`

L’étendue peut maintenant être activée. 
`Set-DhcpServerv4Scope -ScopeId 192.168.1.0 -Name "Formation"   -State Active`
