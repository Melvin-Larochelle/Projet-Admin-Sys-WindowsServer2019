Création d’un utilisateur en PowerShell

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
