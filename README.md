# 📝 ApiArticleJava - Architecture Hexagonale

Ce projet est une API REST développée avec **Spring Boot 3**, structurée selon les principes de l'**Architecture Hexagonale**. Elle permet la gestion d'articles avec plusieurs modes de persistance interchangeables.

## 🚀 Structure du Projet

Le projet est découpé en plusieurs modules Gradle :

* **`core-domain`** : Contient les entités métier (`Article`), les interfaces (`IDAOArticle`) et la logique de service.
* **`adapter-mock`** : Implémentation en mémoire (`ArrayList`) pour le développement rapide.
* **`adapter-mongo`** : Adaptateur pour la persistance NoSQL avec **MongoDB**.
* **`adapter-jpa`** : Adaptateur pour les bases de données relationnelles via **JPA/MySQL**.
* **`app`** : Point d'entrée de l'application (Controllers REST et Configuration).

---

## 🛠 Configuration et Lancement

L'application utilise les **Spring Profiles** pour choisir l'adaptateur de stockage.

### 1. Choisir le mode de stockage
Dans le fichier `app/src/main/resources/application.yml` :
```yaml
app:
  persistence:
    type: mock # options: mock, mongodb, jpa
```

### 2. Gestion des dépendances
Dans le `build.gradle` du module `:app`, activez les modules souhaités :
```gradle
dependencies {
    implementation project(':core-domain')
    // implementation project(':adapter-jpa')
    // implementation project(':adapter-mongo')
    implementation project(':adapter-mock')
}
```

---

## 🛣 API Endpoints

| Méthode | Endpoint         | Description |
| :--- |:-----------------| :--- |
| `GET` | `/articles`      | Récupérer tous les articles |
| `GET` | `/articles/{id}` | Récupérer un article par son ID |
| `POST` | `/articles/save` | Créer ou modifier un article |
| `DELETE` | `/articles/{id}` | Supprimer un article |

---

## 🧰 Prérequis
* **Java 17**
* **Gradle**
* **MongoDB** (optionnel)
* **MySQL** (optionnel)