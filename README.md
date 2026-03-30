## écurité IoT MQTT :- Vulnérabilités et mitigations

| Vulnérabilité | Risque associé | Mitigation mise en place |
| :--- | :--- | :--- |
| **Pas d'authentification** | Accès anonyme sur le broker | [cite_start]Désactivation de l'anonymat (`allow_anonymous false`) et authentification par mot de passe[cite: 133]. |
| **MQTT en clair** | Interception des données (MITM) | [cite_start]Chiffrement des flux via TLS sur le port 8883[cite: 133]. |
| **Topics permissifs** | Injection de fausses données | [cite_start]Mise en place de règles ACL restrictives par utilisateur et par topic[cite: 133]. |

[cite_start]**Principaux challenges de mise en œuvre :** [cite: 132]
La gestion complexe du cycle de vie des certificats (génération, déploiement, révocation) sur des parcs d'appareils étendus, ainsi que les capacités de calcul et de batterie parfois limitées des petits objets IoT pour gérer le chiffrement.

---

## Réponses aux questions

* [cite_start]**Quels risques si MQTT n'est pas sécurisé ?** [cite: 146]
  [cite_start]Le système s'expose à des fuites de données privées, à l'injection de commandes malveillantes pouvant altérer le fonctionnement du système, et augmente drastiquement la surface d'attaque globale de l'infrastructure[cite: 56, 146].

* [cite_start]**Quelle est la différence entre TLS et mTLS ?** [cite: 147]
  * **TLS classique :** Authentification unilatérale. Seul le serveur prouve son identité au client (via son certificat).
  * **mTLS (Mutual TLS) :** Authentification bilatérale. Le serveur s'authentifie, et le client doit **également** présenter un certificat valide pour avoir le droit de se connecter.

* [cite_start]**Pourquoi utiliser des ACL (Access Control Lists) ?** [cite: 148]
  [cite_start]Pour appliquer le contrôle d'accès par topic et le principe du moindre privilège[cite: 120]. [cite_start]Ainsi, si un objet spécifique est compromis, il ne pourra ni lire les données des autres capteurs, ni écrire sur des topics critiques auxquels il n'est pas censé avoir accès[cite: 120, 148].
