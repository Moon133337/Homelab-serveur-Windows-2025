# Partages SMB et permissions NTFS

## Présentation

SMB permet de partager des fichiers et des dossiers sur le réseau. NTFS permet de contrôler les droits d'accès aux fichiers et aux dossiers sur le système de fichiers Windows.

Dans ce laboratoire, les partages réseau sont organisés par service. Les droits sont attribués à l'aide de groupes de sécurité Active Directory.

## Environnement

- **Serveur de fichiers :** `SRV001`
- **Domaine :** `lab.local`
- **Répertoire principal :** `C:\Partages`
- **Groupes de sécurité :** `Administration`, `Compta`, `Direction` et `IT`

## Organisation des partages

Les dossiers sont organisés de la manière suivante :

- `C:\Partages\Administration`
- `C:\Partages\Compta`
- `C:\Partages\Direction`
- `C:\Partages\IT`

Chaque dossier est publié sous forme de partage réseau accessible via `\\SRV001\NomDuPartage`.

## Configuration des permissions

### Permissions SMB

Les permissions SMB contrôlent les accès lorsqu'un utilisateur se connecte au partage via le réseau.

Les droits configurés sont les suivants :

- **Administration :** groupes Administration, Direction et IT.
- **Compta :** groupes Compta, Direction et IT.
- **Direction :** groupes Direction et IT.
- **IT :** groupe IT.

Les groupes autorisés disposent du niveau d'accès `Change` sur les partages correspondants.

### Permissions NTFS

Les permissions NTFS contrôlent les accès aux dossiers et aux fichiers sur le système de fichiers.

- **Administration :** groupes Administration, Direction et IT avec le droit `Modify`.
- **Compta :** groupes Compta, Direction et IT avec le droit `Modify`.
- **Direction :** groupes Direction et IT avec le droit `Modify`.
- **IT :** groupe IT avec le droit `Modify`.
- **SYSTEM et Administrators :** contrôle total pour l'administration du système.

Les permissions ont été configurées pour être héritées par les fichiers et les sous-dossiers.

## Commandes utilisées

### PowerShell

- `Get-SmbShare` : affiche les partages SMB configurés.
- `Get-SmbShareAccess` : affiche les autorisations d'un partage SMB.
- `New-SmbShare` : crée un partage réseau.
- `Grant-SmbShareAccess` : accorde une autorisation sur un partage.
- `Revoke-SmbShareAccess` : retire une autorisation sur un partage.
- `Get-Acl` : affiche les permissions NTFS d'un dossier.

### CMD

- `icacls` : affiche ou modifie les permissions NTFS.

## Différence entre SMB et NTFS

Les permissions SMB s'appliquent à l'accès réseau au partage, tandis que les permissions NTFS s'appliquent aux fichiers et dossiers eux-mêmes.

Lorsqu'un utilisateur accède à un fichier via le réseau, les deux couches de permissions doivent autoriser l'opération demandée. Le niveau d'accès effectif est limité par la combinaison de ces autorisations.

Dans le laboratoire, les partages ont été configurés avec le droit SMB `Change` et les dossiers avec le droit NTFS `Modify`.

## Tests et validation

Les tests ont été réalisés avec des comptes utilisateurs du domaine.

- Vérification de l'accès aux partages selon les groupes de sécurité.
- Test de lecture des fichiers.
- Test de création et de modification de fichiers.
- Test de suppression de fichiers.
- Vérification des autorisations SMB et NTFS en cas de refus d'accès.

Un problème a été rencontré lorsque le partage SMB était limité à `Read`, alors que les permissions NTFS autorisaient `Modify`. La création de fichiers était impossible. Le passage du partage SMB à `Change` a permis de rétablir les opérations attendues.

## Résultats obtenus

- Création de quatre partages réseau.
- Attribution des droits selon les groupes de sécurité Active Directory.
- Configuration distincte des permissions SMB et NTFS.
- Résolution d'un problème de droits d'accès.
- Validation de la lecture, de la création, de la modification et de la suppression de fichiers avec un compte de test IT.

