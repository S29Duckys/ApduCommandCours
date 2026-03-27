# 02 - Constructeurs et `this`

## Le problème

Dans le cours [[01 - Classes et Objets]], on faisait ça pour créer un objet :

```java
Voiture maVoiture = new Voiture();
maVoiture.couleur = "rouge";
maVoiture.vitesse = 0;
```

C'est 3 lignes juste pour créer une voiture. Et si tu oublies une ligne, ton objet est incomplet. Il y a un moyen de tout faire **en une seule ligne** : le **constructeur**.

---

## C'est quoi un constructeur ?

Un constructeur, c'est une **méthode spéciale** qui s'exécute automatiquement quand tu fais `new`. Il sert à **initialiser** l'objet dès sa création.

### Règles d'un constructeur :
- Il a **le même nom que la classe**
- Il n'a **pas de type de retour** (même pas `void`)

```java
class Voiture {
    String couleur;
    int vitesse;

    // C'est le constructeur
    Voiture(String c, int v) {
        couleur = c;
        vitesse = v;
    }
}
```

### Utilisation :

```java
public class Main {
    public static void main(String[] args) {
        // Tout se fait en UNE ligne maintenant
        Voiture maVoiture = new Voiture("rouge", 0);

        System.out.println(maVoiture.couleur);  // rouge
        System.out.println(maVoiture.vitesse);  // 0
    }
}
```

Quand tu écris `new Voiture("rouge", 0)`, Java appelle le constructeur avec `c = "rouge"` et `v = 0`.

---

## Le mot-clé `this`

Dans le constructeur au-dessus, on a utilisé `c` et `v` comme noms de paramètres. Mais c'est pas très clair. On préférerait écrire `couleur` et `vitesse` directement.

Le problème :

```java
Voiture(String couleur, int vitesse) {
    couleur = couleur;  // ??? C'est quoi qui va dans quoi ?
}
```

Java ne sait plus si `couleur` c'est l'attribut ou le paramètre. C'est là que **`this`** intervient.

### `this` = "moi, l'objet actuel"

```java
class Voiture {
    String couleur;
    int vitesse;

    Voiture(String couleur, int vitesse) {
        this.couleur = couleur;   // this.couleur = l'attribut de l'objet
        this.vitesse = vitesse;   // couleur (sans this) = le paramètre
    }
}
```

| Expression | C'est quoi |
|-----------|-----------|
| `this.couleur` | l'attribut de **l'objet** |
| `couleur` | le **paramètre** reçu |

> **`this`** veut dire : "moi, l'objet qu'on est en train de créer/utiliser"

---

## Exemple concret : classe Etudiant

```java
class Etudiant {
    String nom;
    int age;
    double moyenne;

    // Constructeur
    Etudiant(String nom, int age, double moyenne) {
        this.nom = nom;
        this.age = age;
        this.moyenne = moyenne;
    }

    void sePresenter() {
        System.out.println("Je suis " + this.nom + ", " + this.age + " ans, moyenne : " + this.moyenne);
    }
}

public class Main {
    public static void main(String[] args) {
        Etudiant e1 = new Etudiant("Karim", 20, 14.5);
        Etudiant e2 = new Etudiant("Sara", 19, 8.0);

        e1.sePresenter();  // Je suis Karim, 20 ans, moyenne : 14.5
        e2.sePresenter();  // Je suis Sara, 19 ans, moyenne : 8.0
    }
}
```

C'est beaucoup plus propre que de faire 3 lignes par étudiant.

---

## Le constructeur par défaut

Si tu ne crées **aucun** constructeur, Java en crée un automatiquement qui ne fait rien :

```java
class Voiture {
    String couleur;
    int vitesse;
    // Pas de constructeur écrit → Java crée : Voiture() { }
}

// Ça marche :
Voiture v = new Voiture();
```

**Mais attention** : dès que tu crées **ton propre constructeur**, le constructeur par défaut **disparaît** :

