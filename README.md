# The Bradery: E-Commerce App

Ce projet est une application e-commerce qui permet aux utilisateurs de parcourir des produits, de les ajouter à leur panier, et de passer des commandes.

## Structure du Projet

Le dépôt principal comprend deux repositories (SUBMODUELS) :

### Backend

- **Technologie**: NestJs
- **Base de Données**: MySQL
- **Autres Technologies Utilisées**:
  - **Redis**: Utilisé pour le stockage en cache des Acces Token.
  - **Swagger**: Utilisé pour la documentation automatique de l'API ( localhost:3001/api ).
  - **Passport**: Intégré pour l'authentification sécurisée des utilisateurs (@Gards).

### Frontend

- **Technologie**: React
- **Autres Technologies Utilisées**:
  - **Tailwind CSS**: Employé pour le développement rapide de composants UI.
  - **Toast Library**: Intégrée pour des notifications utilisateur élégantes.

## Installation

### Prérequis

- Docker doit être installé localement.

### Instructions

1. Clonez ce dépôt avec ses sous-modules.

```bash
git clone https://github.com/Dedpy/bradery-ecommerce.git
```

2. Dans le dossier `bradery-ecommerce`, exécutez les commandes suivantes pour cloner les sous-modules:

```bash
cd bradery-ecommerce
git submodule init
git submodule update
```

#### Les sous-modules de ce projet pointent vers une branche appelée `docker` pour chaque service. Si vous souhaitez tester chaque projet individuellement, vous pouvez accéder au dépôt de chacun et suivre les instructions fournies. Pour le service backend, visitez [lien vers le dépôt backend](https://github.com/Dedpy/backend-service-ecommerce) et pour le service frontend, visitez [lien vers le dépôt frontend](https://github.com/Dedpy/frontend-service-ecommerce)

3. Démarrer Docker
Assurez-vous que le démon Docker est en cours d'exécution. Ensuite, lancez la commande suivante :

```bash
docker-compose up
```

4. Accéder à l'image MySQL

Une fois que l'application est en cours d'exécution sur Docker, vous pouvez accéder à l'image MySQL pour insérer les données dans la table `products`. Vous pouvez le faire en exécutant la commande suivante :

```bash
docker exec -it db mysql -u root
```

5. Insérer des données dans la table `Products`

Une fois que vous êtes connecté à MySQL, sélectionnez votre base de données avec la commande suivante :

```sql
USE bradery;
```

Insérer des données dans la table Products avec la commande suivante (La table products est deja creer avec nestJs):

```sql
INSERT INTO Products (name, price, inventory) VALUES 
    ('T-shirt Blanc', 19.99, 100),
    ('Jean Slim Noir', 49.99, 75),
    ('Chaussures de Sport', 89.99, 50),
    ('Veste en Cuir', 199.99, 25),
    ("Robe d'Été", 29.99, 60),
    ('Cravate en Soie', 24.99, 40),
    ('Sac à Main', 59.99, 30),
    ('Chapeau Panama', 34.99, 20),
    ('Écharpe en Laine', 29.99, 45),
    ('Ceinture en Cuir', 39.99, 70),
    ('Montre Classique', 149.99, 15),
    ('Bottes en Cuir', 99.99, 40),
    ('Lunettes de Soleil', 79.99, 50),
    ('Chemise à Carreaux', 44.99, 55),
    ('Pull-over Gris', 64.99, 35),
    ('Short en Jean', 39.99, 60),
    ("Sandales d'Été", 49.99, 40),
    ('Bijoux Fantaisie', 14.99, 85),
    ('Pantalon Chino', 54.99, 50),
    ('Blouse Florale', 39.99, 40);
```

6. Tester l'application

Après avoir inséré les données, vous pouvez tester l'application en accédant à `localhost:3000` sur votre machine. Assurez-vous que l'application est en cours d'exécution et que le port 3000 est correctement exposé.

## Améliorations Futures

En raison d'un emploi du temps serré en raison de la fin de mes examens, voici une liste de futures améliorations que je pourrais envisager pour le projet :

1. **Implémenter la session ou le stockage pour stocker le jeton d'authentification :**
   Une amélioration future pourrait inclure l'utilisation du stockage local / session côté client pour gérer de manière plus sécurisée les jetons d'authentification.

2. **Rendre l'appel API pour l'authentification plus sécurisé dans le frontend en transmettant un mot de passe haché :**
   Actuellement, la transmission du mot de passe se fait en texte brut lors de l'authentification. Pour renforcer la sécurité, une amélioration future pourrait inclure le passage d'un mot de passe haché lors des appels API d'authentification.

3. **Enregistrer les détails des commandes même si l'utilisateur n'a pas encore passé de commande :**
   À l'heure actuelle, les détails de la commande ne sont enregistrés qu'après la passation d'une commande. Une amélioration future pourrait inclure l'enregistrement des détails des commandes même si l'utilisateur n'a pas encore finalisé la commande, offrant ainsi une fonctionnalité de sauvegarde du panier.

## Fonctionnalités Implémentées

Voici la liste des fonctionnalités déjà implémentées dans le projet :

- **Ajout de produits au panier :**
  Les utilisateurs peuvent ajouter des produits à leur panier, en respectant la limite de stock disponible pour chaque produit.

- **Passage à la page de paiement et passation de commande :**
  Une fois les produits ajoutés, les utilisateurs peuvent se diriger vers une page de paiement et passer une commande.

- **Mise à jour du stock de produits :**
  Après la passation d'une commande, le stock de produits est automatiquement mis à jour pour refléter les articles achetés.

- **Contraintes sur le choix du stock :**
  Les utilisateurs ne peuvent pas choisir un stock supérieur à l'inventaire disponible ou inférieur à 1 lors de l'ajout d'un produit au panier.

- **Limitation d'un seul produit par panier :**
  Chaque utilisateur peut ajouter un seul produit au panier à la fois et peut le retirer ultérieurement.
