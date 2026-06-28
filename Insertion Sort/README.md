# Insertion Sort / Tri par Insertion

Algorithme de tri qui fonctionne comme trier des cartes dans la main — on prend chaque élément et on l'insère à la bonne position dans la partie déjà triée.

## Principe

```
[5, 3, 8, 1]
→ prend 3, l'insère avant 5  : [3, 5, 8, 1]
→ prend 8, déjà bien placé   : [3, 5, 8, 1]
→ prend 1, l'insère au début : [1, 3, 5, 8] ✅
```

## Pseudocode

```
fonction insertionSort(tableau):
    pour i de 1 à longueur(tableau):
        elementActuel = tableau[i]    // élément à insérer
        j = i - 1                     // on part de l'élément précédent

        // on décale les éléments plus grands vers la droite
        tant que j >= 0 et tableau[j] > elementActuel:
            tableau[j + 1] = tableau[j]  // décale vers la droite
            j = j - 1

        tableau[j + 1] = elementActuel   // on insère au bon endroit

    retourner tableau
```

## Implémentation C#

```csharp
// Trie un tableau en ordre croissant
// Principe    : on prend chaque élément et on l'insère à la bonne position
// Cas de base : liste vide ou 1 élément → déjà trié
// Complexité  : O(n) meilleur cas (déjà trié), O(n²) cas moyen et pire cas
// Avantage    : très rapide sur petites listes → utilisé par Introsort (Array.Sort C#) sous 16 éléments
static int[] InsertionSort(int[] tableau)
{
    for (int i = 1; i < tableau.Length; i++)
    {
        int elementActuel = tableau[i]; // élément à insérer
        int j = i - 1;                 // on part de l'élément précédent

        // on décale les éléments plus grands vers la droite
        while (j >= 0 && tableau[j] > elementActuel)
        {
            tableau[j + 1] = tableau[j]; // décale vers la droite
            j--;
        }

        tableau[j + 1] = elementActuel; // on insère au bon endroit
    }

    return tableau;
}

// Test
int[] tableau = { 5, 3, 8, 1 };
int[] resultat = InsertionSort(tableau);
Console.WriteLine(string.Join(", ", resultat)); // affiche : 1, 3, 5, 8
```

## Ce qui se passe avec `[5, 3, 8, 1]`

```
Départ   : [5, 3, 8, 1]

i = 1 → elementActuel = 3
  tableau[0] = 5 > 3 → décale : [5, 5, 8, 1]
  insère 3 à j+1 = 0 : [3, 5, 8, 1]

i = 2 → elementActuel = 8
  tableau[1] = 5 < 8 → pas de décalage
  insère 8 à j+1 = 2 : [3, 5, 8, 1]

i = 3 → elementActuel = 1
  tableau[2] = 8 > 1 → décale : [3, 5, 8, 8]
  tableau[1] = 5 > 1 → décale : [3, 5, 5, 8]
  tableau[0] = 3 > 1 → décale : [3, 3, 5, 8]
  insère 1 à j+1 = 0 : [1, 3, 5, 8] ✅
```

## Complexité

| Cas | Complexité | Quand |
|-----|------------|-------|
| Meilleur cas | O(n) | Liste déjà triée — aucun décalage nécessaire |
| Cas moyen | O(n²) | Données aléatoires |
| Pire cas | O(n²) | Liste triée à l'envers |

## Comparaison avec Selection Sort

| | Insertion Sort | Selection Sort |
|---|---|---|
| Meilleur cas | **O(n)** | O(n²) |
| Cas moyen | O(n²) | O(n²) |
| Utilisé en prod | ✅ Introsort < 16 éléments | ❌ jamais |
| Stable | ✅ | ❌ |

**Stable** = deux éléments égaux gardent leur ordre relatif après le tri.

## Pourquoi c'est important

Malgré son O(n²) en moyenne, Insertion Sort est **utilisé par `Array.Sort()` en C#** pour les listes de moins de 16 éléments car sa constante est très petite — moins d'overhead que Quicksort sur les très petites listes.
