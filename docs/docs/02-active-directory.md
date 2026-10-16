# Active Directory Domain Services

## Présentation du service

Active Directory Domain Services (AD DS) est un service d'annuaire permettant de centraliser la gestion des utilisateurs, des groupes, des ordinateurs et des ressources d'un domaine Windows.

Dans ce laboratoire, Active Directory permet de gérer les comptes utilisateurs, d'organiser les objets du domaine et de contrôler l'accès aux ressources du réseau.

## Environnement

- **Contrôleur de domaine :** `SRV001`
- **Nom de domaine :** `lab.local`
- **Système d'exploitation :** Windows Server 2025
- **Adresse IP interne du serveur :** `192.168.2.1`

## Configuration réalisée

### Domaine Active Directory

- Configuration du domaine `lab.local`.
- Utilisation de `SRV001` comme contrôleur de domaine.
- Gestion centralisée des comptes et des ressources du domaine.

### Unités d'organisation (OU)

Les unités d'organisation permettent de structurer les objets Active Directory et de faciliter l'administration.

Les unités d'organisation utilisées dans le laboratoire sont :

- `Administration`
- `Compta`
- `Direction`
- `IT`
- `Domain Controllers`

### Utilisateurs et groupes de sécurité

Les groupes de sécurité permettent d'attribuer des droits aux utilisateurs selon leur service.

Les groupes utilisés dans le laboratoire sont :

- `LAB\Administration`
- `LAB\Compta`
- `LAB\Direction`
- `LAB\IT`

Les comptes utilisateurs sont organisés selon les besoins du laboratoire et associés aux groupes appropriés.

## Intégration des postes clients

Les postes clients sont intégrés au domaine `lab.local` afin de bénéficier de l'authentification centralisée et des stratégies de groupe.

Cette intégration permet notamment de tester :

- L'ouverture de session avec un compte du domaine.
- L'accès aux ressources partagées.
- L'application des stratégies de groupe.
- La relation de confiance entre les postes clients et le domaine.

## Diagnostic et validation

Les outils et commandes suivants permettent de vérifier le fonctionnement d'Active Directory.

- `whoami` : identification du compte utilisé pour la session.
- `gpresult /r` : consultation des stratégies de groupe appliquées.
- `Test-ComputerSecureChannel` : vérification de la relation de confiance entre un poste Windows et le domaine.
- `Test-ComputerSecureChannel -Repair -Credential (Get-Credential)` : tentative de réparation de cette relation de confiance avec des identifiants autorisés.

Une réparation de la relation de confiance a notamment été réalisée après un problème rencontré sur un poste client.

## Résultats obtenus

- Gestion centralisée des utilisateurs et des groupes.
- Organisation des objets dans des unités d'organisation.
- Intégration des postes clients au domaine.
- Utilisation des groupes de sécurité pour gérer les accès aux ressources.
- Diagnostic et réparation d'une relation de confiance défaillante.

