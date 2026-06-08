# 📚 BookToRead — BookShelf Manager

Un projet Java de gestion de bibliothèque personnelle, développé en **TDD (Test-Driven Development)** avec JUnit 5 et AssertJ.

---

## 📖 Description

`BookToRead` est une application Java qui modélise une étagère à livres (`BookShelf`). Elle permet d'ajouter, trier et regrouper des livres selon différents critères. Le projet met l'accent sur les bonnes pratiques de développement, notamment les tests unitaires.

---

## 🗂️ Structure du projet

```
bookstoread/
├── Book.java           # Modèle représentant un livre
├── BookShelf.java      # Logique principale de l'étagère
└── BookShelfSpec.java  # Tests unitaires (JUnit 5)
```

---

## 📦 Modèle `Book`

Chaque livre possède les attributs suivants :

| Attribut        | Type        | Description                  |
|----------------|-------------|------------------------------|
| `title`        | `String`    | Titre du livre               |
| `author`       | `String`    | Nom de l'auteur              |
| `publishedOn`  | `LocalDate` | Date de publication          |

---

## ⚙️ Fonctionnalités de `BookShelf`

| Méthode                          | Description                                                      |
|----------------------------------|------------------------------------------------------------------|
| `books()`                        | Retourne la liste immuable des livres (ordre d'insertion)        |
| `add(Book... books)`             | Ajoute un ou plusieurs livres à l'étagère                        |
| `arrange()`                      | Retourne les livres triés par titre (ordre alphabétique)         |
| `arrange(Comparator<Book>)`      | Retourne les livres triés selon un critère personnalisé          |
| `groupByPublicationYear()`       | Regroupe les livres par année de publication (`Map<Year, List<Book>>`) |
| `groupBy(Function<Book, K>)`     | Regroupe les livres selon n'importe quel critère (générique)     |

---

## 🧪 Tests unitaires

Les tests sont écrits avec **JUnit 5** et **AssertJ** et couvrent les cas suivants :

- ✅ Étagère vide à l'initialisation
- ✅ Ajout de livres
- ✅ Immutabilité de la liste retournée par `books()`
- ✅ Tri alphabétique par titre
- ✅ Préservation de l'ordre d'insertion après un `arrange()`
- ✅ Tri selon un critère fourni par l'utilisateur (ex : ordre inversé)
- ✅ Regroupement par année de publication
- ✅ Regroupement par auteur (critère personnalisé)

---

## 🚀 Prérequis & Lancement

### Prérequis

- Java 11+
- Maven ou Gradle
- JUnit 5
- AssertJ

### Lancer les tests avec Maven

```bash
mvn test
```

### Lancer les tests avec Gradle

```bash
./gradlew test
```

---

## 💡 Exemple d'utilisation

```java
BookShelf shelf = new BookShelf();

Book effectiveJava = new Book("Effective Java", "Joshua Bloch", LocalDate.of(2008, Month.MAY, 8));
Book cleanCode     = new Book("Clean Code", "Robert C. Martin", LocalDate.of(2008, Month.AUGUST, 1));

shelf.add(effectiveJava, cleanCode);

// Tri alphabétique
List<Book> sorted = shelf.arrange();

// Regroupement par année
Map<Year, List<Book>> byYear = shelf.groupByPublicationYear();

// Regroupement par auteur
Map<String, List<Book>> byAuthor = shelf.groupBy(Book::getAuthor);
```

---

## 📌 Livres utilisés dans les tests

| Titre                     | Auteur                    | Année |
|--------------------------|---------------------------|-------|
| Effective Java            | Joshua Bloch              | 2008  |
| Code Complete             | Steve McConnel            | 2004  |
| The Mythical Man-Month    | Frederick Phillips Brooks | 1975  |
| Clean Code                | Robert C. Martin          | 2008  |

---

## 🏗️ Approche TDD

Ce projet suit la démarche **Test-Driven Development** :

1. 🔴 **Red** — Écrire un test qui échoue
2. 🟢 **Green** — Écrire le code minimal pour le faire passer
3. 🔵 **Refactor** — Améliorer le code sans casser les tests
