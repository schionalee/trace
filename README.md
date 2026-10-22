# Tracé

Implantation de points d'accroche au télémètre laser, à partir d'un plan DXF, PDF ou CSV.

Chaque point est repéré par sa distance perpendiculaire à deux murs de référence (A et B). On mesure ces deux distances au télémètre, on marque le point au sol, puis on le reporte en hauteur au laser d'aplomb.

## Utilisation

1. **Plan** : charge un DXF (texte, pas binaire), un PDF vectoriel ou un CSV `nom;x;y;z`. Le fichier est lu sur l'appareil et n'est envoyé nulle part. Pour un PDF, vérifie l'échelle : elle est lue sur le plan quand elle y est écrite (« 1/200 »), sinon saisis-la ou calibre-la en touchant les deux bouts d'une cote connue.
2. **Repères** : touche deux murs du plan qui se coupent, et ajoute une correction en mm si le mur réel n'est pas à sa place sur le plan.
3. **Implanter** : pour chaque point, saisis les deux distances mesurées. L'écart s'affiche en direct par rapport à la tolérance, et tu valides le point. Le journal s'exporte en CSV.

## Mode télémètre

Pour un télémètre Bluetooth en « mode clavier » (Leica DISTO X3/X4…) : active le mode à l'étape Implanter et touche le champ « Mesure reçue ». Chaque mesure tapée par le télémètre (suivie d'Entrée, de Tab ou de rien) va au mur actif :

- mesure hors tolérance : bip grave, le mur reste actif, tu te décales et tu remesures ;
- mesure bonne : bip aigu, on passe à l'autre mur ;
- les deux bonnes : le point se valide seul (option) et on passe au suivant.

Les mesures en m, cm ou mm sont reconnues, avec point ou virgule. Une annonce vocale (« Rapproche-toi du mur A de 4 centimètres ») peut être activée. Vibration sur Android.

## Ce que l'outil gère

- Les gros DXF (plusieurs centaines de Mo), lus par morceaux.
- Le symbole d'accroche « cercle à quarts » (cercle + hachurage), reconnu automatiquement, même rangé dans d'autres blocs.
- Les blocs en miroir (extrusion 0,0,-1), l'échelle et la rotation des blocs imbriqués.
- Une unité annoncée dans le fichier ($INSUNITS) mais fausse, avec un avertissement.
- Les calques de murs masquables pour alléger le plan.
- Les PDF vectoriels (exportés depuis le logiciel de dessin, pas scannés) : traits, cercles et symbole « cercle à quarts », y compris quand les cercles sont découpés en petits traits. Les traits sont regroupés par couleur, les cercles simples par diamètre.

Le plan et l'avancement sont enregistrés dans le navigateur (IndexedDB et localStorage).

Les DWG ne sont pas lus : exporte-les en DXF.

## Fichier unique

Tout est dans `index.html`, sans étape de build. Depuis Internet, seules les polices Google Fonts sont chargées, plus [pdf.js](https://mozilla.github.io/pdf.js/) 3.11 (cdnjs) quand on ouvre un PDF.
