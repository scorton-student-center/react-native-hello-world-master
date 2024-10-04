Vous trouverez ci-dessous des informations sur l’exécution de tâches courantes. La version la plus récente de ce guide est disponible ici.

## Table des matières

Mise à jour vers les nouvelles versions
Scripts disponibles
npm start
npm test
npm run ios
npm run android
npm run eject
Écriture et exécution de tests
Variables d’environnement
Configuration de l’adresse IP du packager
Ajout de Flow
Personnalisation du nom d’affichage et de l’icône de l’application
Partage et déploiement
Publication sur la communauté React Native d’Expo
Création d’une application « autonome » Expo
Éjection de Create React Native App
Dépendances de build (Xcode et Android Studio)
Dois-je utiliser ExpoKit ?
Dépannage
Réseau
Le simulateur iOS ne s’ouvre pas
Le code QR ne se scanne pas
## Mise à jour vers les nouvelles versions

Vous ne devriez avoir besoin de mettre à jour l’installation globale de create-react-native-app que très rarement, idéalement jamais.

La mise à jour de la dépendance react-native-scripts de votre application devrait être aussi simple que d’augmenter le numéro de version dans package.json et de réinstaller les dépendances de votre projet.

La mise à niveau vers une nouvelle version de React Native nécessite la mise à jour des versions des packages react-native, react et expo, et la définition du sdkVersion correct dans app.json. Consultez le guide des versions pour obtenir des informations à jour sur la compatibilité des versions des packages.

## Scripts disponibles

Si Yarn a été installé lors de l’initialisation du projet, les dépendances auront été installées via Yarn, et vous devriez probablement l’utiliser pour exécuter ces commandes également. Contrairement à l’installation des dépendances, la syntaxe d’exécution des commandes est identique pour Yarn et NPM au moment de la rédaction de ce document.

### npm start

Exécute votre application en mode développement.

Ouvrez-la dans l’application Expo sur votre téléphone pour la visualiser. Elle se rechargera si vous enregistrez des modifications dans vos fichiers, et vous verrez les erreurs de build et les journaux dans le terminal.

Parfois, vous devrez peut-être réinitialiser ou effacer le cache du packager React Native. Pour ce faire, vous pouvez passer l’indicateur --reset-cache au script de démarrage :


Copy
npm start --reset-cache
# ou
yarn start --reset-cache
#### npm test

Exécute le programme d’exécution de tests jest sur vos tests.

#### npm run ios

Comme npm start, mais tente également d’ouvrir votre application dans le simulateur iOS si vous êtes sur un Mac et que vous l’avez installé.

#### npm run android

Comme npm start, mais tente également d’ouvrir votre application sur un appareil ou un émulateur Android connecté. Nécessite une installation des outils de build Android (voir la documentation React Native pour une configuration détaillée). Nous recommandons également d’installer Genymotion comme émulateur Android. Une fois que vous avez terminé la configuration de l’environnement de build natif, il existe deux options pour rendre la bonne copie de adb disponible pour Create React Native App :

Utilisation de adb d’Android Studio
Assurez-vous que vous pouvez exécuter adb à partir de votre terminal.
Ouvrez Genymotion et accédez à Paramètres -> ADB. Sélectionnez « Utiliser des outils SDK Android personnalisés » et mettez à jour avec votre répertoire Android SDK.
Utilisation de adb de Genymotion
Trouvez la copie de adb de Genymotion. Sur macOS par exemple, il s’agit normalement de /Applications/Genymotion.app/Contents/MacOS/tools/.
Ajoutez le répertoire des outils Genymotion à votre chemin (instructions pour Mac, Linux et Windows).
Assurez-vous que vous pouvez exécuter adb à partir de votre terminal.
#### npm run eject

Cela lancera le processus d’« éjection » des scripts de build de Create React Native App. On vous posera quelques questions sur la façon dont vous souhaitez créer votre projet.

Avertissement : L’exécution de l’éjection est une action permanente (mis à part le système de contrôle de version que vous utilisez). Une application éjectée nécessitera la configuration d’un environnement Xcode et/ou Android Studio.

