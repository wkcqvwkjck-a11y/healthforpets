# Site web Health for Pets

Site statique (HTML/CSS, aucune dépendance) destiné à **GitHub Pages** avec un **nom de
domaine OVH**.

Il contient les pages exigées par l'App Store :

| Page | FR | EN |
|---|---|---|
| Accueil | `index.html` | `en/index.html` |
| Politique de confidentialité | `confidentialite.html` | `en/privacy.html` |
| Conditions d'utilisation | `conditions.html` | `en/terms.html` |
| Support | `support.html` | `en/support.html` |

## 1. Mise en ligne sur GitHub Pages

### a) Créer le dépôt et publier

```bash
# Depuis le dossier website/
cd website
git init
git add -A
git commit -m "Site Health for Pets"
git branch -M main
git remote add origin https://github.com/wkcqvwkjck-a11y/healthforpets.git
git push -u origin main
```

### b) Activer GitHub Pages

1. Dépôt → **Settings** → **Pages**
2. *Source* : **Deploy from a branch**
3. *Branch* : `main` · dossier `/ (root)` → **Save**
4. Le site est visible sur `https://wkcqvwkjck-a11y.github.io/healthforpets/`

### c) Domaine personnalisé

1. Toujours dans **Settings → Pages**, champ *Custom domain* : `healthforpets.app` → **Save**
   (GitHub créera alors le fichier `CNAME` dans le dépôt).
2. Configurer les DNS chez OVH (section 2).
3. Une fois les DNS propagés, cocher **Enforce HTTPS** (certificat Let's Encrypt gratuit).

> ⚠️ Le fichier `CNAME` est actuellement **exclu du dépôt** (`.gitignore`) : il ne faut
> l'ajouter qu'une fois le domaine acheté, sinon l'aperçu `github.io` redirigerait vers
> un domaine inexistant.

## 2. DNS chez OVH

Espace client OVH → **Web Cloud** → **Noms de domaine** → `healthforpets.app` → onglet
**Zone DNS**. Supprimer les entrées « Site web » par défaut, puis ajouter :

| Type | Sous-domaine | Cible |
|---|---|---|
| A | *(vide)* | `185.199.108.153` |
| A | *(vide)* | `185.199.109.153` |
| A | *(vide)* | `185.199.110.153` |
| A | *(vide)* | `185.199.111.153` |
| AAAA | *(vide)* | `2606:50c0:8000::153` |
| AAAA | *(vide)* | `2606:50c0:8001::153` |
| AAAA | *(vide)* | `2606:50c0:8002::153` |
| AAAA | *(vide)* | `2606:50c0:8003::153` |
| CNAME | `www` | `<TON_COMPTE>.github.io.` |

TTL : 3600 s (valeur par défaut). Propagation : de quelques minutes à 24 h.

## 3. Adresse e-mail `support@healthforpets.app`

Deux options :

- **Redirection OVH** (gratuite selon l'offre) : Espace client → E-mails → Redirections.
- **ImprovMX** (gratuit) : créer une redirection `support@` vers ton adresse personnelle,
  puis ajouter l'enregistrement MX indiqué.

## 4. Mettre à jour l'application

Une fois le site en ligne, vérifier les URLs dans `src/constants/legal.ts` :

```ts
export const PRIVACY_POLICY_URL = 'https://healthforpets.app/confidentialite.html';
export const TERMS_URL = 'https://healthforpets.app/conditions.html';
export const SUPPORT_URL = 'https://healthforpets.app/support.html';
export const SUPPORT_EMAIL = 'support@healthforpets.app';
```

## 5. Modifier le site

Les pages sont du HTML simple : modifier le texte directement, puis :

```bash
git add .
git commit -m "Mise à jour du site"
git push
```

GitHub Pages republie automatiquement en ~1 minute.
