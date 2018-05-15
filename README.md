# agd.data.gouv.fr

Le site de l'AGD

## Contribuer

**TODO**

## Démarrage rapide

### Assets

```shell
yarn install && yarn build
```
### Ruby natif

Installer bundler

```
gem install bundler
```

Compiler et démarrer un serveur de documentation

```
git clone https://github.com/etalab/agd.data.gouv.fr
cd agd.data.gouv.fr
bundle install
bundle exec jekyll serve
```

Le site sera disponible sur <http://localhost:4000>.

### Docker Compose

Vous pouvez utiliser [docker-compose](https://docs.docker.com/compose/) pour tester vos modifications localement avant de les soumettre.
Pour ce faire, il suffit simplement d'executer la commande:

```
docker-compose up
```

Ceci va télécharger l'image docker de [Jekyll](https://www.jekyll.io/) et installer les dépendances nécéssaires avant d'effectuer le rendu du site.
Le résultat sera disponible sur <http://localhost:4000>. Les modifications sont automatiquement prises en compte et provoquent un nouveau rendu du site.
