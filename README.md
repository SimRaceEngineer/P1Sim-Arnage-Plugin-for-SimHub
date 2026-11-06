# P1Sim Arnage — plugin SimHub

Plugin SimHub (C# .NET Framework 4.8) pour le volant **P1Sim Arnage**.

## Fonctions

- **Deux switchs FN de 12 positions** (rotatif ABS = positions 1 à 12, rotatif TC = positions 13 à 24).
  - Le « momentary to latching » est intégré : cliquer sur **Apprendre** sur une position, puis tourner le switch dessus.
  - Chaque position reçoit un label et deux rôles Control mapper, un déclenché par **−** et un par **+**.
  - Les rôles sont envoyés en impulsions de 100 ms, si bien qu'aucun rôle ne peut rester bloqué enfoncé.
- **Boutons − / + par switch :** à associer avec la fenêtre de bind SimHub, par exemple aux encodeurs centraux remappés.
- **Écran du volant :** choix du dashboard *en jeu* et *inactif*, avec aperçu. Le plugin est prioritaire sur Devices → LCD.
- **LEDs RGB :** l'interface LEDs de SimHub de l'appareil est intégrée au plugin. Pour les 14 LEDs RPM, utiliser le profil « P1Sim Arnage 14 RPM » avec AutoRPM.
- **Notice illustrée** avec repères numérotés. Interface disponible en 9 langues.

## Installation

1. Télécharger `P1SimArnagePlugin.dll` depuis la [dernière release](../../releases/latest).
2. Fermer SimHub.
3. Copier `P1SimArnagePlugin.dll` dans `C:\Program Files (x86)\SimHub2\SimHub`, à côté de `SimHub.Plugins.dll`.
4. Relancer SimHub et activer **P1Sim Arnage**.

## Propriétés pour les dashboards

- `P1SimArnage.Left.Label`, `.Left.Position`
- `P1SimArnage.Right.Label`, `.Right.Position`
- `P1SimArnage.LastMoved.Label`
- `P1SimArnage.LastAction.Label`, `.Role`
- `P1SimArnage.SlotNN.Label`

## Fichiers

- Réglages : `%APPDATA%\P1SimArnagePlugin\settings.json`
- Journal : `%APPDATA%\P1SimArnagePlugin\log.txt`