## Personnalisation du nom d’affichage et de l’icône de l’application

Vous pouvez modifier app.json pour inclure des clés de configuration sous la clé expo.

Pour modifier le nom d’affichage de votre application, définissez la clé expo.name dans app.json sur une chaîne appropriée.

Pour définir une icône d’application, définissez la clé expo.icon dans app.json sur un chemin local ou une URL. Il est recommandé d’utiliser un fichier png 512x512 avec transparence.

## Écriture et exécution de tests

Ce projet est configuré pour utiliser jest pour les tests. Vous pouvez configurer la stratégie de test de votre choix, mais jest fonctionne dès la sortie de la boîte. Créez des fichiers de test dans des répertoires appelés __tests__ ou avec l’extension .test pour que les fichiers soient chargés par jest. Consultez le projet modèle pour un exemple de test. La documentation jest est également une excellente ressource, tout comme le tutoriel de test React Native.

## Variables d’environnement

Vous pouvez configurer certains comportements de Create React Native App à l’aide de variables d’environnement.

### Configuration de l’adresse IP du packager

Lorsque vous démarrez votre projet, vous verrez quelque chose comme ceci pour l’URL de votre projet :


Copy
exp://192.168.0.2:19000
Le « manifeste » à cette URL indique à l’application Expo comment récupérer et charger le bundle JavaScript de votre application, donc même si vous le chargez dans l’application via une URL comme exp://localhost:19000, l’application cliente Expo tentera toujours de récupérer votre application à l’adresse IP fournie par le script de démarrage.

Dans certains cas, ce n’est pas idéal. Cela peut être le cas si vous devez exécuter votre projet dans une machine virtuelle et que vous devez accéder au packager via une adresse IP différente de celle qui s’affiche par défaut. Afin de remplacer l’adresse IP ou le nom d’hôte détecté par Create React Native App, vous pouvez spécifier votre propre nom d’hôte via la variable d’environnement REACT_NATIVE_PACKAGER_HOSTNAME :

Mac et Linux :


Copy
REACT_NATIVE_PACKAGER_HOSTNAME='my-custom-ip-address-or-hostname' npm start
Windows :


Copy
set REACT_NATIVE_PACKAGER_HOSTNAME='my-custom-ip-address-or-hostname'
npm start
L’exemple ci-dessus ferait en sorte que le serveur de développement écoute sur exp://my-custom-ip-address-or-hostname:19000.

## Ajout de Flow

Flow est un vérificateur de type statique qui vous aide à écrire du code avec moins de bogues. Consultez cette introduction à l’utilisation des types statiques en JavaScript si vous débutez avec ce concept.

React Native fonctionne avec Flow dès la sortie de la boîte, tant que votre version de Flow correspond à celle utilisée dans la version de React Native.

Pour ajouter une dépendance locale à la bonne version de Flow à un projet Create React Native App, suivez ces étapes :

Trouvez la version Flow [version] au bas du fichier .flowconfig inclus.
Exécutez npm install --save-dev flow-bin@x.y.z (ou yarn add --dev flow-bin@x.y.z), où x.y.z est le numéro de version .flowconfig.
Ajoutez "flow": "flow" à la section scripts de votre fichier package.json.
Ajoutez // @flow à tous les fichiers que vous souhaitez vérifier par rapport aux types (par exemple, à App.js).
Vous pouvez maintenant exécuter npm run flow (ou yarn flow) pour vérifier les fichiers afin de détecter les erreurs de type.
Vous pouvez éventuellement utiliser un plugin pour votre IDE ou votre éditeur pour une meilleure expérience intégrée.

Pour en savoir plus sur Flow, consultez sa documentation.

## Partage et déploiement

Create React Native App effectue beaucoup de travail pour simplifier et rendre la configuration et le développement d’applications simples et directs, mais il est très difficile de faire de même pour le déploiement sur l’App Store d’Apple ou le Play Store de Google sans s’appuyer sur un service hébergé.

### Publication sur la communauté React Native d’Expo

Expo fournit un hébergement gratuit pour les applications uniquement JS créées par CRNA, vous permettant de partager votre application via l’application cliente Expo. Cela nécessite l’inscription à un compte Expo.

