# Déploiement d'une application React sur Android

Ce guide explique comment transformer une application React en application Android installable (.apk), en passant par la génération d'un fichier AAB (Android App Bundle).

## Prérequis

- Node.js et npm installés
- Une application React fonctionnelle
- Compte Expo (gratuit)

## Étape 1 : Transformer votre application React en application mobile

1. Installez les outils Expo CLI :
```bash
npm install -g eas-cli
```

2. Connectez-vous à votre compte Expo :
```bash
npx eas login
```

3. Dans votre projet React, initialisez la configuration EAS :
```bash
npx eas build:configure
```

4. Configurez votre projet pour un build Android en créant ou modifiant le fichier `eas.json` :
```json
{
  "build": {
    "production": {
      "android": {
        "buildType": "app-bundle"
      }
    }
  }
}
```

5. Lancez la commande pour générer le fichier AAB :
```bash
npx eas build -p android
```

6. Suivez les instructions à l'écran. À la fin du processus, Expo vous fournira un lien pour télécharger votre fichier AAB.

## Étape 2 : Convertir le fichier AAB en APK

Le fichier AAB (Android App Bundle) est le format officiel pour le Google Play Store, mais pour installer directement l'application sur un appareil, vous avez besoin d'un fichier APK.

### Option 1 : Utiliser une application mobile de conversion

Il existe plusieurs applications Android qui peuvent convertir directement un fichier AAB en APK sur votre téléphone :

1. Téléchargez une application de conversion AAB vers APK depuis le Play Store
2. Ouvrez l'application et sélectionnez votre fichier AAB
3. Lancez la conversion
4. Téléchargez le fichier APK généré

### Option 2 : Utiliser Bundletool en ligne de commande

Si vous préférez utiliser votre ordinateur :

1. Téléchargez [Bundletool](https://github.com/google/bundletool/releases)
2. Exécutez la commande suivante :
```bash
java -jar bundletool.jar build-apks --bundle=votre_app.aab --output=votre_app.apks --mode=universal
```
3. Extrayez l'APK :
```bash
java -jar bundletool.jar extract-apks --apks=votre_app.apks --output-dir=./apk-output
```

## Étape 3 : Distribuer votre APK

1. Hébergez le fichier APK sur un service comme Google Drive, Dropbox ou votre propre serveur
2. Créez un QR code pointant vers le lien de téléchargement
3. Partagez ce QR code avec vos utilisateurs

## Remarques importantes

- Les utilisateurs devront activer "Installation d'applications de sources inconnues" dans les paramètres de leur appareil Android
- Cette méthode convient pour les tests et la distribution limitée
- Pour une distribution à grande échelle, envisagez de publier sur le Google Play Store (frais unique de 25$)

## Dépannage

Si vous rencontrez des erreurs lors du build :
- Vérifiez que votre application React est compatible avec React Native
- Assurez-vous d'avoir les dernières versions des outils Expo
- Consultez les logs d'erreur pour identifier les problèmes spécifiques