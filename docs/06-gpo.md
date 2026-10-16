# Stratégies de groupe (GPO)

## Présentation du service

Les stratégies de groupe (Group Policy Objects ou GPO) permettent de centraliser la configuration des utilisateurs et des ordinateurs d'un domaine Active Directory.

Dans ce laboratoire, elles sont utilisées pour configurer automatiquement les lecteurs réseau accessibles aux utilisateurs selon leur service.

## Environnement

- **Contrôleur de domaine :** `SRV001`
- **Domaine :** `lab.local`
- **Partages réseau :** Administration, Compta, Direction et IT
- **Outil d'administration :** Gestion de stratégie de groupe (GPMC)

## Configuration réalisée

### Création des GPO

Des stratégies de groupe ont été créées pour gérer le mappage des lecteurs réseau.

- `Mappage lecteurs reseau Administration`
- `Mappage lecteurs reseau Compta`
- `Mappage lecteurs reseau Direction`
- `Mappage lecteurs reseau IT`

La création d'une GPO ne suffit pas à son application. Elle doit être liée à un domaine ou à une unité d'organisation appropriée et respecter les conditions de filtrage et d'application.

### Mappage des lecteurs réseau

Les lecteurs réseau sont associés aux partages SMB hébergés sur SRV001.

- **Administration :** lecteur `W:` vers `\\SRV001\Administration`.
- **Compta :** lecteur `X:` vers `\\SRV001\Compta`.
- **Direction :** lecteurs `W:`, `X:` et `Y:` vers les partages Administration, Compta et Direction.
- **IT :** lecteurs `W:`, `X:`, `Y:` et `Z:` vers les partages Administration, Compta, Direction et IT.

Ces mappages permettent aux utilisateurs d'accéder aux ressources réseau correspondant à leur configuration.

## Application des stratégies

L'application d'une GPO dépend notamment de son emplacement de liaison, de son filtrage de sécurité et de la portée de ses paramètres.

Les groupes de sécurité et les unités d'organisation permettent d'organiser les utilisateurs et de cibler les stratégies selon les besoins du laboratoire.

La présence d'une GPO dans la console de gestion ne garantit pas qu'elle soit appliquée à un utilisateur.

## Tests et validation

Les vérifications ont été réalisées depuis les postes clients.

- `gpresult /r` : consultation des stratégies de groupe appliquées à l'utilisateur et à l'ordinateur.
- `gpupdate /force` : actualisation des stratégies de groupe.
- Vérification de la présence des lecteurs réseau dans l'explorateur de fichiers.
- Tests d'accès aux partages mappés.

Un chemin réseau incorrect a été identifié dans la configuration d'un lecteur et corrigé afin de rétablir le mappage attendu.

## Résultats obtenus

- Création de GPO dédiées au mappage des lecteurs réseau.
- Configuration de lecteurs selon les besoins des services.
- Vérification de l'application effective des stratégies.
- Validation des accès aux partages depuis un compte utilisateur du domaine.

