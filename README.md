# TP MQTT

## 1. Vulnérabilités et mitigations

| Vulnerabilite | Risque | Mitigation |
| :--- | :--- | :--- |
| Pas d'auth | Accès anonyme | allow_anonymous false |
| MQTT clair | MITM (Interception) | TLS 8883 |
| Topics permissifs | Injection | ACL user/topic |

Principaux obstacles à la mise en oeuvre :
La puissance de calcul limitee des petits objets connectes et la complexite de gestion du cycle de vie des certificats sur un grand nombre d'appareils.

## 2. Réponses aux questions

Quels risques si MQTT non securise ?
Vol de donnees sensibles, ecoute du trafic reseau et prise de controle des equipements par injection de commandes malveillantes.

Difference TLS / mTLS ?
En TLS classique, seul le serveur prouve son identite. En mTLS, le serveur et le client doivent tous les deux prouver leur identite avec un certificat valide.

Pourquoi utiliser des ACL ?
Pour appliquer le principe de moindre privilege. Cela garantit qu'un utilisateur ou un objet ne peut lire et ecrire que sur les topics qui le concernent strictement, limitant ainsi l'impact en cas de piratage d'un capteur.

## 3. Validation des tests de sécurité

Preuve de fonctionnement du chiffrement TLS et de l'authentification 
:
Commande lancée : mosquitto_pub -p 8883 --cafile server.crt -u user1 -P password -t test -m 'tls'
Résultat obtenu : Le message a bien ete publie de maniere chiffree sans erreur de connexion.
