# Documentation Technique - Aptus

Aptus est un écosystème intelligent d'aide à l'insertion professionnelle et de recrutement. Cette documentation décrit l'architecture globale, le modèle de données, les cas d'utilisation et les différents contrôleurs du système.

---

## 1. Diagramme d'Utilisations Générale (UML)

Voici la modélisation UML des différents rôles et cas d'utilisation de la plateforme. Les rôles **Administrateur**, **Candidat** et **Entreprise** héritent des droits généraux de l'**Utilisateur**.

```mermaid
flowchart LR
    %% Actors
    User[Utilisateur]
    Admin[Administrateur]
    Cand[Candidat]
    Ent[Entreprise]

    %% Generalization (Inheritance)
    Admin --|> User
    Cand --|> User
    Ent --|> User

    %% Use Cases
    UC_Profil([Gérer profil])
    UC_Templates([Gérer Templates])
    UC_Posts([Gérer posts])
    UC_Formulaires([Gérer formulaires])
    UC_Tendances([Gérer tendances du marché])
    UC_CVs([Gérer CVs])
    UC_Candidatures([Gérer candidatures])

    %% Links
    User --> UC_Profil
    Admin --> UC_Templates
    Admin --> UC_Posts
    Cand --> UC_Formulaires
    Cand --> UC_Tendances
    Cand --> UC_CVs
    Ent --> UC_Candidatures

    %% Styles
    style User fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#fff
    style Admin fill:#10b981,stroke:#059669,stroke-width:2px,color:#fff
    style Cand fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style Ent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#fff
    style UC_Profil fill:#3b82f6,stroke:#2563eb,stroke-width:1px,color:#fff
    style UC_Templates fill:#3b82f6,stroke:#2563eb,stroke-width:1px,color:#fff
    style UC_Posts fill:#3b82f6,stroke:#2563eb,stroke-width:1px,color:#fff
    style UC_Formulaires fill:#3b82f6,stroke:#2563eb,stroke-width:1px,color:#fff
    style UC_Tendances fill:#3b82f6,stroke:#2563eb,stroke-width:1px,color:#fff
    style UC_CVs fill:#3b82f6,stroke:#2563eb,stroke-width:1px,color:#fff
    style UC_Candidatures fill:#3b82f6,stroke:#2563eb,stroke-width:1px,color:#fff
```

### Description des rôles :
- **Utilisateur** : Rôle de base (gestion de compte, modification du profil).
- **Candidat** : Chercheur d'un emploi/stage, créant des CVs avec l'IA, consultant les tendances du marché et il peut rejoindre des formations proposées.
- **Entreprise** : Recruteur déposant des offres d'emploi et gérant les candidatures reçues.
- **Administrateur** : Super-utilisateur gérant les modèles (templates) de CV, les utilisateurs et les publications de veille.

---

## 2. Architecture Technique (MVC)

Le projet est structuré selon un modèle **MVC (Modèle-Vue-Contrôleur)** natif en PHP, sans framework externe, garantissant légèreté et contrôle total.

### Organisation des dossiers :
- `controller/` : Logique applicative, interaction avec les API d'IA et opérations CRUD.
- `model/` : Classes de définition des entités (Utilisateur, CV, Offre, etc.).
- `view/` : Interfaces utilisateur, divisées en :
  - `frontoffice/` : Espace candidat, entreprise, tuteur et pages publiques.
  - `backoffice/` : Espace d'administration du système.
  - `assets/` : Feuilles de style (CSS), scripts (JS), polices et images.
- `database/` : Script SQL d'initialisation de la base de données.

---

## 3. Contrôleurs Clés et Services IA

Aptus intègre des contrôleurs PHP spécifiques pour chaque module fonctionnel, notamment les services d'intelligence artificielle :

| Contrôleur / Service | Rôle Principal |
|---|---|
| [AIController.php](file:///c:/xampp/htdocs/aptus_first_official_version/controller/AIController.php) | Centralise les appels d'IA (Groq Llama-3 & Google Gemini) pour l'audit automatique des CVs et la génération de lettres de motivation. |
| [VeilleAIController.php](file:///c:/xampp/htdocs/aptus_first_official_version/controller/VeilleAIController.php) | Utilise l'API Firecrawl pour scraper les offres d'emploi du marché et générer des rapports de tendance de salaires/compétences. |
| [UtilisateurC.php](file:///c:/xampp/htdocs/aptus_first_official_version/controller/UtilisateurC.php) | Gestion des inscriptions, connexions sécurisées, rôles et authentification locale. |
| [CVC.php](file:///c:/xampp/htdocs/aptus_first_official_version/controller/CVC.php) | Gestion de la structure de CV (parcours, compétences, langues) et liaison avec les templates d'affichage. |
| [face_api.php](file:///c:/xampp/htdocs/aptus_first_official_version/controller/face_api.php) | Authentification biométrique Face ID locale via reconnaissance de repères faciaux. |
| [offreC.php](file:///c:/xampp/htdocs/aptus_first_official_version/controller/offreC.php) | Publication, modification et recherche d'offres d'emploi géolocalisées. |

---

## 4. Architecture de la Base de Données

Les tables de la base de données `aptus` sont conçues pour gérer la modularité des profils d'utilisateurs et le stockage des analyses IA :

- **`utilisateur`** : Stocke les informations communes (email, hash du mot de passe, rôle, photo, statut de vérification).
- **`candidat` / `entreprise` / `administrateur`** : Tables de spécialisation liées par clé étrangère à `utilisateur`.
- **`cv`** : Contient les données des CVs des candidats.
- **`templates`** : Les styles visuels applicables aux CVs.
- **`offreemploi`** : Les offres d'emploi publiées par les entreprises.
- **`candidatures`** : Table de liaison entre les offres et les candidats pour le suivi (statut: En attente, Accepté, Refusé).
- **`rapport_ia`** : Stocke l'historique des audits de CV générés par l'intelligence artificielle.
- **`donnee_marche` / `rapport_marche`** : Stocke les indicateurs de salaires et de compétences collectés.
