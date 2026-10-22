# Tracé

Implantation de points d'accroche au télémètre laser, à partir d'un plan DXF ou CSV.

Chaque point est repéré par sa distance perpendiculaire à deux murs de référence (A et B). On mesure ces deux distances au télémètre, on marque le point au sol, puis on le reporte en hauteur au laser d'aplomb.

## Utilisation

1. **Plan** : charge un DXF (texte, pas binaire) ou un CSV `nom;x;y;z`. Le fichier est lu sur l'appareil et n'est envoyé nulle part.
2. **Repères** : touche deux murs du plan qui se coupent, et ajoute une correction en mm si le mur réel n'est pas à sa place sur le plan.
3. **Implanter** : pour chaque point, saisis les deux distances mesurées. L'écart s'affiche en direct par rapport à la tolérance, et tu valides le point. Le journal s'exporte en CSV.

## Ce que l'outil gère

- Les gros DXF (plusieurs centaines de Mo), lus par morceaux.
- Le symbole d'accroche « cercle à quarts » (cercle + hachurage), reconnu automatiquement, même rangé dans d'autres blocs.
- Les blocs en miroir (extrusion 0,0,-1), l'échelle et la rotation des blocs imbriqués.
- Une unité annoncée dans le fichier ($INSUNITS) mais fausse, avec un avertissement.
- Les calques de murs masquables pour alléger le plan.

Le plan et l'avancement sont enregistrés dans le navigateur (IndexedDB et localStorage).

Les DWG ne sont pas lus : exporte-les en DXF.

## Fichier unique

Tout est dans `index.html`, sans dépendance ni étape de build. Seules les polices Google Fonts sont chargées depuis Internet.
