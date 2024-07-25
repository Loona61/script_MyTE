Script de remplissage automatique du Working Hours dans le MyTE


Ce script rempli automatiquement les horaires dans le Working Hours en ce basant sur le Work Schedule défini, il prend donc en charge aussi les semaines Flex sur des semaines en 37h.

Work Schedule pris en charge : 7.5 / 7 / 8.5 / 3
(Il est possible de rajouter d’autre prise en charge à la demande)

1.	Version sans aucune installation

- Il suffit de télécharger ce script (ouvrir le lien puis clic droit -enregistrer)
https://github.com/Loona61/script_MyTE/raw/main/workingHoursScriptManuel.js
- aller sur votre MyTE
- ouvrir la console du navigateur (F12)
- glisser le script dans la console au niveau du >
 
Si tout se passe bien vous devriez voir apparaitre le script
 

ATTENTION : Si c’est la première fois que vous le faite votre navigateur peut vous demander de taper une phrase dans la console pour pouvoir l’utiliser. Un message jaune apparaitra dans la console avec la phrase à écrire, une fois que ce sera fait, vous pourrez de nouveau faire l’étape où vous glissez le script.


2.	Version entièrement automatique avec Tampermonkey
(Cette version ajoute un bouton directement sur votre MyTE pour remplir automatiquement le Working Hours)

- Ajouter l’extension Tampermonkey sur votre navigateur en allant sur ce lien :
https://www.tampermonkey.net/index.php

- choisissez l’onglet correspondant au navigateur sur lequel vous voulez ajouter l’extension puis sur le bouton « Get from Store » de la première version proposé (NON BETA ou LEGACY)

- vous allez être redirigé vers le store du navigateur ou un bouton vous proposera de l’ajouter / l’installer (cela varie en fonction des navigateurs)

- il suffit ensuite d’ouvrir ce lien sur le navigateur ou vous avez installé Tampermonkey :
https://github.com/Loona61/script_MyTE/raw/main/Auto-fill-WorkingHours.user.js
- un onglet Tampermonkey va s’ouvrir en vous montrant le script , cliquez sur « Install »

- vous pouvez maintenant fermer l’onglet Tampermonkey et lancer votre page MyTE pour voir apparaitre le bouton "AutoFill" sur la ligne du Working Hours
 

- Il ne reste plus qu’à cliquer dessus et le laisser remplir 😊


Problèmes connus :

- si vous utilisez la traduction automatique en français du navigateur , il se peut que le script fonctionne mal car il n’arrivera pas a interprété les dates qui changent de format et qui passe parfois en toute lettres.


