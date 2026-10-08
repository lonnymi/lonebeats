# Étape 3 : agrégats des services

Un **agrégat** regroupe les données qu'un service lit et modifie comme un tout. C'est sa frontière de cohérence : une commande modifie un seul agrégat, de manière atomique.

| Service | Agrégat | Clé | Fichier |
|---|---|---|---|
| Catalogue | `Beat` | `idBeat` | [catalogue.beat.json](catalogue.beat.json) |
| Vente | `Achat` | `idAchat` | [vente.achat.json](vente.achat.json) |

## Choix de découpage

- Les **prix** sont dans l'agrégat `Beat`, car ils sont modifiés avec lui par le producteur.
- Un **achat** est un agrégat séparé. Son cycle de vie est indépendant : il est créé par l'artiste et ne change plus une fois payé.
- L'achat **fige le prix payé** (`prixPaye`). Si le producteur change le prix plus tard, les achats déjà faits ne doivent pas changer.

## Requêtes principales (MongoDB)

```js
// Catalogue : retrouver un beat
db.beats.findOne({ idBeat: "BEAT-12" })

// Vente : achats d'un artiste, du plus récent au plus ancien
db.achats.find({ idArtiste: "ART-7" }).sort({ dateAchat: -1 })
db.achats.createIndex({ idArtiste: 1, dateAchat: -1 })
```
