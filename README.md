# 🏦 Banque Service - GraphQL avec Spring Boot

Un service bancaire moderne développé avec Spring Boot et GraphQL, permettant la gestion de comptes bancaires et de transactions.

## 📋 Description

Ce projet est une application Spring Boot qui expose une API GraphQL pour gérer des comptes bancaires et leurs transactions. Il utilise une base de données H2 en mémoire et fournit des fonctionnalités complètes de requêtes et de mutations GraphQL.

## 🚀 Technologies Utilisées

- **Spring Boot 3.5.7**
- **Spring Data JPA** - Persistance des données
- **Spring GraphQL** - API GraphQL
- **H2 Database** - Base de données en mémoire
- **Java 17**
- **Maven** - Gestion des dépendances

## 📁 Structure du Projet

```
src/
├── main/
│   ├── java/com/example/banque_service/
│   │   ├── BanqueServiceApplication.java
│   │   ├── entities/
│   │   │   ├── Compte.java
│   │   │   ├── Transaction.java
│   │   │   ├── TypeCompte.java
│   │   │   └── TypeTransaction.java
│   │   ├── repositories/
│   │   │   ├── CompteRepository.java
│   │   │   └── TransactionRepository.java
│   │   └── web/
│   │       ├── CompteControllerGraphQL.java
│   │       ├── GraphQLExceptionHandler.java
│   │       └── TransactionRequest.java
│   └── resources/
│       ├── application.properties
│       └── graphql/
│           └── schema.graphqls
```

## 🔧 Configuration

Le projet utilise une base de données H2 en mémoire avec les paramètres suivants :

- **URL**: `jdbc:h2:mem:banque`
- **Username**: `sa`
- **Password**: _(vide)_
- **Port**: `8082`
- **Console H2**: Activée sur `/h2-console`
- **GraphiQL**: Activé pour tester les requêtes

## 🎯 Fonctionnalités

### Types de Comptes
- **COURANT** - Compte courant
- **EPARGNE** - Compte épargne

### Types de Transactions
- **DEPOT** - Dépôt d'argent
- **RETRAIT** - Retrait d'argent

### Queries GraphQL

#### Récupérer tous les comptes
```graphql
query {
  allComptes {
    id
    solde
    dateCreation
    type
  }
}
```

#### Récupérer un compte par ID
```graphql
query {
  compteById(id: "1") {
    id
    solde
    dateCreation
    type
    transactions {
      id
      montant
      type
    }
  }
}
```

#### Obtenir les statistiques de solde
```graphql
query {
  totalSolde {
    count
    sum
    average
  }
}
```

#### Récupérer les transactions d'un compte
```graphql
query {
  compteTransactions(id: "1") {
    id
    montant
    date
    type
  }
}
```

#### Obtenir toutes les transactions
```graphql
query {
  allTransactions {
    id
    montant
    date
    type
    compte {
      id
      solde
    }
  }
}
```

#### Obtenir les statistiques des transactions
```graphql
query {
  transactionStats {
    count
    sumDepots
    sumRetraits
  }
}
```

### Mutations GraphQL

#### Créer un nouveau compte
```graphql
mutation {
  saveCompte(compte: {
    solde: 5000.0
    dateCreation: "2025-11-26"
    type: COURANT
  }) {
    id
    solde
    dateCreation
    type
  }
}
```

#### Ajouter une transaction
```graphql
mutation {
  addTransaction(transaction: {
    compteId: "1"
    montant: 500.0
    date: "2025-11-26"
    type: DEPOT
  }) {
    id
    montant
    date
    type
    compte {
      id
      solde
    }
  }
}
```

## 🛠️ Installation et Démarrage

### Prérequis
- Java 17 ou supérieur
- Maven 3.6+

### Étapes d'installation

1. **Cloner le repository**
```bash
git clone https://github.com/Bill17kh/TP-15-Service-GraphQL-avec-Spring-Boot.git
cd TP-15-Service-GraphQL-avec-Spring-Boot
```

2. **Compiler le projet**
```bash
./mvnw clean install
```

3. **Démarrer l'application**
```bash
./mvnw spring-boot:run
```

L'application sera accessible sur `http://localhost:8082`

## 🧪 Tester l'API

### GraphiQL Interface
Accédez à l'interface GraphiQL : `http://localhost:8082/graphiql`

### Console H2
Accédez à la console H2 : `http://localhost:8082/h2-console`

**Paramètres de connexion :**
- JDBC URL: `jdbc:h2:mem:banque`
- User Name: `sa`
- Password: _(laisser vide)_

## 📊 Schéma GraphQL

Le schéma complet est défini dans `src/main/resources/graphql/schema.graphqls` et inclut :

- **Types** : `Compte`, `Transaction`, `SoldeStats`, `TransactionStats`
- **Enums** : `TypeCompte`, `TypeTransaction`
- **Inputs** : `CompteRequest`, `TransactionRequest`
- **Queries** : Consultation des comptes et transactions
- **Mutations** : Création de comptes et ajout de transactions

## 🤝 Contribution

Les contributions sont les bienvenues ! N'hésitez pas à ouvrir une issue ou à soumettre une pull request.

## 📝 Licence

Ce projet est développé à des fins éducatives.

## 👤 Auteur

**Bill17kh**
- GitHub: [@Bill17kh](https://github.com/Bill17kh)

---

*Projet réalisé dans le cadre d'un TP sur GraphQL avec Spring Boot*
