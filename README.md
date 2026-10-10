# Laboratoire Windows Server 2025

## Présentation du projet

Ce projet documente le déploiement et l'administration d'un environnement de laboratoire Windows Server 2025 virtualisé avec Oracle VirtualBox.

L'objectif est de développer des compétences pratiques en administration systèmes, services réseau, gestion des identités et des accès, et administration des stratégies de groupe.

## Environnement du laboratoire

- **Hyperviseur :** Oracle VirtualBox
- **Système d'exploitation :** Windows Server 2025
- **Nom de domaine :** `lab.local`
- **Contrôleur de domaine :** `SRV001`
- **Réseau interne :** `192.168.2.0/24`
- **Adresse IP interne du serveur :** `192.168.2.1`

## Services et configurations réalisés

### 1. Active Directory Domain Services (AD DS)

- Configuration du domaine Active Directory
- Création et gestion des utilisateurs et groupes de sécurité
- Organisation des objets avec les unités d'organisation (OU)
- Intégration des postes clients au domaine

### 2. DNS (Domain Name System)

- Configuration d'une zone de recherche directe
- Création d'enregistrements A et CNAME
- Configuration d'une zone de recherche inversée
- Création d'enregistrements PTR
- Tests de résolution de noms avec `nslookup`

### 3. DHCP (Dynamic Host Configuration Protocol)

- Configuration d'une étendue DHCP et attribution dynamique des adresses IP
- Configuration des options DHCP, notamment DNS et domaine
- Gestion des exclusions et réservations d'adresses IP
- Autorisation du serveur DHCP dans Active Directory

### 4. Partages SMB et permissions NTFS

- Création de partages réseau par service
- Configuration des permissions SMB et NTFS
- Gestion des droits d'accès à l'aide de groupes de sécurité
- Tests de lecture, création, modification et suppression de fichiers
- Diagnostic des problèmes de permissions

### 5. Stratégies de groupe (GPO)

- Création et liaison de stratégies de groupe
- Configuration du mappage automatique des lecteurs réseau
- Adaptation des lecteurs accessibles selon les besoins des utilisateurs
- Vérification de l'application des stratégies avec `gpresult`

## Diagnostic et validation

Les exercices pratiques ont notamment porté sur :

- Le diagnostic de la configuration IP et de la connectivité réseau
- La vérification de la résolution DNS
- Le dépannage de la relation de confiance entre un poste client et le domaine
- Le diagnostic des permissions SMB et NTFS
- La vérification de l'application des GPO

### Outils utilisés

- Invite de commandes Windows (CMD)
- PowerShell
- Gestionnaire DNS
- Gestionnaire DHCP
- Utilisateurs et ordinateurs Active Directory
- Gestion de stratégie de groupe

## Compétences développées

- Compréhension des interactions entre Active Directory et DNS
- Configuration et validation des services réseau
- Gestion des utilisateurs, groupes et droits d'accès
- Différenciation entre permissions SMB et NTFS
- Déploiement et diagnostic des stratégies de groupe
- Utilisation de CMD et PowerShell pour l'administration et le dépannage
- Documentation des procédures techniques

## Évolutions prévues

Ce laboratoire est un projet personnel en cours d'évolution. Les prochaines étapes pourront inclure :

- Approfondissement de l'administration Windows Server
- Mise en place et validation de procédures de sauvegarde et de restauration
- Déploiement de services Linux
- Analyse des journaux système
- Mise en place d'outils de supervision et de détection de sécurité

