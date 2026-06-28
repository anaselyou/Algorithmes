# Binary Search / Recherche Binaire

Algorithme de recherche sur liste **triée**. Au lieu de parcourir chaque élément un par un, on divise la liste en deux à chaque étape — on élimine la moitié des éléments à chaque fois.

**Condition obligatoire : la liste doit être triée.**

## Principe

```
Liste : [1, 3, 5, 7, 9]   On cherche : 3

Étape 1 : milieu = 5 → trop grand → on cherche à gauche
Étape 2 : milieu = 1 → trop petit → on cherche à droite
Étape 3 : milieu = 3 → trouvé ✅ en 3 étapes
```

Sans recherche binaire → on aurait parcouru jusqu'à 5 éléments.

## Pseudocode

```
fonction recherche_binaire(liste, cible):
    bas = 0                        // on commence au début
    haut = longueur(liste) - 1     // on finit à la fin

    tant que bas <= haut:          // tant qu'il reste des éléments à examiner
        milieu = (bas + haut) / 2  // on prend l'élément du milieu
        supposition = liste[milieu]

        si supposition == cible → retourner milieu    // trouvé ✅
        si supposition > cible  → haut = milieu - 1  // trop grand → cherche à gauche
        sinon                   → bas = milieu + 1   // trop petit → cherche à droite

    retourner null   // non trouvé
```

## Implémentation C#

```csharp
// Recherche un élément dans un tableau trié — version itérative
// Condition   : le tableau DOIT être trié, sinon résultat imprévisible
// Complexité  : O(log n) pire cas, O(1) meilleur cas (élément au milieu dès le 1er coup)
int RechercherBinaire(int[] liste, int cible)
{
    int bas = 0;                   // indice de début
    int haut = liste.Length - 1;   // indice de fin
    int compteur = 0;              // compteur d'étapes

    while (bas <= haut)            // tant qu'il reste des éléments à examiner
    {
        compteur++;
        int milieu = (bas + haut) / 2;   // indice du milieu
        int supposition = liste[milieu]; // valeur au milieu

        // Condition de sortie 1 — trouvé
        if (supposition == cible)
        {
            Console.WriteLine($"Trouvé en {compteur} étapes");
            return milieu; // retourne l'indice de l'élément
        }

        // Supposition trop grande → on cherche dans la moitié gauche
        if (supposition > cible)
            haut = milieu - 1;

        // Supposition trop petite → on cherche dans la moitié droite
        else
            bas = milieu + 1;
    }

    // Condition de sortie 2 — bas > haut, plus rien à examiner
    Console.WriteLine($"Non trouvé en {compteur} étapes");
    return -1;
}

// Test
int[] maListe = { 1, 3, 5, 7, 9 };
RechercherBinaire(maListe, 3);  // Trouvé en 2 étapes
RechercherBinaire(maListe, -1); // Non trouvé en 3 étapes
```

## Ce qui se passe avec `[1, 3, 5, 7, 9]`, on cherche `3`

```
Départ : bas = 0, haut = 4

Étape 1 : milieu = 2 → supposition = 5 → trop grand → haut = 1
Étape 2 : milieu = 0 → supposition = 1 → trop petit → bas = 1
Étape 3 : milieu = 1 → supposition = 3 → trouvé ✅ à l'indice 1
```

## Complexité

| Cas | Complexité | Quand |
|-----|------------|-------|
| Meilleur cas | O(1) | L'élément tombe pile au milieu dès le 1er coup |
| Pire cas | O(log n) | Élément aux extrémités ou inexistant |

**Pourquoi O(log n) ?**
À chaque étape on divise par 2 — la question posée par log₂(n) est :
*"Combien de fois dois-je diviser n par 2 pour arriver à 1 ?"*

| n | log₂(n) | Étapes max |
|---|---------|------------|
| 1 024 | 10 | 10 étapes |
| 100 000 | ~17 | 17 étapes |
| 1 000 000 | ~20 | 20 étapes |
| 1 000 000 000 | ~30 | 30 étapes |

**1 milliard d'éléments → 30 étapes maximum.** C'est la puissance de O(log n).

## Comparaison avec la recherche simple

| | Recherche simple | Recherche binaire |
|---|---|---|
| Liste triée requise | ❌ | ✅ obligatoire |
| Complexité | O(n) | O(log n) |
| 1 024 éléments | 1 024 étapes | 10 étapes |
| 1 milliard éléments | 1 000 000 000 étapes | 30 étapes |

## Calcul rapide sur calculette

Pour calculer log₂(n) sur n'importe quelle calculette :
```
log(n) ÷ log(2)
```
Exemple : log(1024) ÷ log(2) = **10** ✅
