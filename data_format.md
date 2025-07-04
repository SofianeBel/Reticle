# 📊 Format des données JSON - Reticle v0.1

Chaque session produit un fichier JSON dans `/logs`. Ce fichier est un tableau d'objets, où chaque objet représente un événement capturé.

## Exemple d'objet

```json
[
  {
    "timestamp": 17230000.123,
    "mouse_x_norm": 0.42,
    "mouse_y_norm": 0.76,
    "click": true,
    "target_visible": true,
    "heatmap_bucket": "top-right"
  }
]
```

## Description des champs

-   `timestamp` (float): Temps UNIX ou relatif en secondes, avec précision à la milliseconde.
-   `mouse_x_norm` (float): Position X du curseur normalisée entre `0.0` (gauche) et `1.0` (droite).
-   `mouse_y_norm` (float): Position Y du curseur normalisée entre `0.0` (haut) et `1.0` (bas).
-   `click` (bool): `true` si un clic de souris a eu lieu durant cet événement.
-   `target_visible` (bool): `true` si le moteur d'analyse estime qu'une cible est présente à l'écran.
-   `heatmap_bucket` (string): Nom de la zone de l'écran où l'événement a eu lieu (ex: "center", "bottom-left"). 