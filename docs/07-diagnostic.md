# Diagnostic et dépannage

## Présentation

Cette documentation regroupe les méthodes et les outils utilisés pour diagnostiquer les problèmes rencontrés dans le laboratoire Windows Server 2025.

L'objectif est de vérifier le fonctionnement des services réseau, d'identifier les causes des erreurs et de valider les corrections apportées.

## Environnement

- **Serveur principal :** `SRV001`
- **Domaine Active Directory :** `lab.local`
- **Réseau interne :** `192.168.2.0/24`
- **Services concernés :** Active Directory, DNS, DHCP, SMB, NTFS et GPO

## Outils de diagnostic

### CMD

- `ipconfig /all` : affiche la configuration IP des interfaces réseau.
- `ping` : vérifie la connectivité IP entre deux équipements.
- `nslookup` : teste la résolution DNS.
- `gpresult /r` : affiche les stratégies de groupe appliquées.
- `whoami` : identifie le compte utilisé pour la session.
- `icacls` : affiche ou modifie les permissions NTFS.

### PowerShell

- `Get-DhcpServerInDC` : affiche les serveurs DHCP autorisés dans Active Directory.
- `Get-SmbShare` : affiche les partages SMB configurés.
- `Get-SmbShareAccess` : consulte les autorisations des partages SMB.
- `Get-Acl` : consulte les permissions NTFS d'un dossier.
- `Test-ComputerSecureChannel` : vérifie la relation de confiance entre un ordinateur et le domaine.

## Problèmes rencontrés et solutions

### Permissions SMB et NTFS

Un utilisateur ne pouvait pas créer de fichier dans un partage alors que les permissions NTFS autorisaient la modification.

Le partage SMB était limité au droit `Read`.

La correction a consisté à accorder le droit SMB `Change` au groupe autorisé, tout en conservant le droit NTFS `Modify`.

Le test de création de fichier a ensuite permis de valider la correction.

### Relation de confiance Active Directory

Une relation de confiance entre un poste client et le domaine a été rompue après le clonage d'une machine virtuelle intégrée au domaine.

La commande suivante a été utilisée pour tenter de réparer cette relation avec des identifiants autorisés :

`Test-ComputerSecureChannel -Repair -Credential (Get-Credential)`

La commande a retourné `True`, confirmant le rétablissement du canal sécurisé.

### Application des GPO

La présence d'une stratégie dans la console de gestion ne garantissait pas son application à l'utilisateur.

La vérification avec `gpresult /r` a permis de contrôler les stratégies effectivement appliquées et d'identifier les problèmes de liaison ou de filtrage.

Un chemin incorrect dans la configuration d'un lecteur réseau a également été corrigé.

### Résolution DNS

Les tests avec `nslookup` ont permis de vérifier la résolution des noms locaux et externes.

La requête vers un serveur DNS public pour un nom appartenant à la zone locale `test.local` a retourné `NXDOMAIN`. Ce résultat était attendu, car cette zone de test n'est pas publiée dans le DNS public.

## Méthode de dépannage

La démarche utilisée repose sur les étapes suivantes :

1. Identifier le problème et le résultat attendu.
2. Vérifier la configuration concernée.
3. Exécuter les commandes de diagnostic adaptées.
4. Identifier la cause probable.
5. Appliquer une correction ciblée.
6. Refaire les tests pour valider le résultat.

## Résultats obtenus

- Diagnostic de problèmes de permissions réseau.
- Réparation d'une relation de confiance Active Directory.
- Vérification de l'application des stratégies de groupe.
- Tests de résolution DNS.
- Utilisation de CMD et PowerShell pour l'administration et le dépannage.

