# DHCP (Dynamic Host Configuration Protocol)

## Présentation du service

Le DHCP permet d'attribuer automatiquement une configuration réseau aux postes clients, notamment une adresse IP, un masque de sous-réseau et les paramètres DNS.

Dans ce laboratoire, le service DHCP est hébergé sur SRV001 et distribue des adresses IP aux machines du réseau interne.

## Environnement

- **Serveur DHCP :** `SRV001`
- **Adresse IP du serveur :** `192.168.2.1`
- **Réseau interne :** `192.168.2.0/24`
- **Masque de sous-réseau :** `255.255.255.0`
- **Plage DHCP :** `192.168.2.200` à `192.168.2.220`
- **Domaine Active Directory :** `lab.local`

## Configuration réalisée

### Étendue DHCP

Une étendue DHCP a été configurée pour attribuer automatiquement des adresses IP aux postes clients du réseau interne.

- Définition de la plage d'adresses distribuées.
- Configuration du masque de sous-réseau.
- Gestion des exclusions et des réservations d'adresses IP.

### Options DHCP

Les options DHCP transmettent aux clients les paramètres nécessaires à leur configuration réseau.

- **Option 006 :** serveur DNS `192.168.2.1`.
- **Option 015 :** nom de domaine DNS `lab.local`.

Le serveur DNS interne permet aux clients de résoudre les noms du domaine Active Directory.

Aucune passerelle interne n'est distribuée par DHCP, car SRV001 n'est pas configuré comme routeur entre le réseau interne et le réseau externe.

### Autorisation du serveur DHCP

Le serveur DHCP a été autorisé dans Active Directory.

- **Nom du serveur :** `SRV001.lab.local`
- **Adresse IP :** `192.168.2.1`

Cette autorisation permet de contrôler les serveurs DHCP autorisés dans le domaine.

## Tests et validation

Les commandes suivantes permettent de vérifier la configuration réseau depuis un poste client.

- `ipconfig /all` : consultation de l'adresse IP, du masque, de la passerelle, du serveur DHCP et des DNS.
- `ipconfig /release` : libération du bail DHCP.
- `ipconfig /renew` : demande d'un nouveau bail DHCP.
- `ping 192.168.2.1` : test de connectivité vers le serveur interne.

Les vérifications permettent de s'assurer que le client reçoit une adresse IP adaptée au réseau interne et utilise le serveur DNS attendu.

## Résultats obtenus

- Configuration d'une étendue DHCP.
- Définition des options DNS et du domaine.
- Autorisation du serveur DHCP dans Active Directory.
- Vérification de la configuration réseau des clients.

## Notions importantes

- **Étendue DHCP :** plage d'adresses IP pouvant être attribuées aux clients.
- **Bail DHCP :** attribution temporaire d'une adresse IP à un client.
- **Réservation DHCP :** attribution d'une adresse déterminée à un équipement identifié.
- **Option 006 :** adresse du serveur DNS.
- **Option 015 :** suffixe de domaine DNS.

