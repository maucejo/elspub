# v1.0.2

## Workaround pour `math.equation`

Ce workaround empêche l'indentation du premier paragraphe après une équation mathématique.

**Fonctionnement :**

1. **Marquage des équations** : Ajoute un label invisible `<eq-end>` à la fin de chaque équation
   ```typst
   show math.equation: it => it + [#[ #[]<eq-end>]]
   ```

2. **Marquage des sauts de paragraphes** : Ajoute un label `<eq-parbreak>` pour chaque saut de paragraphe explicite

3. **Logique conditionnelle** : Lors de l'affichage d'un paragraphe (`show par`) :
   - Cherche le dernier `<eq-end>` avant le paragraphe
   - Vérifie si ce label est immédiatement avant le début du paragraphe (même position)
   - Contrôle s'il y a un saut de paragraphe explicite après l'équation
   - Si pas de saut explicite → reconstruit le paragraphe **sans indentation**
   - Si saut explicite → conserve l'indentation normale (choix intentionnel de l'utilisateur)

**Résumé** : Détecte automatiquement les équations suivies immédiatement par du texte et supprime l'indentation, sauf si l'utilisateur crée explicitement un saut de paragraphe. 