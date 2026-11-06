# P1Sim Arnage plugin — modifications

## P1Sim Arnage plugin 0.5.4

- **Fix rôle bloqué enfoncé** (ex. « SimRace Pitwall+ » restait pressé dans le Control mapper) : le relâchement du bouton −/+
  n'arrivait pas toujours → le rôle restait en `StartRole`. Chaque appui envoie désormais une impulsion
  `ControlMapperInterface.StartStopRole(rôle, 100 ms)` ; plus de dépendance au relâchement (adapté aussi aux crans d'encodeur).
  Chaque appui est journalisé dans `log.txt` (bouton, position, rôle, rôle introuvable).

## P1Sim Arnage plugin 0.5.3 + AutoRPM 0.5.0

- **P1Sim Arnage** : bouton ✕ à côté de « Apprendre » : annule l'apprentissage en cours et efface l'entrée apprise
  pour la position (évite de garder une mauvaise entrée).
- **AutoRPM 0.5.0** (nouveau dossier `AutoRPM/`, sources importées) : barres 8 à 15 LED (`N13_*` à `N15_*`), interface et
  états en 9 langues ; détails dans `AutoRPM/CHANGELOG.md`. Exclu de `SimRaceEngineer.csproj`.

## P1Sim Arnage plugin 0.5.2

- **Notice** : légendes agrandies (24 pt, gras, fond plein de la couleur du repère) et placées dans des marges
  de part et d'autre de la photo au lieu d'être sur les poignées ; cercles et traits plus épais.

## P1Sim Arnage plugin 0.5.1

- **Onglet LEDs** : bloc Télémétrie affiché deux fois (deux sous-appareils LEDs exposent le même bloc) → seul le
  sous-appareil le plus complet est affiché (section LEDs avec le curseur de luminosité, puis Controls).

## P1Sim Arnage plugin 0.5.0 — notice illustrée + aperçu des dashboards

- **Notice** (onglet Switchs FN) : photo de l'Arnage embarquée (`Resources/arnage.png`) avec repères numérotés —
  ① rotatif ABS = switch gauche 1-12, ② rotatif TC = switch droit 13-24, ③ encodeurs remappés pour − / + — et 5 étapes.
- **Aperçu des dashboards** (onglet Écran) : vignette `DashTemplates\<dash>\<dash>.djson.png` sous chaque choix, mise à jour à la sélection.

## P1Sim Arnage plugin 0.4.0 — LEDs gérées dans le plugin

- **Onglet LEDs RGB** : héberge l'interface LEDs native de SimHub de l'appareil « P1SIM Arnage »
  (`LedModuleDevice.GetSettingsControls()` : profil, éditer / importer, gestionnaire de profils, luminosité et balance).
  Mêmes réglages que Devices → LEDs (aucun doublon) ; les contrôles sont rendus à la page Devices quand on quitte le plugin.

## P1Sim Arnage plugin 0.3.0 — plugin autonome + look SimHub

- **Latching intégré** : le plugin fait lui-même le « momentary to latching ». Chaque position apprend son entrée
  SimHub (`PluginManager.InputPressed`, bouton « Apprendre » puis tourner le switch) → plus besoin des groupes FN
  du Control mapper (le FN reste en option si aucune entrée n'est apprise pour le switch).
- **Boutons − / + par la fenêtre de bind SimHub** (`ControlsEditor`, actions `ArnagePlugin.LeftMinus/LeftPlus/RightMinus/RightPlus`) ;
  le plugin déclenche directement le rôle de la position en cours via `ControlMapperInterface.StartRole/StopRole`
  (maintenu tant que le bouton est maintenu). Suppression de la génération de profil et des numéros de boutons.
- **Liste complète des rôles** du Control mapper (`GetAvailableButtonRoles`, rôles personnalisés inclus).
- **Roue des positions** : cadran 12 positions avec labels et aiguille sur la position active, pour chaque switch.
- **Écran** : ciblage direct de l'appareil « P1SIM Arnage » (DevicesPlugin → BitmapDisplayDevice.Settings) ; le plugin
  est prioritaire sur Devices → LCD (réécrit ses dashboards toutes les 5 s s'ils ont été changés).
- **LEDs** : gérées par SimHub (Devices → P1SIM Arnage → LEDs) ; profil « P1Sim Arnage 14 RPM » pour AutoRPM.
- Onglets / sections / boutons aux styles SimHub (`SHTabControl`, `SHSection`, `SHButtonPrimary/Secondary`, `SHToggleCheckbox`).
- Nouvelles propriétés : `P1SimArnage.LastAction.Role/.Label/.Position`.

## P1Sim Arnage plugin 0.2.0 — nouveau plugin SimHub (dossier `P1SimArnagePlugin/`)

- **Switchs FN 2 × 12 positions** : suit les deux groupes « momentary to latching » du Control mapper
  (`ControlMapperPlugin.FNKeyNNActivated`) → position 1-12 (gauche) et 13-24 (droit), avec **un label par position**.
- **Boutons − / + par switch** : pour chaque position, rôle Control mapper sur − et sur + ; génération d'un profil
  `.shcmapping` « … (P1Sim) » (combos bouton + FN de la position) à importer dans le Control mapper. Import du
  profil existant (groupes PressType 10/11 triés par n° de bouton) + bouton « Apprendre » par position.
- **Propriétés dashboard** : `P1SimArnage.Left.Label/.Position/.Fn`, `P1SimArnage.Right.Label/.Position/.Index/.Fn`,
  `P1SimArnage.LastMoved.Label/.Position/.Side`, `P1SimArnage.SlotNN.Label`.
- **Écran (VoCore)** : choix du dashboard inactif / en jeu (liste `DashTemplates`), écrits directement dans les
  réglages VoCore de SimHub (`BitmapDisplaySettings.CurrentDashboard` / `CurrentIdleDashboard` via
  `DashboardSelection.TrySet`) au démarrage (+10 s) et à chaque changement ; SimHub bascule seul entre les deux.
  « Analyser SimHub » écrit `%APPDATA%\P1SimArnagePlugin\screen_scan.txt` en cas de souci.
- **LEDs RGB** : pas encore pilotées (non vues par SimHub, protocole à identifier).
- UI en 9 langues. Exclu de `SimRaceEngineer.csproj`.
