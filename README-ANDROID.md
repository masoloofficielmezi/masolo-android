# Masolo — application Android (https://masolo.site.je/)

Coque native Kotlin qui affiche votre site dans une WebView : envoi de photos / vidéos / documents, téléchargements,
confirmations, bouton retour, page « hors connexion », session conservée. Android 8.0 et plus.
L'adresse du site est dans `gradle.properties` (`MASOLO_PROD_URL`).

## Option A — APK dans le cloud avec GitHub (sans rien installer)
1. Décompresser `masolo-android.zip`.
2. github.com → **New repository** → nom `masolo-android` → Create repository.
3. **uploading an existing file** → glisser **tout le contenu** du dossier décompressé (y compris le dossier caché `.github`) → *Commit changes*.
   Si `.github` n'a pas été envoyé : *Add file → Create new file*, nom `.github/workflows/android.yml`, coller le contenu du fichier `android.yml`.
4. Onglet **Actions** → **Build APK** → **Run workflow** → attendre 5 à 10 minutes (pastille verte).
5. Ouvrir l'exécution → section **Artifacts** → télécharger **Masolo-APK** → décompresser : `Masolo.apk`.
6. Sur le téléphone : copier `Masolo.apk`, l'ouvrir, autoriser « Installer des applis inconnues » pour l'application utilisée, installer.

## Option B — Android Studio
*Open* sur le dossier → synchronisation → *Build > Build Bundle(s)/APK(s) > Build APK(s)* (débogage) ou *Generate Signed Bundle / APK* (release).

## Si le HTTPS n'est pas encore actif
Le site doit répondre en `https://`. Sinon, dans `gradle.properties` : `MASOLO_PROD_URL=http://masolo.site.je/` et `MASOLO_ALLOW_HTTP=true`,
puis recompiler. Repasser en https/false dès que le certificat SSL est actif.

## Option C — Sans code : PWABuilder
Le site est installable (manifeste + service worker, HTTPS requis). Sur pwabuilder.com, saisir `https://masolo.site.je/` →
*Package for stores* → Android → télécharger. (Service tiers : vérifier ses conditions actuelles.)

## Notes
- L'APK « release » produit ici est signé avec la clé de débogage : installable directement. Pour le Play Store, créer votre propre clé
  (`keytool -genkey -v -keystore masolo.jks -keyalg RSA -keysize 2048 -validity 10000 -alias masolo`) et renseigner les lignes
  `MASOLO_KEYSTORE…` de `gradle.properties` ; augmenter `versionCode` à chaque version.
- Changer d'adresse de site = modifier `MASOLO_PROD_URL` et recompiler.
- Pas de notifications quand l'application est fermée (nécessite Firebase Cloud Messaging).
