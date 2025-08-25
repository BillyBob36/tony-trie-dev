# Tony Trie - Application de Tri et Correspondance de Profils

Application web pour analyser et trier des profils en fonction de critères personnalisés, avec export automatique vers Google Sheets.

## Fonctionnalités

- **Import de fichiers Excel** : Chargement et analyse de fichiers .xlsx
- **Critères personnalisés** : Définition de critères de tri flexibles
- **Analyse IA** : Utilisation d'OpenAI pour l'analyse de correspondance
- **Export Google Sheets** : Création automatique de feuilles de calcul
- **Interface intuitive** : Design moderne et responsive

## Technologies utilisées

- HTML5, CSS3, JavaScript (Vanilla)
- Google Sheets API
- OpenAI API
- SheetJS pour la lecture Excel

## Installation et Configuration

### 1. Configuration des clés API

Modifiez le fichier `config.js` avec vos propres clés API :

```javascript
const APP_CONFIG = {
    GOOGLE: {
        CLIENT_ID: 'VOTRE_GOOGLE_CLIENT_ID',
        API_KEY: 'VOTRE_GOOGLE_API_KEY',
        // ... autres paramètres
    },
    OPENAI: {
        API_KEY: 'VOTRE_OPENAI_API_KEY',
        // ... autres paramètres
    }
};
```

### 2. Obtenir les clés API

