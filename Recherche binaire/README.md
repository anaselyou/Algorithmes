# Binary Search / Recherche Binaire

Algorithme de recherche sur liste **triée**. Divise la liste en deux à chaque étape → O(log n)

## Pseudocode

```
fonction recherche_binaire(liste, cible):
    bas = 0
    haut = longueur(liste) - 1
    
    tant que bas <= haut:
        milieu = (bas + haut) / 2
        supposition = liste[milieu]
        
        si supposition == cible → retourner milieu
        si supposition > cible → haut = milieu - 1
        sinon → bas = milieu + 1
    
    retourner null
```

## Implémentation C#

```csharp
int BinarySearch(int[] list, int item)
{
    int low = 0;
    int high = list.Length - 1;
    int count = 0;

    while (low <= high)
    {
        count++;
        int mid = (low + high) / 2;
        int guess = list[mid];

        if (guess == item)
        {
            Console.WriteLine($"Trouvé en {count} étapes");
            return mid;
        }

        if (guess > item)
            high = mid - 1;
        else
            low = mid + 1;
    }

    Console.WriteLine($"Non trouvé en {count} étapes");
    return -1;
}
```

## Complexité

| Cas | Complexité |
|-----|------------|
| Pire cas | O(log n) |
| Meilleur cas | O(1) |

**Exemple :** 1024 éléments → 10 étapes max (log₂ 1024 = 10)
