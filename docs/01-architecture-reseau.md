# Architecture réseau du laboratoire

## Présentation du projet

Cette documentation présente l'architecture réseau du laboratoire Windows Server 2025 virtualisé avec Oracle VirtualBox.

L'objectif est de comprendre l'organisation des machines virtuelles, la configuration des interfaces réseau et les communications entre le serveur et les postes clients.

## Environnement réseau

- **Hyperviseur :** Oracle VirtualBox
- **Serveur principal :** `SRV001`
- **Nom de domaine :** `lab.local`
- **Réseau interne :** `192.168.2.0/24`
- **Masque de sous-réseau :** `255.255.255.0`
- **Adresse IP interne du serveur :** `192.168.2.1`
- **Plage DHCP :** `192.168.2.200` à `192.168.2.220`

## Interfaces réseau

### Réseau interne

Le réseau interne permet aux machines virtuelles de communiquer entre elles et d'accéder aux services hébergés sur SRV001.

- Communication entre le serveur et les postes clients.
- Accès aux services Active Directory, DNS et DHCP.
- Accès aux partages réseau selon les permissions configurées.

### Réseau NAT

Le réseau NAT permet aux machines virtuelles d'accéder au réseau externe.

- **Adresse NAT de SRV001 :** `10.0.3.15`
- **Passerelle NAT :** `10.0.3.2`
- **Mode réseau :** NAT VirtualBox

Cette interface est distincte du réseau interne du laboratoire.

## Services réseau

Le serveur SRV001 centralise les principaux services du laboratoire.

- **Active Directory Domain Services (AD DS) :** gestion du domaine, des utilisateurs et des groupes.
- **DNS :** résolution des noms et localisation des services Active Directory.
- **DHCP :** attribution automatique des adresses IP aux postes clients.
- **SMB :** accès aux partages de fichiers sur le réseau.
- **GPO :** application des stratégies de groupe et configuration des lecteurs réseau.

## Configuration et diagnostic

Les outils suivants permettent de vérifier la configuration et le fonctionnement du réseau.

- `ipconfig /all` : consultation des adresses IP, masques, passerelles et serveurs DNS.
- `ping` : test de connectivité entre deux équipements.
- `nslookup` : vérification de la résolution DNS.
- `ipconfig /release` : libération du bail DHCP d'une interface.
- `ipconfig /renew` : demande d'un nouveau bail DHCP.

Les résultats doivent être analysés en tenant compte de l'interface réseau utilisée et du service testé.

## Objectifs de l'architecture

Cette architecture permet de mettre en pratique :

- La configuration IPv4 et le diagnostic réseau.
- La séparation entre réseau interne et accès externe.
- La communication entre les postes clients et le contrôleur de domaine.
- L'utilisation des services DNS et DHCP.
- L'accès contrôlé aux ressources partagées.
