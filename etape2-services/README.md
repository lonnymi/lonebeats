# Étape 2 : services et commandes

Une **commande** est une demande de traitement envoyée par un utilisateur à un service. Elle exprime une intention (« publier », « acheter ») et peut être refusée, par exemple si le beat n'est plus disponible.

| Service | Commandes | Fichier |
|---|---|---|
| Catalogue | `PublierBeat`, `ModifierPrixBeat`, `RetirerBeat` | [catalogue.commandes.json](catalogue.commandes.json) |
| Vente | `AcheterLicence`, `ConsulterMesAchats` | [vente.commandes.json](vente.commandes.json) |

Le service Statistiques ne reçoit aucune commande : il est alimenté uniquement par des événements (voir l'étape 6).
