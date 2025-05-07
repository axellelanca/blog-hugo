---
date: 2025-05-07T19:53:00+02:00
draft: false
title: 'La stack de mon blog : Hugo, Papermod et autres outils sympas'
weight: 2
Description: 'Découvrez comment j’ai construit un blog statique performant avec Hugo, le thème PaperMod, GitHub Pages, GoatCounter, Utterances pour les commentaires et un déploiement automatisé avec GitHub Actions. Stack simple, rapide, open-source et sans prise de tête.'
tags: []
author: ''
cover:
image: "<image path/url>" # image path/url
alt: "<alt text>" # alt text
caption: "<text>" # display caption under cover
relative: false # when using page bundles set this to true
hidden: true # only hide on current single page
editPost:
URL: "https://github.com/axellelanca/blog-hugo/content/"
Text: "Suggest Changes" # edit text
appendFilePath: true # to append file path to Edit link
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowToc: false
---

# La stack de mon blog : Hugo, Papermod et autres outils sympas

Quand on est dev (et donc flemmard) on veut un site qui **se déploie tout seul**, qui soit **rapide** et qui ne demande **pas trop de maintenance**, non ?
Alors aujourd'hui, je vous emmène faire un tour d'horizon de la stack que j'ai choisi pour mon blog : Pas de magie noire, juste de la simplicité !

## 🧱 Hugo + Papermod

J'ai choisi **[Hugo](https://gohugo.io/)** comme générateur de site statique. Pourquoi ?

### La vitesse 

L'un des atouts majeurs d'Hugo est sa vitesse de construction. Contrairement aux CMS dynamiques qui génèrent chaque page à la volée à chaque requête d'un visiteur, Hugo pré-compile l'ensemble du site en fichiers HTML statiques lors du build. Le résultat ? Des pages qui se chargent quasi instantanément.

### La simplicité
Hugo est conçu pour être simple à utiliser. Il n'y a pas de base de données à configurer, pas de serveur à gérer. Vous écrivez du contenu en Markdown, et Hugo s'occupe du reste. C'est idéal pour les développeurs qui veulent se concentrer sur le contenu plutôt que sur la configuration.

```markdown
    # Exemple de la structure d'un projet Hugo
    .
    ├── archetypes/
    ├── assets/
    ├── config.toml
    ├── content/
    │   └── posts/
    │       └── mon-article.md
    ├── data/
    ├── i18n/
    ├── layouts/
    ├── public/
    ├── resources/
    ├── static/
    └── themes/
        └── PaperMod/
```

Et il y a les thèmes ! J'ai jeté mon dévolu sur **[PaperMod](https://github.com/adityatelange/hugo-PaperMod)**. Un thème épuré, responsive, et configurable sans douleur.

### En sommes 

* C’est **ultra rapide** (on parle de millisecondes pour générer un site complet).

* C’est **simple à installer et à utiliser** : une commande, et c’est parti.

* C’est **open-source** et activement maintenu.

* Il y a une **grande communauté** et plein de thèmes bien fichus.

* J’aime **écrire en Markdown**, et Hugo s’y prête parfaitement.

## 🗂 Une organisation propre grâce aux Branch Bundles

Pour organiser mes articles, j’utilise les Branch Bundles de Hugo. Contrairement aux Leaf Bundles qui contiennent une seule page, les Branch Bundles permettent de regrouper plusieurs contenus dans un même dossier.
```markdown
    content/
    └── posts/
        └── mon-article/
            ├── index.md
            ├── image1.jpg
            └── image2.png
```

Cela permet :

* de lier facilement des ressources (images, vidéos, etc.) à un article sans jongler avec des chemins compliqués,

* d’éviter le bazar dans `static/`,

* et de mieux visualiser la structure de chaque post.

## 💬 Les commentaires avec Utterances

Pour les commentaires, j’ai intégré Utterances. L’idée est simple : chaque post peut avoir un fil de discussion associé dans les issues de votre repo GitHub. Pas besoin de base de données, pas de spam à modérer (merci GitHub), et ça respecte plutôt bien la vie privée.

