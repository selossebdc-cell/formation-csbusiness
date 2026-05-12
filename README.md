# Site statique — formation.csbusiness.fr

Mini-site **GitHub Pages** pour partager des HTML (formations, supports interactifs). Public, sans mot de passe.

## Ce qui est dans ce dossier

| Fichier / dossier | Rôle |
|-------------------|------|
| `CNAME` | Indique à GitHub Pages le domaine custom **`formation.csbusiness.fr`** |
| `.nojekyll` | Désactive Jekyll (évite les surprises sur fichiers qui commencent par `_`) |
| `index.html` | Page d’accueil : liste les liens vers tes documents |
| `documents/` | Dépose ici tes fichiers `.html` (et assets associés si besoin) |
| `assets/` | Logo et futures images communes |

## Mise en ligne (une fois)

### 1. Créer un dépôt GitHub dédié

Ce dossier est prévu pour être **la racine** d’un repo séparé (ex. `formation-csbusiness`), pas comme sous-dossier d’un autre site.

```bash
cd formation-csbusiness
git init
git add .
git commit -m "Initial GitHub Pages — formation.csbusiness.fr"
```

Crée un repo vide sur GitHub (sans README), puis :

```bash
git remote add origin git@github.com:TON_ORG_OU_USER/formation-csbusiness.git
git branch -M main
git push -u origin main
```

(Remplace `TON_ORG_OU_USER` par ton compte ou organisation GitHub.)

### 2. Activer GitHub Pages

Sur GitHub : **Settings → Pages**

- **Source** : Deploy from branch **main**
- **Folder** : `/ (root)`
- **Save**

### 3. Domaine personnalisé

Toujours dans **Settings → Pages** :

- **Custom domain** : `formation.csbusiness.fr`
- Coche **Enforce HTTPS** une fois que le certificat est émis (souvent quelques minutes après le DNS).

Le fichier `CNAME` à la racine du repo doit contenir une seule ligne : `formation.csbusiness.fr`.

### 4. DNS chez ton hébergeur de domaine (csbusiness.fr)

Ajoute un enregistrement **CNAME** :

| Type  | Nom / Host | Cible (points to) |
|-------|------------|-------------------|
| CNAME | `formation` | `TON_USER_OU_ORG.github.io` |

- Si ton compte GitHub est une **organisation** `selossebdc-cell`, la cible est typiquement **`selossebdc-cell.github.io`** (à confirmer dans ton URL GitHub).
- Ne mets **pas** `https://` dans la cible.
- TTL : automatique ou 300 s.

Propagation : souvent 5–30 minutes, parfois jusqu’à 48 h.

### 5. Mettre à jour la page d’accueil

Après chaque ajout de fichier dans `documents/`, édite les liens dans `index.html`, puis :

```bash
git add .
git commit -m "Ajout documents formation FCE"
git push
```

Les participants utilisent : **https://formation.csbusiness.fr**

## Déjà fait dans ce workspace

- Dépôt GitHub : **https://github.com/selossebdc-cell/formation-csbusiness**
- Remote Git local (depuis la racine du repo `csbusiness-local`) : `formation` → ce dépôt
- Pages activée depuis la branche **`main`** (racine)

Pour publier une mise à jour **sans** quitter le mono-repo `csbusiness-local`, après commit sur `main` :

```bash
cd /chemin/vers/csbusiness-local
git subtree push --prefix formation-csbusiness formation main
```

(La première fois peut prendre un peu plus de temps ; ensuite Git optimise.)

## Limite à connaître

Un sous-domaine **`*.csbusiness.fr`** ne peut pointer vers **qu’un seul** dépôt GitHub Pages à la fois pour ce hostname. Si tu réutilises `formation.csbusiness.fr` pour une autre stack plus tard, il faudra changer soit le DNS soit le repo configuré dans GitHub.