#### Google API :
1. Allez sur [Google Cloud Console](https://console.cloud.google.com/)
2. Créez un nouveau projet ou sélectionnez un projet existant
3. Activez les APIs Google Sheets et Google Drive
4. Créez des identifiants (API Key + OAuth 2.0 Client ID)
5. Ajoutez votre domaine dans les origines autorisées

#### OpenAI API :
1. Allez sur [OpenAI Platform](https://platform.openai.com/)
2. Créez un compte et générez une clé API
3. Ajoutez des crédits à votre compte

### 3. Déploiement

#### Local :
```bash
# Serveur Python simple
python -m http.server 8000

# Ou serveur Node.js
npx serve .
```

#### GitHub Pages avec Variables d'Environnement :
1. **Configurez les secrets GitHub** :
   - Allez dans votre dépôt GitHub > Settings > Secrets and variables > Actions
   - Ajoutez les secrets suivants :
     - `GOOGLE_CLIENT_ID` : Votre Client ID Google
     - `GOOGLE_API_KEY` : Votre clé API Google
     - `OPENAI_API_KEY` : Votre clé API OpenAI

2. **Déployez automatiquement** :
   - Poussez le code vers la branche `main`
   - GitHub Actions se charge automatiquement du déploiement
   - L'application sera disponible sur `https://votre-username.github.io/votre-repo`

3. **Configurez Google Cloud Console** :
   - Ajoutez votre URL GitHub Pages dans les origines autorisées
   - Format : `https://votre-username.github.io`

#### Déploiement Manuel (Alternative) :
1. Poussez le code vers votre dépôt GitHub
2. Activez GitHub Pages dans Settings > Pages
3. Configurez les domaines autorisés dans Google Cloud Console

## ⚙️ Configuration Google OAuth

### Étape 1 : Créer un projet Google Cloud

1. Allez sur [Google Cloud Console](https://console.cloud.google.com/)
2. Créez un nouveau projet ou sélectionnez un projet existant
3. Activez les APIs suivantes :
   - Google Sheets API
   - Google Drive API

### Étape 2 : Configurer OAuth 2.0

1. Dans Google Cloud Console, allez dans **APIs & Services > Credentials**
2. Cliquez sur **Create Credentials > OAuth 2.0 Client IDs**
3. Configurez l'écran de consentement OAuth si ce n'est pas déjà fait
4. Choisissez **Web application** comme type d'application
5. Ajoutez les URIs autorisées :
   - **Authorized JavaScript origins** : `http://localhost:8000` (ou votre domaine)
   - **Authorized redirect URIs** : `http://localhost:8000` (ou votre domaine)

### Étape 3 : Obtenir le Client ID

1. Copiez le **Client ID** généré
2. Ouvrez le fichier `app.js`
3. Remplacez `YOUR_GOOGLE_CLIENT_ID` par votre Client ID :

```javascript
const CONFIG = {
    GOOGLE_CLIENT_ID: 'votre-client-id-ici.apps.googleusercontent.com',
    // ...
};
```

## 🖥️ Installation et Lancement

### Option 1 : Serveur local simple

```bash
# Avec Python 3
python -m http.server 8000

# Avec Python 2
python -m SimpleHTTPServer 8000

# Avec Node.js (si vous avez http-server installé)
npx http-server -p 8000
```

### Option 2 : Live Server (VS Code)

1. Installez l'extension "Live Server" dans VS Code
2. Clic droit sur `index.html` > "Open with Live Server"

### Option 3 : Serveur web local

Vous pouvez utiliser n'importe quel serveur web local. L'important est que l'application soit servie via HTTP/HTTPS et non pas ouverte directement comme fichier.

## 📖 Guide d'utilisation

### 1. Connexion

1. Ouvrez l'application dans votre navigateur
2. Cliquez sur le bouton de connexion Google
3. Autorisez l'accès à vos Google Sheets

### 2. Configuration des critères

1. Cliquez sur **"+ Ajouter un Critère"**
2. Donnez un nom à votre critère (ex: "Entreprises intéressantes")
3. Sélectionnez :
   - Le fichier Google Sheets contenant vos critères
   - La feuille appropriée
   - La colonne contenant les valeurs de critères
   - La colonne correspondante dans vos données cibles
4. Répétez pour tous vos critères

### 3. Configuration des données

**Données à analyser :**
- Sélectionnez le fichier contenant les profils à analyser
- Choisissez la feuille appropriée

**Destination des résultats :**
- Sélectionnez le fichier où exporter les résultats
- Choisissez la feuille de destination

### 4. Configuration de l'IA

Le prompt par défaut est optimisé pour la plupart des cas d'usage. Vous pouvez l'ajuster pour :
- Modifier la tolérance aux fautes d'orthographe
- Ajouter des règles spécifiques à votre domaine
- Ajuster la sensibilité aux variations linguistiques

### 5. Lancement du traitement

1. Cliquez sur **"🚀 Démarrer l'Analyse"**
2. Suivez la progression en temps réel
3. Les résultats seront automatiquement exportés vers votre feuille de destination

## 🔧 Personnalisation

### Ajuster la taille des lots

Dans `app.js`, modifiez `BATCH_SIZE` pour optimiser les performances :

```javascript
const CONFIG = {
    // ...
    BATCH_SIZE: 50, // Réduisez si vous avez des timeouts, augmentez pour plus de vitesse
    // ...
};
```

### Modifier le prompt IA

Le prompt peut être personnalisé directement dans l'interface ou modifié par défaut dans la fonction `generateDefaultPrompt()`.

## 🚨 Résolution des problèmes

### Erreur "Unauthorized"
- Vérifiez que votre Client ID est correct
- Assurez-vous que l'URI de votre application est autorisée dans Google Cloud Console

### Erreur "API not enabled"
- Activez Google Sheets API et Google Drive API dans Google Cloud Console

### Timeouts ou erreurs de taux
- Réduisez `BATCH_SIZE` dans la configuration
- Augmentez les délais entre les lots

### Correspondances manquées
- Ajustez le prompt IA pour être plus ou moins strict
- Vérifiez que vos critères sont bien configurés

## 📊 Exemple d'utilisation

**Cas d'usage :** Trouver des profils LinkedIn correspondant à des critères spécifiques

1. **Fichier A** : Liste d'entreprises intéressantes (colonne "Nom entreprise")
2. **Fichier B** : Liste de postes intéressants (colonne "Intitulé poste")
3. **Fichier C** : Base de profils LinkedIn avec colonnes "Entreprise actuelle" et "Poste actuel"

**Configuration :**
- Critère 1 : Entreprises (Fichier A, colonne "Nom entreprise" → Fichier C, colonne "Entreprise actuelle")
- Critère 2 : Postes (Fichier B, colonne "Intitulé poste" → Fichier C, colonne "Poste actuel")

**Résultat :** Tous les profils qui travaillent dans une entreprise intéressante ET occupent un poste intéressant.

## 🔒 Sécurité

### Variables d'Environnement
- **Production** : Les clés API sont injectées via GitHub Secrets lors du déploiement
- **Développement** : Les clés sont dans `config.js` (exclu du dépôt Git)
- **Jamais de clés en dur** : Le code public ne contient aucune clé sensible

### Authentification et Données
- L'application utilise OAuth 2.0 pour une authentification sécurisée
- Aucune donnée n'est stockée sur des serveurs externes
- Toutes les opérations se font directement entre votre navigateur et les APIs Google/OpenAI
- Accès restreint : Seuls les utilisateurs autorisés dans Google Cloud Console peuvent utiliser l'application

### Bonnes Pratiques
- ⚠️ **Important** : Ne jamais commiter de clés API dans le dépôt
- 🔐 **GitHub Secrets** : Utilisez toujours les secrets GitHub pour les clés de production
- 🌐 **Domaines autorisés** : Configurez précisément les origines autorisées dans Google Cloud Console

## 📝 Licence

Ce projet est fourni tel quel pour usage personnel et professionnel.

## 🆘 Support

Pour toute question ou problème, vérifiez d'abord la section "Résolution des problèmes" ci-dessus.