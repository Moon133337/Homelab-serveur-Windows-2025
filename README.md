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
- **Plage DHCP :** `192.168.2.200` à `192.168.2.220`

## Architecture réseau

```text
                 LABORATOIRE WINDOWS SERVER 2025
                 =================================

                    ORACLE VIRTUALBOX
                            |
             +--------------+--------------+
             |                             |
     RESEAU NAT                     RESEAU INTERNE
     Acces Internet                 192.168.2.0/24
             |                             |
       +-----+------+                +-----+------+
       |            |                |            |
   +--------+  +---------+       +--------+  +---------+
   | SRV001 |  | Clients |       | SRV001 |  | Clients |
   +--------+  +---------+       +--------+  +---------+
   10.0.3.15    10.0.3.x         192.168.2.1 192.168.2.x
       |                             |
       |                       +------------------+
       |                       | SERVICES SERVEUR |
       |                       +------------------+
       |                       | AD DS : domaine  |
       |                       | DNS  : resolution|
       |                       | DHCP : adresses  |
       |                       | SMB  : partages  |
       |                       | GPO  : politiques|
       |                       +------------------+

     Le NAT fournit l'acces Internet.
     Le reseau interne permet aux VM de communiquer
     avec le serveur et ses services.
     
     SRV001 possede deux interfaces reseau, mais
     ne route pas le trafic entre les deux reseaux.
```

Le laboratoire utilise plusieurs interfaces réseau virtuelles afin de séparer les communications internes de l'accès au réseau externe.

- **Réseau interne :** communication entre le serveur et les postes clients.
- **Interface NAT :** accès au réseau externe depuis les machines virtuelles.
- **Serveur SRV001 :** hébergement des services d'annuaire et des services réseau.
- **Postes clients :** intégration au domaine pour tester l'authentification, les stratégies de groupe et les accès aux ressources partagées.

## Services et configurations réalisés

### Active Directory Domain Services (AD DS)

- Configuration du domaine `lab.local`.
- Création et gestion des utilisateurs et des groupes de sécurité.
- Organisation des objets à l'aide des unités d'organisation (OU).
- Intégration des postes clients au domaine.

### DNS (Domain Name System)

- Configuration des zones de recherche directe et inversée.
- Création d'enregistrements A, CNAME et PTR.
- Configuration des redirecteurs DNS.
- Vérification de la résolution des noms.

### DHCP (Dynamic Host Configuration Protocol)

- Configuration d'une étendue d'adresses IP dynamiques.
- Définition des options DNS et du nom de domaine.
- Gestion des exclusions et des réservations d'adresses IP.
- Autorisation du serveur DHCP dans Active Directory.

### Partages SMB et permissions NTFS

- Création de partages réseau par service.
- Configuration des permissions SMB et NTFS.
- Attribution des droits à l'aide de groupes de sécurité Active Directory.
- Vérification des droits de lecture, de création, de modification et de suppression de fichiers.

### Stratégies de groupe (GPO)

- Création et liaison de stratégies de groupe.
- Configuration du mappage automatique des lecteurs réseau.
- Adaptation des lecteurs accessibles selon les besoins des utilisateurs.
- Vérification de l'application des stratégies.

## Diagnostic et dépannage

Les exercices pratiques ont notamment porté sur :

- Le diagnostic de la configuration IP et de la connectivité réseau.
- La vérification de la résolution DNS.
- La réparation d'une relation de confiance entre un poste client et le domaine.
- L'analyse et la correction des permissions SMB et NTFS.
- La vérification de l'application des stratégies de groupe.

## Outils utilisés

- CMD (invite de commandes Windows)
- PowerShell
- Gestionnaire DNS et DHCP
- Utilisateurs et ordinateurs Active Directory
- Gestion de stratégie de groupe
- Outils de diagnostic réseau Windows

## Documentation

Les configurations et les manipulations réalisées sont détaillées dans les documents suivants.

- [Architecture réseau](docs/01-architecture-reseau.md)
- [Active Directory](docs/02-active-directory.md)
- [DNS](docs/03-dns.md)
- [DHCP](docs/04-dhcp.md)
- [Partages SMB et permissions NTFS](docs/05-partages-smb-ntfs.md)
- [Stratégies de groupe (GPO)](docs/06-gpo.md)
- [Diagnostic et dépannage](docs/07-diagnostic.md)

## Évolutions prévues

Ce laboratoire est un projet personnel en cours d'évolution. Les prochaines étapes envisagées sont :

- Approfondissement de l'administration Windows Server.
- Mise en place et validation de procédures de sauvegarde et de restauration.
- Déploiement de services Linux.
- Analyse des journaux système.
- Mise en place d'outils de supervision et de détection de sécurité.
