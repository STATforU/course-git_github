# Notes 

Ce document a pour objectif de recueillir des notes afin de préparer la formation sur 4 séances d'une heure sur les bases de Git et GitHub dans le cadre d'analyse de données associées à un projet. Ce projet peut être un mémoire, un article scientifique, une expérience particulière...

## Introduction théorique à Git et GitHub

### Git 

Git est un gestionnaire de version, c'est-à-dire un logiciel qui permet de garder un historique de toutes les modifications d'un fichier (ou de plusieurs fichiers au cours du temps) dans un dépôt (un dossier spécifique sur l'ordinateur).

Il permet de revenir sur une version précédente, de suivre l'évolution d'un projet et de collaborer sur un même document.

Git s'installe facilement sur macOS, Windows ou Linux <https://git-scm.com/downloads>

### [GitHub](https://github.com/)

GitHub est un réseau social lié à Git. Il permet d'héberger le dépôt en ligne. Un dépôt en ligne est un dépôt distant par opposition au dépôt local. Il existe plusieurs plateformes pour héberger les dépôts comme GitLab, Bitbucket ou encore GitHub. 

Le dépôt est très utile pour la collaboration sur des projets et avoir une sauvegarde de son dépôt en ligne. 

La création d'un compte sur GitHub est simple et gratuite.L'élément clé est de bien choisir son nom d'utilisateur. Cette plateforme peut vous servir de porte-folio valorisable dans un C.V. Il est donc préférable d'éviter les noms comiques.

Voici par exemple mon compte sur GitHub <https://github.com/GuyliannEngels>


Fonction utile pour configurer son identité :

```
# Que sait Git de moi ? 
git config --list
# Ajout de mon nom d'utilisateur et de mon email.
git config --global user.name "GuyliannEgnels"
git config --global user.email guyliann.engels@umons.ac.be
```

## Initialiser un projet

Pour débuter un nouveau projet que l'on souhaite organiser sous la forme d'un dépôt, on peut décider de le débuter sur GitHub puis d'en faire une copie locale ou bien on va initier le dépôt localement que l'on ajoutera sur GitHub par la suite.

### Créer un dépôt distant

- Sélectionner `Create a new repository`
- Nommer le dépôt (= repository)
- Décrire brièvement le but du dépôt
- Décider si le dépôt doit être public ou privé
- Initialiser le dépôt (uniquement si le dépôt local n'a pas encore été créé)
  - Ajouter un README
  - Ajouter un un fichier .gitignore
  - Ajouter une licence

L'étape suivante consiste dans le clone du dépôt distant localement. Le dépôt cloné se nommera dépôt local.

### Initialiser un dépôt local

On crée un dossier localement qui va servir de dépôt. On utilise ensuite le terminal pour transformer ce dossier en dépôt avec les instructions ci-dessous.

```
# Sélectionner le dossier d'intérêt
cd ~/Desktop/monprojet
git init
```

On doit créer un dépôt vide sur GitHub comme présenté précédemment puis on lie le dépôt local au dépôt distant vide. 

Mon petit conseil est d'utiliser la première stratégie qui consiste dans la création du dépôt distant puis de la cloner.

```
git remote add origin https://github.com/GuyliannEngels/SFU-monpremierprojet.git
git branch -M main
```
On va pousser notre version locale sur la version en ligne.

```
git push -i origin main
```

## Progresser pas à pas dans son projet

Lorsqu'on édite un fichier qui fait partie de notre dépôt, on peut décider de figer les modifications réalisées en réalisant un commit que l'on peut voir comme un état de sauvegarde du projet contenant une série de fichiers modifiés par rapport à la version précédente. 

Pour réaliser ce commit nous devons débuter par sélectionner les fichiers qui ont été modifiés. On parlera d'indexer un fichier.

```
git add monfichier.md
```

Ensuite, on va réaliser un commit. Un commit est toujours associé à un message explicite sur ce que contient ce commit et pourquoi. 

```
git commit -m "message explicite sur la nouvelle version"
```

Les mauvais messages associés à un commit : version1, commit, dernier commit,...

Pour envoyer les modifications réalisées dans le dépôt local vers le dépôt distant, on réalise un push.

```
git push origin main
```

Dans cette situation le dépôt local sert uniquement à être un endroit de stockage du projet. 

### Le bon fichier et le mauvais fichier

Tous les formats de fichiers ne sont pas adéquats à être versionné. Les outils de gestion de version sont principalement et anciennement utilisés par les développeurs. 

- écriture de texte : doc, docx -> md
- tableau de données : xlsx, xls -> csv
- code : ce qui permet de générer un fichier avec la suite d'instruction réalisée : R


## Le dépôt distant 

Les fonctions utiles 

```
git clone
git push
git pull
git fetch
```

Dans la section précédente, nous avons vu que le dépôt distant servait de point de stockage. On utilise git push pour pousser nos dernières modifications sur le réseau. Il est possible de faire bien plus avec le dépôt distant. 

## La collaboration sur un projet

Il de plus en plus improbable de travailler seul dans son coin et de ne pas collaborer. La collaboration est même un élément central dans la recherche. 

Il est tout à fait possible de travailler à plusieurs sur un dépôt distant. Chaque collaborateur va réaliser un clone puis va travailler de la même manière que pour un projet individuel. 

Si deux collaborateurs travaillent sur la même partie d'un fichier, comment définir quelle version est la bonne ? Git ne prend pas la décision pour vous. Il va vous générer un conflit que vous allez devoir résoudre. L'un des deux collaborateurs va devoir choisir la partie la plus à jour d'un fichier.

```
<<<<<<< HEAD 
partie 1
=====
partie 2
>>>>>
```

Une fois le choix réalisé. Il faut indexer puis réaliser un commit du fichier problématique.

## Étudie de l'historique du dépôt

Les fonctions utiles 

```
git reflog
git log 
git blame
```

git log va permettre de voir les commits réalisé dans l'ordre inverse des réalisations (du plus récent au plus ancien)

git reflog affiche toutes les actions réalisés. 

git blame permet d'examiner le contenu d'un fichier ligne par ligne

## Les fonctions utiles

### Fichier qui devait être indexé

J'ai oublié d'indexer un fichier. Il n'est pas nécessaire de refaire un commit. Il est possible de l'ajouter au dernier commit.

```
git add FichierOublie.txt
git commit --amend --no-edit
```

### Message du commit erroné

```
git commit --amend -m "Votre nouveau message de commit"
```

### Fichier qui ne devait pas être indexé 

J'ai réalisé une erreur, j'ai ajouté un fichier à mon commit que je ne voulais pas. Je n'ai pas encore réalisé de push. Mon erreur est présente uniquement localement.

Il faut trouver le commit en question avec la fonction git log

```
git log 
```

Il faut employer la fonction git reset qui permet d'annuler ces changements. Il y a trois versions à cette instruction.

git reset --soft
git reset --mixed
git reset --hard


La version hard permet de revenir à l'état du commit désiré. C'est puissant, mais destructif. Tout ce qui a été fait après le commit sélectionné est perdu.


La version mixed permet de revenir juste après le commit souhaité, sans supprimer vos modifications. Il faudra donc à nouveau les indexer puis les committer.

La version soft permet de revenir en arrière et de voir ce que l'on a fait. Elle ne supprime pas de fichier, pas de commit,... Cette version me semble peu utile.


