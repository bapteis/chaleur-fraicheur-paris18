# Chaleur, fraîcheur et ombrières dans le 18e arrondissement de Paris

Où installer en priorité des **ombrières** et des **brumisateurs** dans le 18e ? Et, plus largement, où fait-il chaud, où sont les lieux frais, qui habite loin de ces lieux ? Ce dépôt réunit une analyse en **données ouvertes**, deux cartes interactives et un projet QGIS réutilisables.

- 🗺️ **Carte des propositions** : [lien uMap à compléter]
- 🗺️ **Carte de référence** (chaleur, fraîcheur, population, fréquentation, sans les propositions) : [lien uMap à compléter]
- 📄 **Méthode détaillée** : [resultats/methode.html](resultats/methode.html) (en ligne : `https://<compte>.github.io/<depot>/resultats/methode.html`)

## Ce que fait l'analyse

1. **Lieux comparés** : 360 lieux où l'on attend ou reste un moment : arrêts de bus et tram, sorties de métro, rues aux écoles, aires piétonnes, marchés, squares, aires de jeux.
2. **Critères** :
   - fréquentation (passages de bus, validations du métro en juin, commerces) ;
   - type de lieu et bancs ;
   - exposition au soleil le 15 juillet de 11h à 19h, calculée sur le LiDAR HD de l'IGN ;
   - végétation, aléa de chaleur (Institut Paris Région) ;
   - quartiers prioritaires (QPV 2024), brumisateurs existants.
3. **Règles** : pas d'ombrière dans les squares, aires de jeux et îlots de fraîcheur (déjà végétalisés). 500 m au moins entre deux propositions.
4. **Éloignement des lieux frais** : distance, sur une grille de 50 m, au plus proche îlot de fraîcheur de la Ville ou brumisateur. Le résultat est croisé avec la population INSEE (carreaux de 200 m), dont les personnes fragiles à la chaleur (enfants de 0-3 ans et personnes de 65 ans et plus).

### Principaux résultats

- **5 ombrières proposées** : Porte de Clignancourt, rue Richomme (rue aux écoles, Goutte d'Or), Porte de la Chapelle, marché Ney, aire piétonne rue Duhesme.
- **3 brumisateurs proposés** : Porte de Clignancourt, aire de jeux rue de l'Évangile, aire piétonne rue René Binet.
- **Environ 17 600 habitants (10 %)** vivent à plus de 200 m à vol d'oiseau d'un lieu frais. Plus de la moitié sont dans la zone de la rue Ordener, entre la rue des Poissonniers et Marx Dormoy (environ 10 800 habitants).

Ces résultats sont une aide à la décision, à vérifier sur le terrain : faisabilité technique, réseaux, largeur des trottoirs, usages réels.

## Contenu

| Fichier | Contenu |
|---|---|
| `resultats/carte_ombrieres_18e.umap` | carte uMap complète (Importer dans [uMap](https://umap.openstreetmap.fr)) |
| `resultats/carte_reference_18e.umap` | carte uMap sans les propositions, pour d'autres sujets |
| `resultats/carte_18e.qgz` | projet QGIS (≥ 3.28), couches rangées par thème et stylées |
| `resultats/analyse_ombrieres_18e.gpkg` | toutes les couches (GeoPackage, styles inclus) |
| `resultats/lidar_hauteur_18.tif` | hauteur au-dessus du sol en mètres (LiDAR HD IGN), pour QGIS |
| `resultats/classement_lieux_sejour_18e.xlsx` | classement des 360 lieux, avec liens Street View |
| `resultats/classement_lieux_18e.xlsx` | première version : arrêts de bus et tram seuls |
| `resultats/methode.html` | méthode, limites, parcours QGIS « points chauds » |
| `scripts/` | le calcul complet (Python) |
| `donnees_sources/` | données sources téléchargées (sauf les plus lourdes, voir ci-dessous) |

Pour QGIS, téléchargez le dossier `resultats/` et ouvrez `carte_18e.qgz`. Le projet, le GeoPackage et le raster doivent rester dans le même dossier.

## Reproduire le calcul

Python 3.11 ou plus récent :

```
pip install -r requirements.txt
```

Trois sources trop lourdes ne sont pas dans le dépôt :

| Fichier attendu dans `donnees_sources/` | Où le trouver |
|---|---|
| `IDFM-gtfs.zip` | [Horaires GTFS IDFM](https://data.iledefrance-mobilites.fr/explore/dataset/offre-horaires-tc-gtfs-idfm/) (`https://eu.ftp.opendatasoft.com/stif/GTFS/IDFM-gtfs.zip`) |
| `ile-de-france-260421-free.gpkg/ile-de-france.gpkg` | extrait OpenStreetMap « free » Île-de-France de [Geofabrik](https://download.geofabrik.de/europe/france/ile-de-france.html), au format GeoPackage. Adapter le chemin `OSM` dans `scripts/commun.py` si besoin |
| `lidar_mns_18.tif`, `lidar_mnh_18.tif` | téléchargés automatiquement au premier lancement (WMS-R de la Géoplateforme IGN) |

Ordre de lancement, depuis `scripts/` :

```
python 01_passages_gtfs.py      # passages de bus et tram par arrêt (GTFS)
python 02_analyse_lieux.py      # arrêts de bus et tram, abris
python 04_lieux_sejour.py       # tous les lieux, scores, propositions
python 05_couches_reference.py  # couches de référence, population, éloignement du frais
python 03_export_umap.py        # cartes uMap
"C:\Program Files\QGIS 3.xx\bin\python-qgis-ltr.bat" 06_styles_qgis.py   # styles et projet QGIS
```

Corrections de terrain : `donnees_sources/corrections_terrain.csv` (lignes de bus déviées à retirer d'un arrêt).

## Sources

- **Île-de-France Mobilités** : horaires GTFS (passages, bouches de métro), validations du réseau ferré par jour (2e trimestre 2026), zones de correspondance.
- **Ville de Paris** (opendata.paris.fr) :
  - îlots de fraîcheur (espaces verts frais ; équipements et activités) ;
  - arbres, espaces verts, aires piétonnes et rues aux écoles, marchés découverts, Paris Respire ;
  - plan de voirie, arrondissements.
- **Eau de Paris** : fontaines à boire et brumisateurs.
- **IGN** : BD TOPO (bâtiments, voies ferrées), LiDAR HD (modèles numériques de surface et de hauteur).
- **Institut Paris Région** : îlots de chaleur urbains, aléa de jour et de nuit (2022).
- **INSEE** : Filosofi 2019, données carroyées à 200 m (via la Géoplateforme IGN).
- **ANCT** : quartiers prioritaires de la politique de la ville 2024.
- **OpenStreetMap** (© les contributeurs OpenStreetMap, via Geofabrik) : bancs, commerces, écoles, crèches, aires de jeux.

## Licence

- **Code** (`scripts/`) : licence MIT, voir [LICENSE](LICENSE).
- **Données produites** (`resultats/`) : [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/), car elles contiennent des données OpenStreetMap et Ville de Paris sous ODbL. Mentionner : « © [nom de l'auteur], données IDFM, Ville de Paris, Eau de Paris, IGN, Institut Paris Région, INSEE, ANCT, © contributeurs OpenStreetMap ».
- **Données sources** (`donnees_sources/`) : licences de leurs producteurs respectifs (ODbL ou Licence Ouverte Etalab).
