# Esprit--PI---2A22--2526--Aptus-
Aptus | AI-Powered Career Ecosystem Architected and developed a comprehensive, AI-driven career platform consisting of five integrated modules to guide candidates through their professional lifecycle.

# Aptus

## Description
Aptus est une plateforme Web intelligente d'aide à l'insertion professionnelle et de recrutement, spécialement conçue pour connecter les candidats (étudiants), les entreprises et les tuteurs. Elle intègre des fonctionnalités avancées d'analyse de CV par IA, d'autofill, de suggestions de compétences, et un tableau de bord complet pour le suivi des candidatures.

## Technologies utilisées
- **Frontend** : HTML5, CSS3, JavaScript (ES6+)
- **Backend** : PHP 8+ (natif, sans framework)
- **Base de données** : MySQL (via phpMyAdmin / XAMPP)

## Prérequis
- XAMPP / WAMP / MAMP (avec PHP 8+ et MySQL)
- Un navigateur web moderne (Chrome, Firefox, Edge, Safari)

## Installation
1. Copiez le dossier du projet dans le dossier racine de votre serveur local (ex: `C:/xampp/htdocs/aptus_first_official_version`).
2. Importez la base de données :
   - Ouvrez phpMyAdmin (`http://localhost/phpmyadmin`).
   - Créez une base de données nommée `aptus`.
   - Importez le fichier SQL situé dans `database/schema.sql`.

## Lancement
- Démarrez Apache et MySQL depuis le panneau de contrôle XAMPP.
- Ouvrez votre navigateur et accédez à : `http://localhost/aptus_first_official_version/view/frontoffice/landing.php`
- Ou utilisez le serveur PHP intégré :
  ```bash
  php -S localhost:8000
  ```

## Variables d'environnement
Voir le fichier `.env.example` pour configurer les clés API nécessaires (Groq, Gemini, Firecrawl). Renommez ce fichier en `.env` dans votre environnement local pour qu'elles soient prises en compte.

## Démo
Le dossier `demo/` contient les captures d'écran et la documentation visuelle du projet.

## Auteurs
- **Ons Mestaoui** - Classe : 2A22 - Année : 2025/2026
- **Tuteur** : Chedy Bouslema
