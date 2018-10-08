# Modélisation des problèmes scientifiques

## Cours 

- Module 1: Python
[Cours python](https://www.youtube.com/channel/UCWpkVtH93qQ5JpSZEwONjGA)


https://www.codingame.com/

https://perso.esiee.fr/~georgesj/esiee/igi-3008/TP5.pdf

# Mon premier voyage sur Jupyter

## Préambule

* prérequis : notions de python

## Introduction

Auparavent connus sous le nom de `notebooks python`, les notebooks
`jupyter` s'écrivent désormais en Julia, Python ou R (d'où son nom
Ju-Pyt-R). En réalité, la scission entre notebook et ipython doit
permettre l'utilisation de n'importe quel langage pour peu qu'il soit
fourni un noyau d'exécution approprié (scala, javascript, bash,
etc). Mais cela dépasse largement le périmètre de cet humble petit
plongeon, dont l'objectif est tout simplement de découvrir les
notebooks.

Qu'est-ce donc qu'un notebook ? Il s'agit un d'une application
web, qui permet de servir des bloc-notes, contenant:
* des blocs de code lisibles et **exécutables**,
* le résultat de l'exécution du code sous forme de figures, ou simple texte
* des blocs de texte enrichi (écrit en markdown) permettant de hiérarchiser l'ensemble ou disserter sur le code

## Installation de Jupyter

Plusieurs images docker sont disponibles

![](https://jupyter-docker-stacks.readthedocs.io/en/latest/_images/inherit.svg)

Nous utiliserons [jupyter/datascience-notebook](https://hub.docker.com/r/jupyter/datascience-notebook/)

C'est une version avec un ensemble de libraries pour l'analyse de données issues des communautés Julia, Python, et R.

Pour lancer jupyter

```bash
$ mkdir modelisationscientifique
$ cd modelisationscientifique
$ docker run --rm -p 8888:8888 -e JUPYTER_LAB_ENABLE=yes -v "$PWD":/home/jovyan/work jupyter/datascience-notebook
```


Vous n'avez donc plus qu'à ouvrir un navigateur à l'URL
`http://localhost:8888/?token=264e40c1f9a033172c8fb290546a538fa7260c1b1694a48e`.

La valeur du token est à récupérer dans la console dans laquelle vous avez lancé jupyter. 

## Les notebooks, pour quoi faire ?

Le contexte principal de développement de cet outil est celui de la
recherche scientifique, les notebooks sont pensés pour les chercheurs,
en particulier ceux qui font face aux problématiques d'analyse de
données.

L'intérêt principal est de permettre le partage de résultats incluant
le code pour y arriver (par exemple un scénario d'exploration de
données). Les notebooks font partie du paysage des outils de la
recherche reproductible et collaborative.

Le second cas d'application principal, pas vraiment décorrélé du
premier, est celui de l'enseignement. Comme illustré dans l'exemple
précédent, le notebook se prête bien à la démonstration. 
Un certain nombre d'outils ont même été développés en complément des
notebooks dans ce contexte:
* _jupyterhub_: qui permet de servir des notebooks à un
  groupe d'utilisateur simultanément
* _nbgrader_: qui permet de gérer et évaluer les contenus de notebooks assignés

## Comment ça marche ?

L'exécution de code (ici python pour l'exemple) depuis un notebook
jupyter repose sur le noyau ipython, qui vit dans un processus
séparé. Le notebook communique avec le noyau via l'envoi de message
ZeroMQ au format Json.

Le notebook, servi sur l'application web, peut être sauvé dans un
document statique (.ipynb), qui contiendra l'ensemble du code, du
texte et des résultats (même graphiques). Ces fichiers peuvent être
sauvés, échangés ou même convertis par exemple au format HTML, via
l'outil `nbconvert`. Encore plus fort, si votre fichier .ipynb est
accessible au web (par exemple sauvé dans un repository git public),
l'outil `nbviewer` (http://nbviewer.jupyter.org/) se charge d'en
fournir un rendu HTML sur une page que vous pourrez alors partager
avec vos collaborateurs sans qu'ils aient besoin d'installer Jupyter
eux-mêmes.

## Allez, on se lance !

### Ecrire un notebook

C'est le moment d'écrire votre propre notebook. Le sujet est libre,
mais nous vous suggérons d'essayer toutes les techniques:

* exécution de code dans des blocs séparés
* par du texte enrichi avec titre, texte en gras, italique,
* et des équations (indice, utiliser le symbole $)
* des tables (avec | et -)
* des liens vers des fichiers locaux et des images (utiliser image.png)

### Configurer jupyter

La configuration de jupyter peut-être modifée, via l'édition du fichier
~/.jupyter/jupyter_notebook_config.py

Pour générer un tel fichier, tapez la commande `jupyter notebook
--generate-config`, puis survolez l'ensemble des options de ce fichier. 

Comme nous avons lancé jupyter depuis le container docker, connectez-vous
à ce dernier par la commande `docker exec -i -t dockerid /bin/bash`
après avoir récupérer le dockerid via `docker ps`

Des extensions vous permettent de compléter les fonctionnalités de
base de jupyter. Pour les survoler et les activer, rendez-vous sur la
page `http://localhost:8888/nbextensions` (pour compléter votre
installation locale, utiliser la commande `conda install -c
conda-forge jupyter_contrib_nbextensions`)

## Sources

 * [Jupyter documentation](http://jupyter.readthedocs.io/en/latest/index.html)
 * [Jupyter examples](https://jupyter-notebook.readthedocs.io/en/latest/examples/Notebook/examples_index.html)

## Exercice à rendre pour le module python:

### Exercice 1: Base de python

Récupérer le [fichier suivant](https://github.com/barais/modelisation_des_problemes_scientifiques/blob/master/TP1-introPython.ipynb) et rééxecuter l'ensemble des exemples de code fournis. Vérifier que vous les comprenez tous. 

### Exercice 2: Modélisation objet

Récupérer le [fichier suivant](https://github.com/barais/modelisation_des_problemes_scientifiques/blob/master/TP2-PythonProg.ipynb) et rééxecuter l'ensemble des exemples de code fournis. Vérifier que vous les comprenez tous.

### Exercice 3

Lors du premier tome de Harry Potter les trois héros doivent résoudre une énigme - qui ne nécessite aucune magie - afin d’accéder à la salle où est cachée la pierre philosophale. Ce problème, dont l’auteur serait le professeur Rogue (Professor Snape pour les anglophones), consiste à trouver deux potions parmi les sept qui se trouvent devant eux : celles permettent d’avancer et de reculer. Ils sont aidés de quelques indices :

- Il y a trois fioles de poison, deux fioles de vin d’ortie, une fiole permettant d’avancer et une fiole permettant de reculer.
- Immédiatement à gauche de chacune des deux fioles de vin se trouve une fiole de poison.
- Les fioles 1 et 7 ont des contenus différents~; ni l’une ni l’autre n’est la fiole qui permet d’avancer.
- Ni la fiole la plus grande (fiole 6) ni la plus petite (fiole 3) ne contient du poison.
- Les contenus des fioles 2 et 6 sont identiques.

## Exercice 3