Installez l’outil de ligne de commande exp et exécutez la commande de publication :


Copy
$ npm i -g exp
$ exp publish
### Création d’une application « autonome » Expo

Vous pouvez également utiliser un service comme les builds autonomes d’Expo si vous souhaitez obtenir un IPA/APK pour la distribution sans avoir à créer vous-même le code natif.

### Éjection de Create React Native App

Si vous souhaitez créer et déployer vous-même votre application, vous devrez éjecter de CRNA et utiliser Xcode et Android Studio.

Ceci est généralement aussi simple que d’exécuter npm run eject dans votre projet, ce qui vous guidera tout au long du processus. Assurez-vous d’installer react-native-cli et suivez le guide de démarrage du code natif pour React Native.

#### Dois-je utiliser ExpoKit ?

Si vous avez utilisé des API Expo pendant que vous travailliez sur votre projet, ces appels d’API cesseront de fonctionner si vous éjectez vers un projet React Native ordinaire. Si vous souhaitez continuer à utiliser ces API, vous pouvez éjecter vers « React Native + ExpoKit », ce qui vous permettra toujours de créer votre propre code natif et de continuer à utiliser les API Expo. Consultez le guide d’éjection pour plus de détails sur cette option.

## Dépannage

### Réseau

Si vous ne parvenez pas à charger votre application sur votre téléphone en raison d’un délai d’expiration du réseau ou d’une connexion refusée, une première étape consiste à vérifier que votre téléphone et votre ordinateur sont sur le même réseau et qu’ils peuvent se joindre. Create React Native App a besoin d’accéder aux ports 19000 et 19001, assurez-vous donc que vos paramètres réseau et pare-feu autorisent l’accès de votre appareil à votre ordinateur sur ces deux ports.

Essayez d’ouvrir un navigateur Web sur votre téléphone et d’ouvrir l’URL que le script du packager affiche, en remplaçant exp:// par http://. Ainsi, par exemple, si sous le code QR dans votre terminal, vous voyez :


Copy
exp://192.168.0.1:19000
Essayez d’ouvrir Safari ou Chrome sur votre téléphone et de charger


Copy
http://192.168.0.1:19000
et


Copy
http://192.168.0.1:19001
Si cela fonctionne, mais que vous ne parvenez toujours pas à charger votre application en scannant le code QR, veuillez ouvrir un problème sur le référentiel Create React Native App avec des détails sur ces étapes et tous les autres messages d’erreur que vous avez pu recevoir.

Si vous ne parvenez pas à charger l’URL http dans le navigateur Web de votre téléphone, essayez d’utiliser la fonction de partage de connexion/point d’accès mobile sur votre téléphone (attention à la consommation de données), de connecter votre ordinateur à ce réseau Wi-Fi et de redémarrer le packager. Si vous utilisez un VPN, vous devrez peut-être le désactiver.

### Le simulateur iOS ne s’ouvre pas

Si vous êtes sur un Mac, il existe quelques erreurs que les utilisateurs voient parfois lorsqu’ils tentent d’exécuter npm run ios :

« code de sortie non nul : 107 »
« Vous devrez peut-être installer Xcode » mais il est déjà installé
et d’autres
Il y a quelques étapes que vous pouvez suivre pour résoudre ce type d’erreurs :

Assurez-vous que Xcode est installé et ouvrez-le pour accepter le contrat de licence s’il vous le demande. Vous pouvez l’installer à partir du Mac App Store.
Ouvrez les préférences de Xcode, l’onglet Emplacements, et assurez-vous que l’option de menu Outils de ligne de commande est définie sur quelque chose. Parfois, lorsque les outils CLI sont installés pour la première fois par Homebrew, cette option est laissée vide, ce qui peut empêcher les utilitaires Apple de trouver le simulateur. Assurez-vous de relancer npm/yarn run ios après cela.
Si cela ne fonctionne pas, ouvrez le simulateur et, dans le menu de l’application, sélectionnez Réinitialiser le contenu et les paramètres…. Une fois que cela est terminé, quittez le simulateur et relancez npm/yarn run ios.
