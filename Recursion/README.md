# Récursion / Recursion

La récursion c'est quand une fonction s'appelle elle-même. Toute fonction récursive doit avoir :
- Un **cas de base** : le problème le plus simple, celui qui arrête la récursion
- Un **cas récursif** : on réduit le problème à chaque appel pour se rapprocher du cas de base

**Astuce** : pour un problème sur un tableau, le cas de base est souvent un tableau vide ou à 1 élément.

---

## 1. Somme d'un tableau

**Complexité : O(n)**

### Pseudocode
```
fonction somme(tableau, index):
    si index == longueur(tableau) → retourner 0    // cas de base : tableau vide
    retourner tableau[index] + somme(tableau, index + 1)  // cas récursif
```

### Implémentation C#
```csharp
// Calcule la somme de tous les éléments d'un tableau
// Cas de base  : index == longueur → retourne 0 (élément neutre de l'addition)
// Cas récursif : élément actuel + somme du reste
// Complexité   : O(n) — un appel par élément
static int Somme(int[] tab, int index = 0)
{
    if (index == tab.Length)
        return 0;

    return tab[index] + Somme(tab, index + 1);
}
```

---

## 2. Compter les éléments d'une liste

**Complexité : O(n)**

### Pseudocode
```
fonction compter(liste, index):
    si index == longueur(liste) → retourner 0    // cas de base : liste vide
    retourner 1 + compter(liste, index + 1)      // cas récursif : +1 par élément
```

### Implémentation C#
```csharp
// Compte le nombre d'éléments dans une liste
// Cas de base  : index == Count → retourne 0
// Cas récursif : 1 + count du reste
// Complexité   : O(n) — un appel par élément
static int Count(List<int> liste, int index = 0)
{
    if (index == liste.Count)
        return 0;

    return 1 + Count(liste, index + 1);
}
```

---

## 3. Maximum d'une liste

**Complexité : O(n)**

### Pseudocode
```
fonction maximum(liste, index):
    si index == longueur(liste) - 1 → retourner liste[index]   // cas de base : 1 élément
    retourner max(liste[index], maximum(liste, index + 1))      // cas récursif
```

### Implémentation C#
```csharp
// Trouve le plus grand élément dans une liste
// Cas de base  : dernier élément → on le retourne directement
// Cas récursif : max entre élément actuel et max du reste
// Complexité   : O(n) — un appel par élément
// Attention    : ne pas retourner 0 comme cas de base → faux si tous les éléments sont négatifs
static int Maximum(List<int> liste, int index = 0)
{
    if (index == liste.Count - 1)
        return liste[index];

    return Math.Max(liste[index], Maximum(liste, index + 1));
}
```

---

## 4. Recherche Binaire Récursive

**Complexité : O(log n)**

### Pseudocode
```
fonction recherche_binaire(liste, cible, bas, haut):

    si bas > haut → retourner -1              // cas de base 1 : non trouvé

    milieu = (bas + haut) / 2
    supposition = liste[milieu]

    si supposition == cible → retourner milieu         // cas de base 2 : trouvé
    si supposition > cible  → recherche(liste, cible, bas, milieu - 1)   // cas récursif : cherche à gauche
    sinon                   → recherche(liste, cible, milieu + 1, haut)  // cas récursif : cherche à droite
```

### Implémentation C#
```csharp
// Recherche binaire récursive sur un tableau trié
// Cas de base 1 : bas > haut → élément non trouvé, retourne -1
// Cas de base 2 : liste[milieu] == cible → trouvé, retourne l'indice
// Cas récursif 1 : supposition trop grande → cherche à gauche
// Cas récursif 2 : supposition trop petite → cherche à droite
// Complexité    : O(log n) — on divise par 2 à chaque appel
// Note          : version itérative préférable en prod (moins de mémoire O(1) vs O(log n))
static int RecherchebinaireRecursive(int[] liste, int cible, int bas, int haut, int count = 0)
{
    // Cas de base 1 — non trouvé
    if (bas > haut)
    {
        Console.WriteLine($"Non trouvé en {count} étapes");
        return -1;
    }

    count++;
    int milieu = (bas + haut) / 2;
    int supposition = liste[milieu];

    // Cas de base 2 — trouvé
    if (supposition == cible)
    {
        Console.WriteLine($"Trouvé en {count} étapes");
        return milieu;
    }

    // Cas récursif 1 — cherche à gauche
    if (supposition > cible)
        return RecherchebinaireRecursive(liste, cible, bas, milieu - 1, count);

    // Cas récursif 2 — cherche à droite
    return RecherchebinaireRecursive(liste, cible, milieu + 1, haut, count);
}
```

---

## Complexité récapitulatif

| Fonction | Complexité temps | Complexité mémoire |
|---|---|---|
| Somme | O(n) | O(n) — une frame par élément |
| Count | O(n) | O(n) — une frame par élément |
| Maximum | O(n) | O(n) — une frame par élément |
| Recherche binaire | O(log n) | O(log n) — une frame par division |

**Note :** toute fonction récursive consomme de la mémoire proportionnellement à la profondeur de la pile. Pour des listes très grandes, préférer la version itérative.
