# Convertisseur de Sauvegarde Stormshield en JSON / Stormshield Backup to JSON Converter

[Version Française](#version-française-fr) | [English Version](#english-version-en)

---

## Version Française (FR)

Cette application écrite en Python (GUI construite avec tkinter, intégré à Python) permet de charger et convertir une archive de firewall Stormshield (`*.na`) en un fichier JSON unique et structuré.

### Fonctionnalités

- **Extraction & Décryptage** : Appelle l'utilitaire `decbackup.exe` pour décrypter l'archive (prend en charge les mots de passe si l'archive est chiffrée).
- **Structure JSON** : Organise les dossiers et fichiers sous forme de dictionnaire imbriqué (les clés correspondent aux noms réels des dossiers/fichiers).
- **Formatage des fichiers** : 
  - Les fichiers de type configuration (ex. `config`) sont analysés comme des fichiers INI (les sections comme `[ProxyHTTP]` deviennent des sous-clés).
  - Les commentaires (commençant par `#`) sont supprimés et les lignes vides épurées.
  - Les fichiers textes simples sont stockés sous forme de liste de lignes.
  - Les fichiers binaires ou chiffrés non lisibles sont marqués `"Non déchiffrable"` (ou `"Undecipherable"`).
  - Les fichiers binaires globaux sont convertis en Base64.
- **Interface** :
  - Thèmes Clair et Sombre.
  - Multilingue (Français / Anglais) dynamique sans redémarrage.
  - Arbre de navigation interactif avec barre de recherche filtrante en temps réel.
  - Aperçu hybride (visualisation de la structure arborescente à gauche, contenu et métadonnées du fichier sélectionné à droite, avec un onglet d'aperçu du JSON brut final).

### Prérequis

- **decbackup.exe** : Placé à la racine du projet ou configuré via l'onglet Paramètres.
- **Aucune dépendance externe** à installer.

### Lancement

Double clic sur l'application `naBackupToJson.exe`

### Comparaison de sauvegardes (Diff)

L'application permet de comparer deux sauvegardes (deux fichiers `.json` déjà générés, deux archives `.na`, ou un mélange des deux) et de générer un fichier JSON ne contenant que les différences.

- **Dans l'IHM** : cliquez sur le bouton **"Comparer (Diff)"** en haut de la fenêtre, sélectionnez les fichiers "avant" et "après" (avec mot de passe si nécessaire pour un `.na`), cliquez sur "Comparer", puis "Enregistrer la différence".
- **En ligne de commande** :
  ```powershell
  python main.py -db <fichier_avant.json|.na> -da <fichier_apres.json|.na> [-do <diff_sortie.json>] [-pwb <mot_de_passe_avant>] [-pwa <mot_de_passe_après>]
  ```
- Le fichier de différence généré contient, pour chaque élément modifié, ajouté ou supprimé, un marqueur `__diff__` (`added`, `removed` ou `modified`) ainsi que les valeurs concernées ; les éléments identiques entre les deux fichiers ne sont pas repris.

---

## English Version (EN)

This Python application (GUI built with tkinter, bundled with Python) allows you to load and convert a Stormshield firewall backup archive (`*.na`) into a single structured JSON file.

### Features

- **Extraction & Decryption**: Runs `decbackup.exe` to decrypt the archive (handles encryption passwords).
- **JSON Structure**: Organizes folders and files as a nested dictionary (keys are folder/file names).
- **Configuration Parsing**:
  - Configuration-style text files (e.g. `config`) are parsed as INI files (sections like `[ProxyHTTP]` become sub-keys).
  - Comments (starting with `#`) are stripped and empty lines are removed.
  - Regular text files are parsed as a list of lines.
  - Undecipherable/encrypted values are marked `"Undecipherable"` (or `"Non déchiffrable"`).
  - Global binary files are Base64-encoded.
- **Interface**:
  - Light and Dark themes.
  - Dynamic multilingual support (French / English) without restarting.
  - Interactive file tree view with a real-time filter search bar.
  - Hybrid layout (file tree structure on the left, selected file details/content on the right, alongside a raw JSON output preview).

### Prerequisites

- **decbackup.exe**: Placed at the project root or configured in the Settings panel.
- **No external dependencies** to install.

### Run

Double-click on the `naBackupToJson.exe` application

### Backup Comparison (Diff)

The application can compare two backups (two already-generated `.json` files, two `.na` archives, or a mix of both) and generate a JSON file containing only the differences.

- **In the GUI**: click the **"Compare (Diff)"** button at the top of the window, pick the "before" and "after" files (with a password if needed for a `.na` archive), click "Compare", then "Save difference".
- **From the command line**:
  ```powershell
  python main.py -db <before_file.json|.na> -da <after_file.json|.na> [-do <output_diff.json>] [-pwb <before_password>] [-pwa <after_password>]
  ```
- The generated diff file marks each added, removed, or modified element with a `__diff__` key (`added`, `removed`, or `modified`) along with the relevant values; items identical between both files are omitted.
