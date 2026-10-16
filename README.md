# Laboratoire Windows Server 2025

## Présentation du projet

Ce projet documente le déploiement et l'administration d'un laboratoire Windows Server 2025 virtualisé avec Oracle VirtualBox.

L'objectif est de développer des compétences pratiques en administration systèmes, réseaux, gestion des identités et des accès, ainsi qu'en diagnostic et résolution d'incidents.

## Environnement du laboratoire

- **Hyperviseur :** Oracle VirtualBox
- **Système d'exploitation :** Windows Server 2025
- **Nom de domaine :** `lab.local`
- **Contrôleur de domaine :** `SRV001`
- **Adresse IP interne du serveur :** `192.168.2.1`
- **Réseau interne :** `192.168.2.0/24`

## Architecture réseau

Le laboratoire utilise plusieurs interfaces réseau virtuelles afin de séparer les communications internes de l'accès au réseau externe.

- **SRV001 :** contrôleur de domaine Active Directory, serveur DNS et serveur DHCP.
- **Réseau interne :** communication entre le serveur et les postes clients.
- **Interface NAT :** accès au réseau externe depuis les machines virtuelles.
- **Postes clients :** intégrés au domaine `lab.local` pour tester les services et les stratégies de groupe.

## Services et configurations réalisés

### Active Directory Domain Services (AD DS)

- Configuration du domaine `lab.local`.
- Création et gestion des utilisateurs et des groupes de sécurité.
- Organisation des objets à l'aide des unités d'organisation (OU).
- Intégration des postes clients au domaine.

### DNS (Domain Name System)

- Configuration des zones de recherche directe et inversée.
- Création d'enregistrements A, CNAME et PTR.
- Configuration de la résolution des noms.
- Vérification du fonctionnement avec `nslookup`.

### DHCP (Dynamic Host Configuration Protocol)

- Configuration d'une étendue d'adresses IP dynamiques.
- Définition des options DNS et du nom de domaine.
- Gestion des exclusions et des réservations d'adresses IP.
- Autorisation du serveur DHCP dans Active Directory.

### Partages réseau et permissions SMB/NTFS

- Création de partages réseau par service.
- Configuration des permissions SMB et NTFS.
- Attribution des droits à l'aide de groupes de sécurité Active Directory.
- Vérification des droits de lecture, de création, de modification et de suppression de fichiers.
- Diagnostic et correction des problèmes de permissions.

### Stratégies de groupe (GPO)

- Création et liaison de stratégies de groupe.
- Configuration du mappage automatique des lecteurs réseau.
- Adaptation des lecteurs accessibles selon les groupes et les
