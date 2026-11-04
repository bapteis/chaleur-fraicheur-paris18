# Chaleur, fraîcheur et fréquentation dans le 18e arrondissement de Paris : carte de référence

Une carte qui réunit, en **données ouvertes**, ce qui fait chauffer le 18e, les lieux frais, la population exposée et la fréquentation des lieux d'attente. Elle sert à repérer les **points chauds** : zones chaudes, éloignées d'un lieu frais, densément peuplées ou habitées par des personnes fragiles.

- 🗺️ **Carte uMap** : [Chaleur, fraîcheur et fréquentation – 18e (référence)](https://umap.incubateur.anct.gouv.fr/fr/map/chaleur-fraicheur-et-frequentation-18e-reference_7188#16/48.889873/2.346449)
- 📄 **Méthode détaillée** : [methode_reference.html](methode_reference.html) en ligne : https://bapteis.github.io/chaleur-fraicheur-paris18/methode_reference.html

Chaque calque a sa légende dans le panneau des calques d'uMap, et chaque objet affiche ses chiffres au clic. Les données de la carte sont téléchargeables depuis uMap (menu « Exporter »).

## Ce que contient la carte

| Thème | Couches |
|---|---|
| **Chaleur** | îlots de chaleur urbains, aléa de jour et de nuit (Institut Paris Région) |
| **Fraîcheur** | îlots de fraîcheur de la Ville (espaces verts, équipements et activités) ; fontaines et brumisateurs Eau de Paris |
| **Éloignement du frais** | grille de 50 m : distance au lieu frais le plus proche, et sept zones à plus de 200 m |
| **Population** | INSEE Filosofi 2019, carreaux de 200 m : habitants, enfants de 0-3 ans, personnes de 65 ans et plus, ménages pauvres, logements sociaux, et part de personnes fragiles à la chaleur |
| **Fréquentation** | validations du métro un jour ouvré de juin (taille des stations), bouches de métro, passages de bus et tram, commerces |
| **Lieux d'attente** | rues aux écoles, aires piétonnes, marchés, Paris Respire, écoles, crèches, aires de jeux, bancs |
| **Contexte** | quartiers prioritaires de la politique de la ville (QPV 2024), limite de l'arrondissement |

## Comment elle est faite

1. **Lieux frais** : tous les îlots de fraîcheur de la Ville (espaces verts, piscines, bibliothèques, églises, musées, brumisateurs…) et les brumisateurs Eau de Paris.
2. **Éloignement** : sur une grille de 50 m, distance à vol d'oiseau au lieu frais le plus proche. Au-delà de 200 m (3 à 4 minutes de marche), une cellule est jugée éloignée.
3. **Population** : carreaux INSEE de 200 m, répartis sur la grille au prorata de la surface. Les personnes fragiles à la chaleur sont les enfants de 0-3 ans et les personnes de 65 ans et plus.
4. **Fréquentation** : passages de bus et tram entre 11h et 19h (horaires GTFS), validations du métro en juin hors vacances scolaires, commerces OpenStreetMap.

Le détail, les formules et les limites sont dans la [méthode](methode_reference.html).

### Principal résultat

Environ **17 600 habitants (10 %)** vivent à plus de 200 m à vol d'oiseau d'un lieu frais. Plus de la moitié sont dans la zone de la rue Ordener, entre la rue des Poissonniers et Marx Dormoy (environ 10 800 habitants). Les personnes fragiles à la chaleur représentent 19 % des habitants du 18e.

C'est une aide à la lecture du territoire, pas une mesure de température : aucun capteur ne couvre finement le 18e en données ouvertes. Horaires d'ouverture non pris en compte, distance à vol d'oiseau et non à pied, population de 2019.

## Sources

- **Île-de-France Mobilités** : horaires GTFS (passages, bouches de métro), validations du réseau ferré par jour, zones de correspondance.
- **Ville de Paris** (opendata.paris.fr) :
  - îlots de fraîcheur (espaces verts frais ; équipements et activités) ;
  - espaces verts, aires piétonnes et rues aux écoles, marchés découverts, Paris Respire ;
  - plan de voirie, arrondissements.
- **Eau de Paris** : fontaines à boire et brumisateurs.
- **Institut Paris Région** : îlots de chaleur urbains, aléa de jour et de nuit (2022).
- **INSEE** : Filosofi 2019, données carroyées à 200 m (via la Géoplateforme IGN).
- **ANCT** : quartiers prioritaires de la politique de la ville 2024.
- **OpenStreetMap** (© les contributeurs OpenStreetMap, via Geofabrik) : bancs, commerces, écoles, crèches, aires de jeux.

## Licence

Texte et données produites : [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/), car elles contiennent des données OpenStreetMap et Ville de Paris sous ODbL. Mentionner : « © bapteis, données IDFM, Ville de Paris, Eau de Paris, Institut Paris Région, INSEE, ANCT, © contributeurs OpenStreetMap ».
