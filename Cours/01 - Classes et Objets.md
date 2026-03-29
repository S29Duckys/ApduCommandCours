# 01 - Classes et Objets

## C'est quoi une classe ?

Une **classe**, c'est comme un **plan de construction**. Imagine que tu veux construire des voitures. Avant de construire une voiture, tu as besoin d'un plan qui dit :
- une voiture a une **couleur**
- une voiture a une **vitesse**
- une voiture peut **accélérer**
- une voiture peut **freiner**

Ce plan, c'est la **classe**. La voiture que tu construis à partir de ce plan, c'est un **objet**.

> **Classe** = le plan
> **Objet** = la chose concrète créée à partir du plan

---

## Ta première classe

```java
class Voiture {
    // Ce sont les ATTRIBUTS (les caractéristiques)
    String couleur;
    int vitesse;
}
```

C'est tout ! Tu viens de créer une classe. Elle dit :
- chaque voiture aura une `couleur` (du texte → `String`)
- chaque voiture aura une `vitesse` (un nombre → `int`)

> `String` et `int` sont des **types de données**. On les explique en détail dans [[03 - Tableaux et types de donnees]].

---

## Créer un objet

Maintenant on va **construire** une voiture à partir de ce plan :

```java
class Voiture {
    String couleur;
    int vitesse;
}

public class Main {
    public static void main(String[] args) {
        // On crée un objet de type Voiture
        Voiture maVoiture = new Voiture();

        // On donne des valeurs aux attributs
        maVoiture.couleur = "rouge";
        maVoiture.vitesse = 0;

        // On affiche
        System.out.println("Couleur : " + maVoiture.couleur);
        System.out.println("Vitesse : " + maVoiture.vitesse);
    }
}
```

**Résultat :**
```
Couleur : rouge
Vitesse : 0
```

### Décortiquons la ligne importante :

```java
Voiture maVoiture = new Voiture();
```