Et hyper simple (vraiment le mot d'ordre ici) à mettre en place : il suffit d'ajouter un script dans le `head` de votre site et de configurer quelques options, et le tour est joué.

```html
    <script src="https://utteranc.es/client.js"
            repo="mon-utilisateur/mon-blog"
            issue-term="pathname"
            theme="github-light"
            crossorigin="anonymous"
            async>
    </script>
```

### Les autres alternatives

| Outil         | Avantages                              | Inconvénients                                  |
|---------------|----------------------------------------|------------------------------------------------|
| **Utterances**| Simple, GitHub natif, gratuit          | Nécessite un compte GitHub pour commenter      |
| **Disqus**    | Populaire, riche en fonctionnalités    | Intrusif, collecte de données, traqueur        |
| **Commento**  | Respectueux de la vie privée, léger    | Moins répandu, auto-hébergement recommandé     |
| **Giscus**    | Moderne, basé sur GitHub Discussions   | GitHub obligatoire, moins connu que Disqus     |

## ✍️ Proposer des corrections (et être cité !)

Comme je ne suis pas à l’abri d’une coquille ou d’un raccourci malheureux, j’ai activé une fonctionnalité GitHub : "suggest changes". Tu peux ainsi proposer directement une modification sur un article, et si elle est pertinente (et validée), ton nom sera cité comme contributeur.
J'avais envie de créer des articles un peu collaboratifs, et je trouve que c'est une bonne manière de le faire !

## 📊 Statistiques sans flicage : GoatCounter

Google Analytics ? Non merci. J’ai opté pour GoatCounter, un outil de statistiques simple, open-source, respectueux de la vie privée.

Pourquoi ce choix ?

* Pas de cookies.

* Interface minimaliste mais suffisante.

* Une simple ligne de JS à intégrer :
    ```html
        <script data-goatcounter="https://moncompte.goatcounter.com/count"
                async src="//gc.zgo.at/count.js"></script>
    ```

C’est tout. J’ai des chiffres, sans vendre mon âme.

## 🌐 Hébergement sur GitHub Pages + sous-domaine personnalisé

Le site est hébergé sur GitHub Pages, ce qui signifie :

* Aucun serveur à gérer.

* Zéro facture d’hébergement.

* Déploiement en quelques secondes.

Et pour la touche finale, j’ai configuré un sous-domaine personnalisé : 

👉🏼`blog.axellelanca.com`

> 📌 **Astuce DNS**  
> Côté DNS, il suffit de pointer un enregistrement **CNAME** vers `nomdutilisateur.github.io`,  
> et de s’assurer que le fichier `CNAME` est bien présent à la racine du dossier `public/`  
> au moment du déploiement.  
> Sinon, ça fait quelques problèmes !

## 🛠 Déploiement continu avec GitHub Actions

À chaque push, mon site se build de nouveau et se redéploie automatiquement sur GitHub Pages. Pas besoin de cliquer nulle part : c'est... (devinez)... **simple**, c'est pratique, c'est magique.

Voici le contenu de mon fichier yaml pour les curieux : 

```yaml
name: Déployer le site Hugo sur GitHub Pages

on:
  push:
    branches: [ main ]

permissions:
  contents: write

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Vérifier le code
        uses: actions/checkout@v4

      - name: Vérifier les sous-modules
        run: git submodule update --init --recursive

      - name: Installer Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.145.0'
          extended: true

      - name: Construire le site Hugo
        run: hugo --minify

      - name: Ajouter le fichier CNAME
        run: echo "blog.axellelanca.com" > public/CNAME

      - name: Déployer sur GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: gh-pages
          commit_message: "Déploiement automatique par GitHub Actions"
```

## 🤔 Et pourquoi pas autre chose ?

Tu te demandes peut-être : “Mais pourquoi pas WordPress ? Ou Medium ? Ou écrire sur LinkedIn comme tout le monde ?”

Simplement parce que :

* Je veux garder le contrôle de mes données.

* J’aime le minimalisme (pas de plugin qui fait planter le site dès que je touche un bouton, je pose ça là comme ça).

* Je peux personnaliser comme je veux sans dépendre d’un écosystème.

* Et surtout… j’aime bricoler et que Hugo c'est quand même très sympa à utiliser !

## Conclusion

Eh voilà, mon petit blog tour est terminé, pas de grand tuto, juste un petit partage de ma stack et des choix que j'ai fait.
Ça me permet d’écrire, expérimenter, publier tranquillement ! 