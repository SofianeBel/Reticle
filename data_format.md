# Reticle - Spécification du Format de Données v0.1

Ce document définit la structure du fichier `session_data.json` exporté par Reticle. Ce format est figé pour le MVP pour garantir la stabilité de la pipeline de données.

## Structure de l'objet JSON

Chaque événement (capture de frame, clic) génère un objet JSON avec la structure suivante. Le fichier d'export est un tableau de ces objets.

```json
[
  {
    "timestamp": 172000932.123,
    "mouse_x": 312,
    "mouse_y": 456,
    "normalized_x": 0.1625,
    "normalized_y": 0.4222,
    "click": true,
    "target_visible": true,
    "heatmap_bucket": "top-left"
  }
]
```

## Description des champs

-   `timestamp` (float): Timestamp UNIX avec millisecondes de l'événement. Essentiel pour l'analyse temporelle.
-   `mouse_x` (int): Coordonnée X absolue du curseur (en pixels).
-   `mouse_y` (int): Coordonnée Y absolue du curseur (en pixels).
-   `normalized_x` (float): Coordonnée X normalisée entre 0.0 et 1.0. **Crucial pour la heatmap et l'analyse indépendante de la résolution.**
-   `normalized_y` (float): Coordonnée Y normalisée entre 0.0 et 1.0. **Crucial pour la heatmap et l'analyse indépendante de la résolution.**
-   `click` (bool): `true` si un clic de souris a eu lieu durant cette frame.
-   `target_visible` (bool): `true` si le moteur d'analyse estime qu'une cible est présente à l'écran. (Logique simplifiée pour le MVP).
-   `heatmap_bucket` (string): Catégorise la position du clic dans une zone prédéfinie de l'écran (ex: "top-left", "center", "bottom-right"). Permet de construire la heatmap de manière optimisée. 