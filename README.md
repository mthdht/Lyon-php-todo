# Création d'une Todo liste

**Prérequis**: Base PHP, les objets, le modèle MVC, la validation

**Objectif**: Savoir utiliser toutes les connaissances jusque là accumulé (voir prérequis)

Dans cet exercice, nous allons créer une app qui permettra aux utilisateur de s'inscrire et de créer des todo listes.

## Etape 0 - Le repot Git

- `git init`
- `git remote add origin https://github.com/mthdht/Lyon-php-todo.git `
- `git pull origin master`


## Etape 1 - La structure de fichiers

Notre application aura la stucture suivante

```
TodoList
    public/
        index.php
        style.css
    src/
        Controllers/
            UserController.php
            TodoController.php
        Models/
            User.php
            Todo.php
            Task.php
            UserManager.php
            TodoManager.php
            TaskManager.php
        Views/
            Auth/
                login.php
                register.php
            Todo/
                index.php
                show.php
                create.php
        Router.php
```

## Etape 2 - Composer et l'autoloading

- Initialiser le dossier comme étant un projet composer 

```shell
$ composer init  # crée le fichier composer.json
$ composer install # install l'autoloader
```

- Remplir le fichier composer avec la règle d'autoloading

```json
"autoload": {
    "psr-4": {
        "RootName\\": "src/"
    }
}
```

- Réinitialiser l'autoloader

```shell
$ composer dump-autoload
```

## Etape 3 - Le router 

Créer la classe Router

- créer une methode `run()` qui redirigera vers le bon controller et la bonne methode en fonction de l'url

Voici une liste de route que l'on peut implementer:

- "/", GET => Accueil
- "/login, GET => page de connexion
- "/register, GET => page d'inscription
- "/register, POST =>  crée le nouveau user
- "/dashboard, GET => dashboard qui montre toutes les todo liste de l'utilisateur
- "/dashboard/{todo}, GET => montre le détail d'une todo liste
- "/dashboard/nouveau, GET => création d'une todo liste
- "/dashboard/nouveau, POST => crée la todo liste en base dde données
- "/dashboard/{todo}, POST => met en jour la todo liste
- "/dashboard/{todo}/delete => supprime la todoliste

## Etape 3 - Les Models

Création des entitées `User`, `TodoList`, `Task` et des managers `UserManager`, `TodoListManager`, `TaskManager``

Pour les manager, on va pouvoir implementer les methodes:

- `find($id)` => retrouve une entité grâce à son id
- `findOneBy($field, $value)` => retrouve une entité grâce à n'importe quel champs renseigné
- `all()` => retrouve toutes les entité
- `store()` => enregistre une entité
- `update($param)` => met à jour une entité
- `delete($param)`=> supprime une entité

## Etape 4 - Le controller

Créer un `TodoController` avec les methodes suivante:

- `index()` => montre toutes les todo d'un user
- `show($param)`=> montre une todoliste
- `create()` => formulaire de création
- `store()`=> enregistre la todoliste
- `edit($param)` => formulaire pour editer la todoliste
- `update($param)`=> met à jour la todoliste
- `delete($param)`=> supprime la todo liste