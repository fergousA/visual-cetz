# Publier Visual CeTZ sur GitHub

Ce dossier est **déjà un dépôt Git** avec un premier commit contenant les
23 fichiers (sources, Makefile, README, LICENSE et le PDF).

Il ne s'agit pas d'un paquet Typst : Universe n'héberge que du code importable.
Un manuel se diffuse par un dépôt Git et une *release*.

---

## 1. Votre identité Git

À faire une fois sur votre machine :

```sh
git config --global user.name  "Votre Nom"
git config --global user.email "vous@exemple.org"
```


```
cd /chemin/vers/visual-cetz-0.5.2     # là où vous avez dézippé
git init -b main
git add -A
git commit -m "Visual CeTZ 0.5.2"
```

Le commit initial a été créé sous un nom générique. Réattribuez-le :

```sh
cd ~/cetz-guide
git commit --amend --reset-author --no-edit
```

Vérifiez : `git log -1 --format='%an <%ae>'`.

## 2. Créer le dépôt sur GitHub

Créez un dépôt **vide** — sans README, sans licence, sans `.gitignore` — pour
éviter un conflit au premier push. Nommez-le par exemple `visual-cetz`.

Puis reliez-le et poussez :

```sh
cd ~/cetz-guide
git remote add origin git@github.com:VOUS/visual-cetz.git
git push -u origin main
```

En HTTPS plutôt qu'en SSH :

```sh
git remote add origin https://github.com/VOUS/visual-cetz.git
```

Le `README.md` s'affichera automatiquement sur la page d'accueil du dépôt.

## 3. Publier le PDF en release

Une release rend le PDF téléchargeable en un clic, sans passer par l'historique.

```sh
cd ~/cetz-guide
git tag -a v0.5.2 -m "Visual CeTZ pour CeTZ 0.5.2"
git push origin v0.5.2
```

Puis sur GitHub : **Releases → Draft a new release → tag `v0.5.2`**, et joignez
`Visual-CeTZ-0.5.2.pdf`.

Avec [`gh`](https://cli.github.com/), tout en une commande :

```sh
gh release create v0.5.2 Visual-CeTZ-0.5.2.pdf \
   --title "Visual CeTZ 0.5.2" \
   --notes "Guide visuel de CeTZ 0.5.2 — 51 pages, 27 chapitres, 200 exemples."
```

### Numérotation des versions

Le tag suit la version de CeTZ documentée. Pour une correction du guide sans
changement de CeTZ, ajoutez un suffixe : `v0.5.2-2`, `v0.5.2-3`, etc.

---

## Faut-il versionner le PDF ?

Il l'est actuellement, et c'est un choix délibéré : le lecteur qui clone obtient
le manuel sans rien compiler. Coût : 1,8 Mo par version enregistrée.

Si vous publiez souvent, préférez la release seule et retirez le PDF du suivi :

```sh
cd ~/cetz-guide
git rm --cached Visual-CeTZ-0.5.2.pdf
echo "Visual-CeTZ-0.5.2.pdf" >> .gitignore
git commit -m "Ne plus versionner le PDF, disponible en release"
```

Pensez alors à ajouter un lien de téléchargement en tête du README, car le
`[Visual-CeTZ-0.5.2.pdf](Visual-CeTZ-0.5.2.pdf)` actuel serait cassé :

```markdown
**→ [Télécharger le PDF](https://github.com/VOUS/visual-cetz/releases/latest)**
```

---

## Vérifié

Un clone frais de ce dépôt compile sans rien d'autre que Typst : les paquets
`cetz`, `cetz-plot` et `cetz-venn` sont téléchargés automatiquement au premier
lancement. Testé sur une copie propre — 51 pages produites.

## Diffuser plus largement

- **Le forum Typst** : [forum.typst.app](https://forum.typst.app/), catégorie
  *Show and Tell*.
- **Awesome Typst** : [github.com/qjcg/awesome-typst](https://github.com/qjcg/awesome-typst),
  par pull request.
- **GitHub Pages** : `Settings → Pages` sert le PDF à une URL stable, pratique
  pour un lien permanent dans une bibliographie.
- **Le dépôt CeTZ** : une mention dans une *discussion* peut intéresser ses
  auteurs et ses utilisateurs.
