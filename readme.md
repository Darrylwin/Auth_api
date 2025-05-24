# API d'Authentification - Documentation des Endpoints

Cette documentation présente tous les endpoints disponibles dans notre API d'authentification.

## Endpoints d'Authentification

### Inscription
- **URL**: `/api/auth/register`
- **Méthode**: `POST`
- **Description**: Créer un nouveau compte utilisateur
- **Corps de la requête**:
  ```json
  {
    "username": "string",
    "email": "string",
    "password": "string"
  }
  ```
- **Réponse réussie**:
  ```json
  {
    "id": "string",
    "username": "string",
    "email": "string",
    "createdAt": "date"
  }
  ```

### Connexion
- **URL**: `/api/auth/login`
- **Méthode**: `POST`
- **Description**: Authentifier un utilisateur et obtenir un token
- **Corps de la requête**:
  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
- **Réponse réussie**:
  ```json
  {
    "token": "string",
    "refreshToken": "string",
    "expiresIn": "number"
  }
  ```

### Déconnexion
- **URL**: `/api/auth/logout`
- **Méthode**: `POST`
- **Description**: Déconnecter l'utilisateur (invalider le token)
- **En-têtes**: `Authorization: Bearer {token}`
- **Réponse réussie**: 
  ```json
  {
    "message": "Déconnexion réussie"
  }
  ```

### Rafraîchir Token
- **URL**: `/api/auth/refresh-token`
- **Méthode**: `POST`
- **Description**: Obtenir un nouveau token d'accès avec un refresh token
- **Corps de la requête**:
  ```json
  {
    "refreshToken": "string"
  }
  ```
- **Réponse réussie**:
  ```json
  {
    "token": "string",
    "refreshToken": "string",
    "expiresIn": "number"
  }
  ```

### Mot de passe oublié
- **URL**: `/api/auth/forgot-password`
- **Méthode**: `POST`
- **Description**: Demander un lien de réinitialisation de mot de passe
- **Corps de la requête**:
  ```json
  {
    "email": "string"
  }
  ```
- **Réponse réussie**:
  ```json
  {
    "message": "Si l'adresse e-mail existe, un lien de réinitialisation a été envoyé"
  }
  ```

### Réinitialiser mot de passe
- **URL**: `/api/auth/reset-password`
- **Méthode**: `POST`
- **Description**: Réinitialiser le mot de passe avec un token valide
- **Corps de la requête**:
  ```json
  {
    "token": "string",
    "newPassword": "string"
  }
  ```
- **Réponse réussie**:
  ```json
  {
    "message": "Mot de passe réinitialisé avec succès"
  }
  ```

## Endpoints de Gestion de Compte

### Obtenir Profil Utilisateur
- **URL**: `/api/users/me`
- **Méthode**: `GET`
- **Description**: Récupérer les informations du profil de l'utilisateur connecté
- **En-têtes**: `Authorization: Bearer {token}`
- **Réponse réussie**:
  ```json
  {
    "id": "string",
    "username": "string",
    "email": "string",
    "createdAt": "date",
    "profile": {
      "firstName": "string",
      "lastName": "string",
      "avatar": "string"
    }
  }
  ```

### Mettre à jour Profil
- **URL**: `/api/users/me`
- **Méthode**: `PUT`
- **Description**: Mettre à jour les informations du profil
- **En-têtes**: `Authorization: Bearer {token}`
- **Corps de la requête**:
  ```json
  {
    "username": "string",
    "firstName": "string",
    "lastName": "string"
  }
  ```
- **Réponse réussie**:
  ```json
  {
    "id": "string",
    "username": "string",
    "email": "string",
    "profile": {
      "firstName": "string",
      "lastName": "string",
      "avatar": "string"
    }
  }
  ```

### Changer Mot de Passe
- **URL**: `/api/users/change-password`
- **Méthode**: `POST`
- **Description**: Modifier le mot de passe de l'utilisateur connecté
- **En-têtes**: `Authorization: Bearer {token}`
- **Corps de la requête**:
  ```json
  {
    "currentPassword": "string",
    "newPassword": "string"
  }
  ```
- **Réponse réussie**:
  ```json
  {
    "message": "Mot de passe modifié avec succès"
  }
  ```

## Endpoints d'Administration

### Lister Utilisateurs
- **URL**: `/api/admin/users`
- **Méthode**: `GET`
- **Description**: Récupérer la liste des utilisateurs (admin uniquement)
- **En-têtes**: `Authorization: Bearer {token}`
- **Paramètres de requête**: 
  - `page`: numéro de page (défaut: 1)
  - `limit`: nombre d'éléments par page (défaut: 10)
- **Réponse réussie**:
  ```json
  {
    "users": [
      {
        "id": "string",
        "username": "string",
        "email": "string",
        "role": "string",
        "createdAt": "date"
      }
    ],
    "totalPages": "number",
    "currentPage": "number"
  }
  ```

### Obtenir Utilisateur par ID
- **URL**: `/api/admin/users/{userId}`
- **Méthode**: `GET`
- **Description**: Récupérer les détails d'un utilisateur spécifique (admin uniquement)
- **En-têtes**: `Authorization: Bearer {token}`
- **Réponse réussie**:
  ```json
  {
    "id": "string",
    "username": "string",
    "email": "string",
    "role": "string",
    "createdAt": "date",
    "profile": {
      "firstName": "string",
      "lastName": "string",
      "avatar": "string"
    }
  }
  ```

### Mettre à jour Rôle Utilisateur
- **URL**: `/api/admin/users/{userId}/role`
- **Méthode**: `PUT`
- **Description**: Modifier le rôle d'un utilisateur (admin uniquement)
- **En-têtes**: `Authorization: Bearer {token}`
- **Corps de la requête**:
  ```json
  {
    "role": "string"
  }
  ```
- **Réponse réussie**:
  ```json
  {
    "id": "string",
    "username": "string",
    "role": "string",
    "message": "Rôle mis à jour avec succès"
  }
  ```

### Désactiver Compte Utilisateur
- **URL**: `/api/admin/users/{userId}/disable`
- **Méthode**: `PUT`
- **Description**: Désactiver un compte utilisateur (admin uniquement)
- **En-têtes**: `Authorization: Bearer {token}`
- **Réponse réussie**:
  ```json
  {
    "id": "string",
    "username": "string",
    "status": "disabled",
    "message": "Compte désactivé avec succès"
  }
  ```

## Statuts d'Erreur Communs

- **400 Bad Request**: Requête mal formée ou données invalides
- **401 Unauthorized**: Token d'authentification manquant ou invalide
- **403 Forbidden**: Permissions insuffisantes pour l'action demandée
- **404 Not Found**: Ressource introuvable
- **422 Unprocessable Entity**: Validation échouée
- **500 Internal Server Error**: Erreur serveur
