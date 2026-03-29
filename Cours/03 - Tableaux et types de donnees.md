# 03 - Tableaux et types de données

## Les types primitifs

En Java, il y a deux grandes familles de types : les **primitifs** et les **[[01 - Classes et Objets#Créer un objet|objets]]**. Tu connais déjà certains primitifs sans le savoir (on les a utilisés dans [[01 - Classes et Objets]] et [[02 - Constructeurs et this]]).

### Les 8 types primitifs :

| Type | Ce qu'il stocke | Exemple |
|------|----------------|---------|
| `byte` | Petit nombre entier (-128 à 127) | `byte b = 100;` |
| `short` | Nombre entier moyen (-32 768 à 32 767) | `short s = 30000;` |
| `int` | Nombre entier classique | `int age = 20;` |
| `long` | Très grand nombre entier | `long pop = 8000000000L;` |
| `float` | Nombre à virgule (peu précis) | `float pi = 3.14f;` |
| `double` | Nombre à virgule (plus précis) | `double prix = 19.99;` |
| `char` | Un seul caractère | `char lettre = 'A';` |
| `boolean` | Vrai ou faux | `boolean actif = true;` |

### Ceux que tu utiliseras le plus :
- `int` pour les nombres entiers
- `double` pour les nombres à virgule
- `boolean` pour vrai/faux
- `byte` (très important en **Java Card** plus tard, car les cartes à puce communiquent en octets)

---

## Primitif vs Objet

| Primitif | Objet |
|----------|-------|
| `int`, `double`, `boolean`... | `String`, `Voiture`, `Etudiant`... |
| Stocke directement la valeur | Stocke une **référence** (une adresse) |
| Commence par une **minuscule** | Commence par une **majuscule** |
| Pas de [[01 - Classes et Objets#Les méthodes (les actions)|méthodes]] | A des méthodes |

```java
int a = 5;              // a contient directement 5
String s = "Bonjour";   // s contient l'adresse vers "Bonjour"
```

### Pourquoi c'est important ?

```java
int a = 5;
int b = a;    // b reçoit une COPIE de 5
b = 10;
System.out.println(a);  // 5 (a n'a pas changé)
```

Avec les primitifs, chacun a **sa propre copie**. On verra plus tard que les [[01 - Classes et Objets#Créer un objet|objets]] ne fonctionnent pas pareil.

---

## Les tableaux

Un **tableau** c'est une boîte qui contient **plusieurs valeurs du même type**, rangées côte à côte.

### Déclarer un tableau :

```java
// Méthode 1 : on connaît les valeurs
int[] notes = {15, 12, 18, 9, 14};

// Méthode 2 : on connaît la taille mais pas encore les valeurs
int[] notes = new int[5];  // crée un tableau de 5 cases (toutes à 0)
```

### Accéder aux éléments :

Les cases sont numérotées à partir de **0** (pas 1 !) :

```
Index :    [0]  [1]  [2]  [3]  [4]
Valeurs :  15   12   18    9   14
```

```java
int[] notes = {15, 12, 18, 9, 14};

System.out.println(notes[0]);  // 15 (premier élément)
System.out.println(notes[2]);  // 18 (troisième élément)
System.out.println(notes[4]);  // 14 (dernier élément)

// Modifier une valeur
notes[1] = 16;
System.out.println(notes[1]);  // 16
```

> **Attention** : si tu fais `notes[5]`, tu auras une erreur car l'index 5 n'existe pas (le tableau va de 0 à 4).

### Taille d'un tableau :

```java
int[] notes = {15, 12, 18, 9, 14};
System.out.println(notes.length);  // 5
```

`length` n'a **pas de parenthèses** (c'est pas une [[01 - Classes et Objets#Les méthodes (les actions)|méthode]], c'est un [[01 - Classes et Objets#Ta première classe|attribut]]).

---

## Parcourir un tableau

### Avec une boucle `for` classique :

```java
int[] notes = {15, 12, 18, 9, 14};

for (int i = 0; i < notes.length; i++) {
    System.out.println("Note " + i + " : " + notes[i]);
}
```

**Résultat :**
```
Note 0 : 15
Note 1 : 12
Note 2 : 18
Note 3 : 9
Note 4 : 14
```

### Avec un `for-each` (plus simple) :

```java
int[] notes = {15, 12, 18, 9, 14};

for (int note : notes) {
    System.out.println(note);
}
```

Le `for-each` dit : *"pour chaque `note` dans `notes`, fais..."*

| Boucle | Quand l'utiliser |
|--------|-----------------|
| `for` classique | Quand tu as besoin de l'index `i` |
| `for-each` | Quand tu veux juste lire chaque valeur |

---

## Exemple : calculer la moyenne

```java
public class Main {
    public static void main(String[] args) {
        int[] notes = {15, 12, 18, 9, 14};

        int somme = 0;
        for (int note : notes) {
            somme = somme + note;
        }

        double moyenne = (double) somme / notes.length;
        System.out.println("Moyenne : " + moyenne);  // Moyenne : 13.6
    }
}
```

### C'est quoi `(double)` ?

C'est un **cast** (conversion). Sans ça, `68 / 5` donnerait `13` (division entière). En écrivant `(double) somme`, on convertit `somme` en `double` pour avoir `13.6`.

---

## Tableaux d'objets

Les tableaux ne sont pas limités aux primitifs. Tu peux faire des tableaux d'[[01 - Classes et Objets#Créer un objet|objets]] :

```java
class Etudiant {
    String nom;
    double moyenne;

    Etudiant(String nom, double moyenne) {
        this.nom = nom;
        this.moyenne = moyenne;
    }
}
```

> Ici on utilise un [[02 - Constructeurs et this#C'est quoi un constructeur ?|constructeur]] avec [[02 - Constructeurs et this#Le mot-clé `this`|`this`]] pour initialiser chaque étudiant en une ligne.

```java
public class Main {
    public static void main(String[] args) {
        Etudiant[] classe = new Etudiant[3];

        classe[0] = new Etudiant("Karim", 14.5);
        classe[1] = new Etudiant("Sara", 16.0);
        classe[2] = new Etudiant("Youssef", 11.0);

        for (Etudiant e : classe) {
            System.out.println(e.nom + " : " + e.moyenne);
        }
    }
}
```

**Résultat :**
```
Karim : 14.5
Sara : 16.0
Youssef : 11.0
```

---

## Tableaux de `byte` (important pour Java Card)

En Java Card, tu travailleras beaucoup avec des **tableaux de bytes** car les cartes à puce communiquent en octets :

```java
// Un tableau de bytes en hexadécimal
byte[] commande = {(byte) 0x00, (byte) 0xA4, (byte) 0x04, (byte) 0x00};

// Parcourir et afficher en hexadécimal
for (byte b : commande) {
    System.out.printf("%02X ", b);
}
// Affiche : 00 A4 04 00
```

> Ne t'inquiète pas si l'hexadécimal te semble compliqué pour l'instant. On y reviendra en détail dans les cours sur les commandes APDU.

Le `(byte)` est un **cast** (comme le `(double)` vu plus haut) : `0xA4` est un `int` par défaut, et il faut le convertir en `byte`.

---

## Tableau à 2 dimensions

Un tableau peut contenir d'autres tableaux. C'est comme un **tableau de notes par matière** :

```java
int[][] notes = {
    {15, 12, 18},    // notes de maths
    {10, 14, 16},    // notes de physique
    {13, 11, 17}     // notes d'info
};

// Accéder : notes[ligne][colonne]
System.out.println(notes[0][2]);  // 18 (maths, 3ème note)
System.out.println(notes[1][0]);  // 10 (physique, 1ère note)

// Parcourir tout
for (int i = 0; i < notes.length; i++) {
    for (int j = 0; j < notes[i].length; j++) {
        System.out.print(notes[i][j] + " ");
    }
    System.out.println();
}
```

**Résultat :**
```
15 12 18
10 14 16
13 11 17
```

---

## Résumé

| Concept | C'est quoi | Exemple |
|---------|-----------|---------|
| **Type primitif** | Valeur simple stockée directement | `int`, `double`, `byte`, `boolean` |
| **Type objet** | Référence vers un [[01 - Classes et Objets#Créer un objet|objet]] | `String`, `Voiture` |
| **Tableau** | Conteneur de taille fixe, même type | `int[] tab = {1, 2, 3};` |
| **Index** | Position dans le tableau (commence à 0) | `tab[0]` = premier élément |
| **length** | Taille du tableau | `tab.length` |
| **Cast** | Conversion d'un type vers un autre | `(double) somme` |
| **for-each** | Parcourir sans index | `for (int x : tab)` |

### Prochaine étape
→ [[04 - Heritage]] : apprendre à créer des classes qui héritent d'autres classes

---

## Exercice

Crée une [[01 - Classes et Objets#C'est quoi une classe ?|classe]] `Classe` (comme une classe d'école) avec :
- Attribut : `eleves` (un tableau d'`Etudiant`)
- [[02 - Constructeurs et this#C'est quoi un constructeur ?|Constructeur]] qui reçoit le tableau d'étudiants
- [[01 - Classes et Objets#Méthodes qui renvoient une valeur|Méthode]] `moyenneGenerale()` : renvoie la moyenne de tous les étudiants
- Méthode `meilleurEleve()` : renvoie l'`Etudiant` qui a la meilleure moyenne
- Méthode `afficher()` : affiche tous les étudiants et leur moyenne

Teste avec :
```java
Etudiant[] eleves = {
    new Etudiant("Karim", 14.5),
    new Etudiant("Sara", 16.0),
    new Etudiant("Youssef", 11.0)
};

Classe maClasse = new Classe(eleves);
maClasse.afficher();
System.out.println("Moyenne générale : " + maClasse.moyenneGenerale());  // 13.83...
System.out.println("Meilleur : " + maClasse.meilleurEleve().nom);        // Sara
```