| Partie      | Signification                    |
| ----------- | -------------------------------- |
| `Voiture`   | le type (c'est une Voiture)      |
| `maVoiture` | le nom qu'on donne à notre objet |
| `new`       | "crée un nouvel objet"           |
| `Voiture()` | appelle le plan de construction (le [[02 - Constructeurs et this|constructeur]]) |

C'est comme dire : *"Crée-moi une nouvelle Voiture et appelle-la maVoiture"*

> Ici on donne les valeurs une par une (3 lignes). C'est un peu long. Dans, tu apprendras à tout initialiser en **une seule ligne** grâce au **constructeur**  [[02 - Constructeurs et this]].

---

## On peut créer plusieurs objets

Un plan peut servir à construire **plusieurs** voitures :

```java
public class Main {
    public static void main(String[] args) {
        Voiture voiture1 = new Voiture();
        voiture1.couleur = "rouge";
        voiture1.vitesse = 0;

        Voiture voiture2 = new Voiture();
        voiture2.couleur = "bleu";
        voiture2.vitesse = 50;

        System.out.println(voiture1.couleur); // rouge
        System.out.println(voiture2.couleur); // bleu
    }
}
```

Chaque objet a **ses propres valeurs**. Changer la couleur de `voiture1` ne change pas celle de `voiture2`.

> Quand tu auras beaucoup d'objets, tu pourras les ranger dans un [[03 - Tableaux et types de donnees|tableau]] pour les parcourir avec une boucle.

---

## Les méthodes (les actions)

Les attributs c'est ce que l'objet **a**. Les méthodes c'est ce que l'objet **fait**.

```java
class Voiture {
    String couleur;
    int vitesse;

    // Méthode : accélérer
    void accelerer() {
        vitesse = vitesse + 10;
        System.out.println("La voiture accélère ! Vitesse : " + vitesse);
    }

    // Méthode : freiner
    void freiner() {
        if (vitesse >= 10) {
            vitesse = vitesse - 10;
        }
        System.out.println("La voiture freine ! Vitesse : " + vitesse);
    }
}
```

### Utilisation :

```java
public class Main {
    public static void main(String[] args) {
        Voiture maVoiture = new Voiture();
        maVoiture.couleur = "rouge";
        maVoiture.vitesse = 0;

        maVoiture.accelerer();  // Vitesse : 10
        maVoiture.accelerer();  // Vitesse : 20
        maVoiture.accelerer();  // Vitesse : 30
        maVoiture.freiner();    // Vitesse : 20
    }
}
```

**Résultat :**
```
La voiture accélère ! Vitesse : 10
La voiture accélère ! Vitesse : 20
La voiture accélère ! Vitesse : 30
La voiture freine ! Vitesse : 20
```

Le mot `void` veut dire que la méthode **ne renvoie rien**, elle fait juste une action.

---

## Méthodes avec paramètres

On peut donner des infos à une méthode :

```java
class Voiture {
    String couleur;
    int vitesse;

    // On choisit de combien on accélère
    void accelerer(int ajout) {
        vitesse = vitesse + ajout;
        System.out.println("Vitesse : " + vitesse);
    }
}
```

```java
maVoiture.accelerer(30);  // Vitesse : 30
maVoiture.accelerer(50);  // Vitesse : 80
```

Le `int ajout` entre parenthèses, c'est le **paramètre**. Quand tu appelles `accelerer(30)`, le 30 va dans `ajout`.

> Dans [[02 - Constructeurs et this]], tu verras que quand le paramètre a le **même nom** que l'attribut, on utilise le mot-clé `this` pour les différencier.

---

## Méthodes qui renvoient une valeur

Parfois on veut que la méthode **donne un résultat** au lieu de juste afficher :

```java
class Voiture {
    String couleur;
    int vitesse;

    // Cette méthode RENVOIE un texte
    String getDescription() {
        return "Voiture " + couleur + " à " + vitesse + " km/h";
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Voiture maVoiture = new Voiture();
        maVoiture.couleur = "rouge";
        maVoiture.vitesse = 80;

        String description = maVoiture.getDescription();
        System.out.println(description);
    }
}
```

**Résultat :**
```
Voiture rouge à 80 km/h
```

| Mot clé | Signification |
|---------|--------------|
| `void` | la méthode ne renvoie rien |
| `String` | la méthode renvoie du texte |
| `int` | la méthode renvoie un nombre entier |
| `boolean` | la méthode renvoie vrai ou faux |
| `return` | "voici le résultat" |

> Pour la liste complète des types (`int`, `double`, `byte`, `boolean`...), voir [[03 - Tableaux et types de donnees#Les types primitifs]].

---

## Exemple complet récapitulatif

```java
class Etudiant {
    String nom;
    int age;
    double moyenne;

    void sePresenter() {
        System.out.println("Salut, je suis " + nom + ", j'ai " + age + " ans.");
    }

    boolean estAdmis() {
        if (moyenne >= 10.0) {
            return true;
        } else {
            return false;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Etudiant e1 = new Etudiant();
        e1.nom = "Karim";
        e1.age = 20;
        e1.moyenne = 14.5;

        Etudiant e2 = new Etudiant();
        e2.nom = "Sara";
        e2.age = 19;
        e2.moyenne = 8.0;

        e1.sePresenter();  // Salut, je suis Karim, j'ai 20 ans.
        e2.sePresenter();  // Salut, je suis Sara, j'ai 19 ans.

        System.out.println(e1.nom + " admis ? " + e1.estAdmis());  // true
        System.out.println(e2.nom + " admis ? " + e2.estAdmis());  // false
    }
}
```

> Tu remarques qu'on initialise chaque étudiant en 3 lignes. Avec un [[02 - Constructeurs et this|constructeur]], on pourrait écrire directement `new Etudiant("Karim", 20, 14.5)`.

---

## Résumé

| Concept | C'est quoi | Exemple |
|---------|-----------|---------|
| **Classe** | Le plan / le modèle | `class Voiture { }` |
| **Objet** | Une instance concrète du plan | `new Voiture()` |
| **Attribut** | Une caractéristique de l'objet | `String couleur;` |
| **Méthode** | Une action que l'objet peut faire | `void accelerer() { }` |
| **Paramètre** | Une info donnée à la méthode | `void accelerer(int ajout)` |
| **return** | Renvoie un résultat | `return vitesse;` |

### Prochaine étape
→ [[02 - Constructeurs et this]] : apprendre à initialiser un objet en une seule ligne

---

## Exercice pour pratiquer

Crée une classe `Telephone` avec :
- Attributs : `marque` (String), `batterie` (int, de 0 à 100)
- Méthode `appeler()` : affiche "Appel en cours..." et enlève 5 de batterie
- Méthode `charger(int minutes)` : ajoute les minutes à la batterie (sans dépasser 100)
- Méthode `afficherEtat()` : affiche la marque et le niveau de batterie

Essaie de le faire toi-même avant de demander la correction !
