# DNS (Domain Name System)

## Présentation du service

Le DNS permet de traduire les noms de domaine en adresses IP et de localiser les services du réseau.

Dans ce laboratoire, le service DNS est hébergé sur SRV001. Il est utilisé par Active Directory et par les postes clients pour résoudre les noms des machines et des services.

## Environnement

- **Serveur DNS :** `SRV001`
- **Adresse IP du serveur DNS :** `192.168.2.1`
- **Domaine Active Directory :** `lab.local`
- **Zone de test :** `test.local`
- **Redirecteurs DNS :** `1.1.1.1` et `8.8.8.8`

## Configuration réalisée

### Zone de recherche directe

Une zone de recherche directe permet de retrouver une adresse IP à partir d'un nom DNS.

La zone de test `test.local` a été créée pour pratiquer la gestion des enregistrements DNS.

Les enregistrements configurés sont :

- **Enregistrement A :** `serveur-test.test.local` associé à `192.168.2.1`.
- **Enregistrement CNAME :** `web.test.local` associé au nom `serveur-test.test.local`.

L'enregistrement A associe un nom à une adresse IPv4. Le CNAME permet d'utiliser un nom alternatif pour désigner un autre nom DNS.

### Zone de recherche inversée

Une zone de recherche inversée permet de retrouver un nom DNS à partir d'une adresse IP.

La zone de recherche inversée configurée est :

- **Zone :** `2.168.192.in-addr.arpa`
- **Enregistrement PTR :** adresse `192.168.2.1` associée à `SRV001.lab.local`.

L'enregistrement PTR permet d'associer une adresse IP à un nom DNS.

### Redirecteurs DNS

Les redirecteurs permettent au serveur DNS de transmettre les requêtes qu'il ne peut pas résoudre localement à d'autres serveurs DNS.

Les redirecteurs configurés sont :

- `1.1.1.1`
- `8.8.8.8`

Ils permettent notamment de résoudre des noms de domaine externes, comme `google.com`.

## Tests et validation

Les tests ont été réalisés avec `nslookup`.

- **Résolution d'un nom externe :** `nslookup google.com`
- **Interrogation d'un serveur DNS externe :** `nslookup google.com 8.8.8.8`
- **Test d'un nom de la zone locale auprès d'un DNS externe :** `nslookup serveur-test.test.local 8.8.8.8`

Les tests de résolution de `google.com` ont réussi.

La requête portant sur `serveur-test.test.local` auprès de `8.8.8.8` a renvoyé une réponse `NXDOMAIN`. Ce résultat est attendu, car ce nom appartient à une zone de test locale qui n'est pas publiée sur le DNS public.

## Diagnostic et notions importantes

- **Zone de recherche directe :** résolution d'un nom vers une adresse IP.
- **Zone de recherche inversée :** résolution d'une adresse IP vers un nom.
- **Enregistrement A :** association d'un nom à une adresse IPv4.
- **Enregistrement CNAME :** création d'un alias DNS.
- **Enregistrement PTR :** association d'une adresse IP à un nom DNS.
- **Redirecteur DNS :** transmission des requêtes à un autre serveur DNS.

Le DNS est essentiel au fonctionnement d'Active Directory. Les postes clients doivent utiliser le DNS interne pour localiser correctement les services du domaine `lab.local`.

## Résultats obtenus

- Création et configuration d'une zone DNS de test.
- Gestion des enregistrements A, CNAME et PTR.
- Configuration des redirecteurs DNS.
- Vérification de la résolution des noms avec `nslookup`.
- Compréhension de la différence entre résolution DNS locale et résolution DNS publique.

