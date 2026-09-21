# gridz-public

Contenu public statique de Gridz.

## Pages legales et support — GitHub Pages

`politique-confidentialite/`, `support/`, `supprimer-compte/`, `rejoindre-test/`
sont servies par GitHub Pages sur `https://aa-hb.github.io/gridz-public/`.
Ces URL sont referencees dans les fiches Play Store et App Store : ne pas
ajouter de fichier `CNAME` ici sans mettre les fiches a jour, sinon GitHub
redirige tout et les liens des stores cassent.

## Lien d'installation — Firebase Hosting

`install/` est publie sur `https://play.gridz.fr` (site Hosting `gridz-link`
du projet `gridz-e580a`), et **pas** par GitHub Pages.

- `install/index.html` — redirige vers l'App Store, Google Play ou l'app web
  selon la plateforme. `?stay=1` desactive la redirection pour relire la page.
- `install/.well-known/apple-app-site-association` — Universal Links iOS
- `install/.well-known/assetlinks.json` — App Links Android

Les deux fichiers `.well-known` doivent etre servis en `application/json` :
c'est ce que garantit le bloc `headers` de `firebase.json`.

Deploiement :

```
firebase deploy --only hosting
```

Le domaine et les identifiants correspondants sont declares cote app dans
`gridz-app` : `android/app/src/main/AndroidManifest.xml` (intent-filter
`autoVerify` sur `play.gridz.fr`) et `ios/Runner/Runner.entitlements`
(`applinks:play.gridz.fr`). Changer de domaine impose de modifier les deux,
puis de republier l'app sur les stores : la verification App Links n'a lieu
qu'a l'installation.
