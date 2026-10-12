# Où sont les toilettes ? — premier MVP

Prototype web installable (PWA) pour Android, réalisé sans abonnement ni clé d'API. Le MVP utilise OpenStreetMap pour afficher la carte et OpenStreetMap/Overpass pour chercher les toilettes taguées `amenity=toilets` dans la zone visible.

## Ce qui fonctionne

- Carte interactive et marqueurs de toilettes réels présents dans OpenStreetMap.
- Résultats limités à la zone courante; zoom minimum volontaire pour éviter une requête sur tout le pays.
- Recherche textuelle parmi les résultats chargés, filtre accessibilité fauteuil roulant et filtre gratuit lorsque ces informations sont explicitement renseignées.
- Fiche OSM, détails connus et ouverture d'un itinéraire Google Maps.
- Position facultative via l'autorisation de localisation du navigateur; la carte reste utilisable sans.
- Coquille web mise en cache par le navigateur pour une réouverture possible. Les tuiles de carte et les données nécessitent Internet.

## Ce qui est réel et ce qui ne l'est pas

Les lieux affichés viennent de requêtes en direct à Overpass. Il n'y a pas de jeu de données France préchargé ni de faux lieux de démonstration. La couverture varie selon les contributions OSM; les toilettes absentes d'OSM ne peuvent pas apparaître. Les horaires, tarifs, accessibilité et état actuel sont parfois inconnus ou périmés. Le MVP ne garantit pas que le lieu soit ouvert ou accessible à votre arrivée.

## Lancer sur Windows (sans installer Android Studio)

1. Décompressez le ZIP dans un dossier facile à retrouver.
2. Installez gratuitement Python 3 depuis Microsoft Store ou python.org si `python` n'est pas reconnu.
3. Ouvrez le dossier décompressé dans l'Explorateur de fichiers.
4. Cliquez dans la barre d'adresse, tapez `powershell`, puis Entrée.
5. Dans la fenêtre PowerShell, tapez `python -m http.server 8000` puis Entrée.
6. Sur le PC, ouvrez `http://localhost:8000` dans Chrome ou Edge. Gardez la fenêtre PowerShell ouverte.

Pour tester sur Android : publiez les fichiers sur un hébergement statique HTTPS gratuit (par exemple GitHub Pages) ou démarrez le serveur avec accès réseau local et utilisez HTTPS. Dans Chrome Android, ouvrez le lien HTTPS, puis menu ⋮ → « Installer l'application » ou « Ajouter à l'écran d'accueil ». La géolocalisation et l'installation PWA nécessitent un contexte sécurisé (HTTPS, ou `localhost` sur l'appareil lui-même); une adresse HTTP locale en Wi-Fi peut ne pas les activer. Le ZIP s'exécute sur ordinateur immédiatement; il ne contient pas encore un APK Android.

## Limites des services gratuits publics

Overpass est un service communautaire sans SLA. Le projet attend entre les requêtes, ne lance qu'une requête à la fois, n'interroge qu'à partir d'un niveau de zoom local, plafonne à 150 éléments et essaie un second endpoint si le premier échoue. Ces mesures réduisent la charge mais ne garantissent pas l'accès. Une erreur ou réponse partielle peut survenir; réessayez plus tard. Pour un service public en production, il faudra prévoir une source de données appropriée, surveiller la charge et ne pas dépendre d'un endpoint public partagé.

Les tuiles standard OSM sont chargées uniquement à l'écran, sans préchargement hors ligne. Leur attribution est visible dans la carte et le panneau. Pour une app à audience substantielle ou une activité commerciale, sélectionner un fournisseur de tuiles avec des conditions adaptées.

## Licence et attribution

Les données OpenStreetMap sont © les contributeurs OpenStreetMap et disponibles sous ODbL; voir https://www.openstreetmap.org/copyright. Le code de ce prototype est fourni sous MIT (voir `LICENSE`). Leaflet est distribué sous BSD-2-Clause (https://github.com/Leaflet/Leaflet/blob/main/LICENSE). La carte est fournie par le serveur de tuiles standard OpenStreetMap, soumis à sa politique d'utilisation : https://operations.osmfoundation.org/policies/tiles/.

## Personnaliser

Le code est regroupé dans `index.html` pour rester simple à modifier. `manifest.webmanifest` décrit l'installation PWA, `sw.js` met en cache uniquement la coquille de l'application et `icon.svg` est l'icône. Pas de serveur applicatif, base locale, compte utilisateur ou publicité pour cette première version.