```java
class Voiture {
    String couleur;
    int vitesse;

    Voiture(String couleur, int vitesse) {
        this.couleur = couleur;
        this.vitesse = vitesse;
    }
}

// ERREUR : Voiture v = new Voiture();  ← ne marche plus !
// Il faut obligatoirement : new Voiture("rouge", 0);
```

---

## Plusieurs constructeurs (surcharge)

Tu peux avoir **plusieurs constructeurs** avec des paramètres différents. C'est la **surcharge** :

```java
class Voiture {
    String couleur;
    int vitesse;

    // Constructeur complet
    Voiture(String couleur, int vitesse) {
        this.couleur = couleur;
        this.vitesse = vitesse;
    }

    // Constructeur avec seulement la couleur (vitesse = 0 par défaut)
    Voiture(String couleur) {
        this.couleur = couleur;
        this.vitesse = 0;
    }

    // Constructeur sans paramètre
    Voiture() {
        this.couleur = "blanc";
        this.vitesse = 0;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Voiture v1 = new Voiture("rouge", 100);  // rouge, 100
        Voiture v2 = new Voiture("bleu");         // bleu, 0
        Voiture v3 = new Voiture();               // blanc, 0

        System.out.println(v1.couleur + " - " + v1.vitesse);  // rouge - 100
        System.out.println(v2.couleur + " - " + v2.vitesse);  // bleu - 0
        System.out.println(v3.couleur + " - " + v3.vitesse);  // blanc - 0
    }
}
```

Java choisit le bon constructeur en regardant **le nombre et le type** des paramètres que tu donnes.

---

## `this` dans les méthodes aussi

`this` ne sert pas que dans les constructeurs. Tu peux l'utiliser dans n'importe quelle méthode pour parler de l'objet actuel :

```java
class Voiture {
    String couleur;
    int vitesse;

    Voiture(String couleur) {
        this.couleur = couleur;
        this.vitesse = 0;
    }

    void accelerer(int ajout) {
        this.vitesse = this.vitesse + ajout;
    }

    // Méthode qui compare deux voitures
    boolean estPlusRapideQue(Voiture autre) {
        return this.vitesse > autre.vitesse;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Voiture ferrari = new Voiture("rouge");
        Voiture twingo = new Voiture("bleu");

        ferrari.accelerer(200);
        twingo.accelerer(80);

        // ferrari.estPlusRapideQue(twingo)
        // this = ferrari, autre = twingo
        System.out.println(ferrari.estPlusRapideQue(twingo));  // true
        System.out.println(twingo.estPlusRapideQue(ferrari));  // false
    }
}
```

Quand tu appelles `ferrari.estPlusRapideQue(twingo)` :
- `this` = ferrari (l'objet qui appelle la méthode)
- `autre` = twingo (le paramètre)

---

## Résumé

| Concept | C'est quoi | Exemple |
|---------|-----------|---------|
| **Constructeur** | Méthode qui initialise l'objet à la création | `Voiture(String couleur) { }` |
| **`this`** | Référence vers l'objet actuel | `this.couleur = couleur;` |
| **Constructeur par défaut** | Créé automatiquement si tu n'en écris aucun | `Voiture() { }` |
| **Surcharge** | Plusieurs constructeurs avec des paramètres différents | `Voiture()`, `Voiture(String c)` |

---

## Exercice

Crée une classe `CompteBancaire` avec :
- Attributs : `proprietaire` (String), `solde` (double)
- Un constructeur qui prend le nom et le solde initial
- Un constructeur qui prend seulement le nom (solde = 0 par défaut)
- Méthode `deposer(double montant)` : ajoute au solde
- Méthode `retirer(double montant)` : retire du solde seulement si le solde est suffisant, sinon affiche "Solde insuffisant"
- Méthode `afficher()` : affiche le propriétaire et le solde

Teste avec :
```java
CompteBancaire c1 = new CompteBancaire("Karim", 500);
CompteBancaire c2 = new CompteBancaire("Sara");
c1.retirer(200);    // OK
c2.retirer(100);    // Solde insuffisant
c2.deposer(300);
c2.afficher();      // Sara - 300.0
```
