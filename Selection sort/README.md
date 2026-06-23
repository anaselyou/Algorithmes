# Selection Sort / Tri par Sélection

Algorithme de tri qui trouve le plus petit élément à chaque passage et le place dans un nouveau tableau → O(n²)

## Pseudocode

```
fonction trouverLePlusPetit(tableau):
    plusPetit = tableau[0]           // on suppose que le premier est le plus petit
    indicePlusPetit = 0              // on mémorise son indice

    pour i de 1 à longueur(tableau):
        si tableau[i] < plusPetit:
            plusPetit = tableau[i]   // on a trouvé un plus petit
            indicePlusPetit = i      // on met à jour l'indice

    retourner indicePlusPetit        // on retourne l'indice, pas la valeur


fonction triParSelection(tableau):
    nouveauTableau = []              // tableau vide qui contiendra le résultat trié

    pour i de 0 à longueur(tableau):
        indicePlusPetit = trouverLePlusPetit(tableau)    // on trouve le plus petit
        nouveauTableau.ajouter(tableau[indicePlusPetit]) // on l'ajoute au résultat
        tableau.supprimer(indicePlusPetit)               // on le retire du tableau original

    retourner nouveauTableau
```

## Implémentation C#

```csharp
// Trouve l'indice du plus petit élément dans le tableau
int TrouverLePlusPetit(List<int> tableau)
{
    int plusPetit = tableau[0];      // on suppose que le premier est le plus petit
    int indicePlusPetit = 0;         // on mémorise son indice

    for (int i = 1; i < tableau.Count; i++)
    {
        if (tableau[i] < plusPetit)  // si on trouve un élément plus petit
        {
            plusPetit = tableau[i];  // on met à jour le plus petit
            indicePlusPetit = i;     // on met à jour son indice
        }
    }

    return indicePlusPetit;          // on retourne l'indice, pas la valeur
}

// Trie un tableau du plus petit au plus grand
List<int> TriParSelection(List<int> tableau)
{
    List<int> nouveauTableau = new List<int>(); // tableau vide pour le résultat

    int nombreElements = tableau.Count;         // on mémorise la taille initiale

    for (int i = 0; i < nombreElements; i++)
    {
        int indicePlusPetit = TrouverLePlusPetit(tableau); // on trouve le plus petit
        nouveauTableau.Add(tableau[indicePlusPetit]);       // on l'ajoute au résultat
        tableau.RemoveAt(indicePlusPetit);                  // on le retire du tableau original
    }

    return nouveauTableau;
}

// Test
List<int> tableau = new List<int> { 5, 3, 6, 2, 10 };
List<int> resultat = TriParSelection(tableau);

Console.WriteLine(string.Join(", ", resultat)); // affiche : 2, 3, 5, 6, 10
```

## Complexité

| Cas | Complexité |
|-----|------------|
| Pire cas | O(n²) |
| Meilleur cas | O(n²) |

**Pourquoi O(n²) ?** Pour chaque élément (n passages), on parcourt tout le tableau pour trouver le plus petit (n opérations) → n × n = n²

**Exemple :** 5 éléments → on cherche le plus petit 5 fois en parcourant jusqu'à 5 éléments à chaque fois → 25 opérations maximum
