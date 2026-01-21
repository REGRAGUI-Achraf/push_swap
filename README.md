# Push Swap

## 📚 Concept

**                              Push Swap             ** est un projet d'algorithmique qui consiste à trier une pile de nombres entiers en utilisant un ensemble limité d'instructions et en minimisant le nombre d'opérations.

### Les Structures de Données

Le programme utilise deux piles :
- **Stack A** : contient initialement tous les nombres à trier
- **Stack B** : vide au départ, sert de zone de stockage temporaire

### Les Opérations Autorisées

| Opération | Description |
|-----------|-------------|
| `sa` | Swap A - Échange les 2 premiers éléments de la pile A |
| `sb` | Swap B - Échange les 2 premiers éléments de la pile B |
| `ss` | Swap A et B simultanément |
| `pa` | Push A - Déplace le premier élément de B vers le sommet de A |
| `pb` | Push B - Déplace le premier élément de A vers le sommet de B |
| `ra` | Rotate A - Le premier élément devient le dernier |
| `rb` | Rotate B - Le premier élément devient le dernier |
| `rr` | Rotate A et B simultanément |
| `rra` | Reverse Rotate A - Le dernier élément devient le premier |
| `rrb` | Reverse Rotate B - Le dernier élément devient le dernier |
| `rrr` | Reverse Rotate A et B simultanément |

### Objectif

À la fin de l'algorithme :
- Stack A doit contenir tous les nombres triés en ordre croissant
- Stack B doit être vide
- Le nombre d'opérations doit être minimal

---

## 🔧 L'Algorithme de Shanks

L'algorithme de **Shanks** (aussi appelé **Chunk Sort** ou **Range Sort**) est une approche efficace pour trier de grandes quantités de nombres dans Push Swap.

### Principe de Base

L'algorithme divise l'ensemble des nombres en plusieurs **chunks** (groupes) de taille similaire, puis pousse ces chunks de Stack A vers Stack B par ordre croissant d'index, avant de les repousser vers A dans l'ordre décroissant.

### Étapes de l'Algorithme

#### 1. **Indexation**
Les nombres sont d'abord indexés de 0 à n-1 selon leur position dans l'ordre trié final.

Exemple : `[5, 2, 8, 1]` → indices : `[2, 1, 3, 0]`

#### 2. **Détermination du Nombre de Chunks**
```
• Pour 100 nombres : 5 chunks (20 nombres par chunk)
• Pour 500 nombres : 11 chunks (~45 nombres par chunk)
```

#### 3. **Push vers Stack B par Chunks**
Pour chaque chunk (du plus petit au plus grand) :
1. Rechercher les nombres appartenant au chunk actuel dans Stack A
2. Les déplacer vers le sommet de Stack A (rotation optimale)
3. Les pousser vers Stack B (`pb`)
4. Optimiser la position dans Stack B en utilisant `rb` ou `rrb`

**Optimisation** : On place les plus petits indices en bas de Stack B et les plus grands en haut.

#### 4. **Push vers Stack A (tri final)**
Répéter jusqu'à ce que Stack B soit vide :
1. Trouver le plus grand nombre dans Stack B
2. Le déplacer au sommet avec rotation optimale (`rb` ou `rrb`)
3. Le pousser vers Stack A (`pa`)

### Exemple Visuel

```
Début:
A: [5, 2, 8, 1, 9, 3]
B: []

Après indexation:
A: [3, 1, 5, 0, 6, 2]  (indices)
B: []

Chunk 0 (indices 0-1):
A: [3, 5, 6, 2]
B: [1, 0]

Chunk 1 (indices 2-3):
A: [5, 6]
B: [1, 0, 2, 3]

Chunk 2 (indices 4-6):
A: []
B: [1, 0, 2, 3, 5, 6]

Push back (du plus grand au plus petit):
A: [0, 1, 2, 3, 5, 6]  → Trié!
B: []
```

### Avantages de Shanks

✅ **Efficacité** : Complexité O(n log n) en moyenne  
✅ **Scalabilité** : Fonctionne bien avec de grandes piles (100-500 éléments)  
✅ **Prévisibilité** : Nombre d'opérations relativement constant  
✅ **Simplicité** : Logique claire et facile à implémenter  

### Optimisations Possibles

1. **Calcul intelligent des rotations** : Choisir entre `ra`/`rra` selon la distance
2. **Dual rotation** : Utiliser `rr` et `rrr` quand les deux stacks doivent tourner
3. **Ajustement dynamique des chunks** : Adapter la taille selon la distribution
4. **Pre-sorting** : Détecter les séquences déjà triées

---

## 🎯 Benchmark

Pour respecter les contraintes du projet 42 :

| Taille | Opérations Max | Shanks Moyen |
|--------|----------------|--------------|
| 3 | 3 | 2-3 |
| 5 | 12 | 8-12 |
| 100 | 700 | 550-650 |
| 500 | 5500 | 4500-5000 |

---

## 🚀 Compilation et Utilisation

```bash
# Compilation
make

# Exécution
./push_swap 4 67 3 87 23

# Vérification avec checker
./push_swap 4 67 3 87 23 | ./checker 4 67 3 87 23
```

---

## 📖 Ressources

- [Push Swap Visualizer](https://github.com/o-reo/push_swap_visualizer)
- [Algorithme de tri](https://medium.com/@jamierobertdawson/push-swap-the-least-amount-of-moves-with-two-stacks-d1e76a71789a)

---

**Auteur** : aregragu  
**Date** : Janvier 2026
