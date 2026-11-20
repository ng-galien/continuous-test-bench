# continuous-test-bench

Banc de test continu piloté par des agents.

## Principe

Un agent vérifie un parcours dans le navigateur. Quand il conclut que le comportement est correct, ses actions et les
mesures observées sont enregistrées : cet enregistrement est la référence du parcours.

Après un changement de code, le parcours est rejoué et comparé à sa référence :

- un écart validé remplace la référence ;
- un écart non validé est une régression.

Un parcours est une suite de paires (action, mesures). L'action est sémantique (« cliquer sur le bouton Exporter »).
Les mesures sont prises juste après l'action : structure du DOM visible, textes, requêtes réseau, erreurs console,
traces côté serveur.

Les mesures se rangent en trois classes :

| Classe | Exemples | Traitement d'un écart |
| --- | --- | --- |
| Invariant strict | erreur console, texte manquant, requête en échec | signalé |
| Budget | nombre de requêtes, latence, hauteur de page | signalé au-delà d'une tolérance |
| Volatile | dates, identifiants, ordre d'éléments non triés | ignoré |

## Contenu du dépôt

- Le banc : enregistrement d'un parcours, stockage dans PostgreSQL, rejeu, comparaison à la référence.
- Un projet de test simple : une petite application (liste, formulaire, page de détail, API, base) sur laquelle le banc
  se met au point.

## Statut

Exploration. La valeur du principe se mesure sur un premier parcours : temps et tokens de réalignement, comparés au
même parcours écrit en test Playwright classique.
