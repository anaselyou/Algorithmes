# Quicksort / Tri rapide

Algorithme de tri récursif basé sur le principe **Diviser pour Mieux Régner (D&C)**.
On choisit un pivot, on divise le tableau en deux sous-tableaux, on trie récursivement chaque partie.

## Pseudocode

```
fonction quicksort(tableau):

    // Cas de base — tableau vide ou 1 élément, déjà trié
    si longueur(tableau) < 2 → retourner tableau

    // Cas récursif
    pivot = tableau[0]                                        // on prend le premier élément comme pivot

    moinsPetit  = [i pour i dans tableau[1:] si i <= pivot]  // éléments inférieurs ou égaux au pivot
    plusGrand   = [i pour i dans tableau[1:] si i > pivot]   // éléments supérieurs au pivot

    retourner quicksort(moinsPetit) + [pivot] + quicksort(plusGrand)
```

## Implémentation C#

```csharp
// Trie un tableau en ordre croissant via le principe D&C
// Cas de base  : tableau vide ou 1 élément → déjà trié, on retourne directement
// Cas récursif : on choisit un pivot, on crée deux sous-tableaux, on trie récursivement
// Complexité   : O(n log n) en moyenne, O(n²) dans le pire cas (pivot toujours le plus petit/grand)
// Note         : pivot = premier élément — risque O(n²) si liste déjà triée
static List<int> Quicksort(List<int> tableau)
{
    // Cas de base — tableau vide ou 1 élément
    if (tableau.Count < 2)
        return tableau;

    // Pivot = premier élément
    int pivot = tableau[0];

    // Sous-tableau des éléments inférieurs ou égaux au pivot
    List<int> moinsPetit = tableau.Skip(1).Where(i => i <= pivot).ToList();

    // Sous-tableau des éléments supérieurs au pivot
    List<int> plusGrand = tableau.Skip(1).Where(i => i > pivot).ToList();

    // Récursion : trie gauche + pivot + trie droite
    List<int> resultat = Quicksort(moinsPetit);
    resultat.Add(pivot);
    resultat.AddRange(Quicksort(plusGrand));

    return resultat;
}

// Test
List<int> tableau = new List<int> { 10, 5, 2, 3 };
List<int> trie = Quicksort(tableau);
Console.WriteLine(string.Join(", ", trie)); // affiche : 2, 3, 5, 10
```

## Ce qui se passe avec `[10, 5, 2, 3]`

```
Quicksort([10, 5, 2, 3])
  pivot = 10
  moinsPetit = [5, 2, 3]
  plusGrand  = []

  Quicksort([5, 2, 3])
    pivot = 5
    moinsPetit = [2, 3]
    plusGrand  = []

    Quicksort([2, 3])
      pivot = 2
      moinsPetit = []
      plusGrand  = [3]

      Quicksort([])  → [] ← cas de base ✅
      Quicksort([3]) → [3] ← cas de base ✅

    retourne [] + [2] + [3] = [2, 3]
  retourne [2, 3] + [5] + [] = [2, 3, 5]
retourne [2, 3, 5] + [10] + [] = [2, 3, 5, 10] ✅
```

## Complexité

| Cas | Complexité | Quand |
|-----|------------|-------|
| Meilleur cas | O(n log n) | pivot tombe toujours au milieu |
| Cas moyen | O(n log n) | pivot aléatoire |
| Pire cas | O(n²) | pivot toujours le plus petit ou grand (liste déjà triée) |

**Pourquoi O(n log n) en moyenne ?**
- **n** éléments à traiter à chaque niveau
- **log n** niveaux de division
- → n × log n opérations

**Stratégies de pivot :**
- `tableau[0]` → simple mais dangereux sur liste triée
- Aléatoire → évite le pire cas
- Médiane de 3 → meilleur compromis, utilisé par `Array.Sort()` en C#
