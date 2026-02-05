# TP Docker - Évaluation

**Formation BTS/Licence - CI/CD (Docker / Git)**  
**Durée** : 10 minutes  
**Date** : 05 février 2026

---

## Objectifs

Ce TP vise à évaluer vos compétences sur :

- La manipulation des conteneurs avec les commandes de base Docker
- La création d'un fichier `docker-compose.yml` pour orchestrer plusieurs services

---

## Partie 1 : Commandes Docker de base (5 minutes)

### Objectif

Manipuler des conteneurs avec `docker run` et `docker exec -it`

### Consignes

Réalisez les opérations suivantes dans l'ordre :

1. **Téléchargez** l'image officielle `nginx:alpine`

\\\bash

docker pull nginx:alpine

\\\

2. **Lancez** un conteneur nommé `test-nginx` avec les caractéristiques suivantes :
   - Mode détaché (arrière-plan)
   - Port 8080 de votre machine mappé sur le port 80 du conteneur

```bash

docker run -d --name test-nginx -p 8080:80 nginx:alpine

```

3. **Vérifiez** que le conteneur est bien en cours d'exécution

```bash

docker ps

```

4. **Connectez-vous** au shell du conteneur en mode interactif

```bash

docker exec -it cdc6d43f1b4c bash

```

5. **Dans le conteneur**, créez un fichier `/usr/share/nginx/html/test.html` contenant le texte suivant :

   ```
   Hello Docker Eval
   ```

```bash

mkdir /usr/share/nginx/html/
echo 'Hello Docker Eval' >> test.html
docker exec -it cdc6d43f1b4c bash

```

6. **Sortez** du conteneur

7. **Arrêtez** puis **supprimez** le conteneur `test-nginx`

### Barème : 5 points

- Téléchargement de l'image : **0.5 pt**
- Commande `docker run` avec les bonnes options : **1.5 pt**
- Vérification de l'exécution : **0.5 pt**
- Connexion interactive au conteneur : **1 pt**
- Création du fichier dans le conteneur : **1 pt**
- Arrêt et suppression du conteneur : **0.5 pt**

---

## Partie 2 : Docker Compose (5 minutes)

### Objectif

Créer un fichier `docker-compose.yml` fonctionnel pour déployer une application web avec base de données

### Consignes

Créez un fichier `docker-compose.yml` qui respecte les spécifications suivantes :

#### Service `web`

- **Image** : `nginx:alpine`
- **Nom du conteneur** : `eval-web`
- **Mapping de port** : 8080 (hôte) → 80 (conteneur)
- **Réseau** : `eval-network`

#### Service `db`

- **Image** : `mysql:8.0`
- **Nom du conteneur** : `eval-mysql`
- **Variables d'environnement** :
  - `MYSQL_ROOT_PASSWORD: secret123`
  - `MYSQL_DATABASE: eval_db`
- **Volume** : Volume nommé `mysql-data` monté sur `/var/lib/mysql`
- **Réseau** : `eval-network`

#### Volumes

Déclarez le volume nommé `mysql-data`

#### Networks

Déclarez le réseau `eval-network`

### Lancement

Une fois le fichier créé, **lancez la stack complète en arrière-plan** avec la commande appropriée.

### Barème : 5 points

- Structure générale valide (`version`, `services`, `volumes`, `networks`) : **1 pt**
- Configuration correcte du service `web` : **1 pt**
- Configuration correcte du service `db` (image, variables, volume) : **1.5 pt**
- Déclaration des volumes et réseaux : **1 pt**
- Commande de lancement correcte : **0.5 pt**

---

## Note finale

**Total** : 10 points

---

## Consignes générales

- Vous travaillez **individuellement**
- Vous pouvez consulter vos notes de cours
- Testez vos commandes pour vous assurer qu'elles fonctionnent
- Notez toutes les commandes que vous exécutez pour la Partie 1
- Sauvegardez votre fichier `docker-compose.yml` pour la Partie 2

**Bon courage !**
