Script de démarrage automatique pour reconstruire l'environnement ComfyUI de
production d'Inès (modèles, LoRA, workflow) sur une nouvelle instance Vast.ai,
sans manipulation manuelle en terminal.

## Contenu

- `ines_provisioning_script.sh` — script exécuté automatiquement au boot de
  l'instance Vast.ai (variable d'environnement `PROVISIONING_SCRIPT`)

## Mise en place (une seule fois)

1. **Créer ce repo sur GitHub** (public ou privé, peu importe) :
   - github.com → bouton vert "New" → nom du repo (ex. `ines-vast-provisioning`) → Create
   - Cliquer "Add file" → "Upload files" → glisser `ines_provisioning_script.sh` → Commit

2. **Récupérer l'URL "raw"** du script :
   - Ouvrir le fichier dans GitHub → bouton "Raw" → copier l'URL
   - Elle ressemble à : `https://raw.githubusercontent.com/<user>/<repo>/main/ines_provisioning_script.sh`

3. **Configurer le template Vast.ai** (une seule fois) :
   - Dans le template ComfyUI, section "Environment Variables", ajouter :
     - `PROVISIONING_SCRIPT` = l'URL raw copiée à l'étape 2
     - `HF_TOKEN` = ton token HuggingFace
     - `CIVITAI_TOKEN` = ton token API Civitai (civitai.com → Settings → API Keys)
   - Sauvegarder le template

4. **Partager le fichier LoRA v6 sur Drive** en "Anyone with the link" (sinon
   le script ne peut pas le télécharger).

## Utilisation (à chaque location)

Rien à faire — louer une instance à partir du template configuré déclenche
le script automatiquement. Premier boot : ~40-60 min. Boots suivants (même
instance, stoppée pas détruite) : quasi instantané.

## Point non garanti

Le VAE réel de production (`Wan2_1_VAE_fp32.safetensors`) n'a pas de source
publique identifiée avec certitude — voir le commentaire dans le script.
Si le premier rendu diverge de la référence (mâchoire, iris ambre/doré),
c'est le premier point à vérifier.
