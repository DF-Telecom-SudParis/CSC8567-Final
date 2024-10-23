<p align="center">
    <img src="https://github.com/user-attachments/assets/3ba5a526-c617-49c7-8165-30c3f3505d5c" width="300" alt="TSP logo">
</p>

# CSC8567 - Architectures distribuées et applications web
## Projet Final Kubernetes

## Auteurs

- Timothée Mathubert (timothee.mathubert@telecom-sudparis.eu)
- Gatien Roujanski (gatien.roujanski@telecom-sudparis.eu)
- Arthur Jovart (arthur.jovart@telecom-sudparis.eu)
- (Inspirations du cours NET4255 de Vincent Gauthier & Gatien Roujanski)

## Présentation du projet Kubernetes

C'est le moment d'attaquer Kubernetes !

Pour venir à bout de votre projet, les règles sont un peu différentes que lors de la première partie du cours.

Il vous faudra compléter des Défis. Compléter des Défis vous rapporte des points. Pour compléter un défi, il faut :
- Compléter le Contenu, expliquant les tâches à réaliser pour le Défi.
- Esquisser un schéma de l'infrastructure réseau complète mise en jeu lors de la réalisation du Contenu.
- Répondre aux Questions lorsqu'il y en a.

Pour compléter un Défi, il faut aller le faire valider auprès d'un professeur (Timothée ou Gatien), en faisant une petite démo montrant ce que vous avez fait, et en expliquant le schéma que vous avez réalisé.

Lorsque votre Défi est validé, vous pouvez passer au Défi suivant.

À partir du Défi 2, les premiers groupes ayant complété un Défi révèleront à tout le monde le Défi suivant. Considérez que lorsque vous arrivez à ces Défis là, vous vous débrouillez bien !

Bon courage !

## Démarrage des projets

Pour cette partie du cours, vous aurez besoin d'installer le programme `kubectl`.
1. Veuillez suivre les instructions disponibles sur ce [tuto d'installation de `kubectl`](https://kubernetes.io/fr/docs/tasks/tools/install-kubectl/).
2. Venez ensuite voir un professeur : donnez la composition de votre groupe. Un namespace vous sera alors créé sur le cluster du cours (`u-XXX`). Un compte vous sera aussi créé sur le cluster.
3. Une fois votre compte créé, [connectez-vous au site de gestion du cluster](https://csc8567.luxbulb.org) avec vos identifiants, et créez vous un mot de passe personnel.
4. Allez ensuite dans la rubrique "Cluster Management". 
5. Sélectionnez le cluster "csc8567", et cliquez sur "Download KubeConfig".
6. Créez un dossier `.kube` dans votre dossier Home :
```
mkdir ~/.kube
```
7. Déplacez le fichier téléchargé à l'adresse `~/.kube/config`:
```
mv ~/Téléchargements/csc8567.yaml ~/.kube/config
```
8. Essayez la commande dans un terminal (en remplaçant le "u-XXX" par votre ID d'utilisateur/espace de noms) :
```
kubectl get pods -n u-XXX
```
*Pour info, la notion `-n u-XXX` permet de préciser que la commande est exécutée dans l'espace de noms "u-XXX". Sans la mention de ce dernier, elle serait exécutée dans le namespace "default", auquel vous n'avez pas accès. Probablement une info utile pour la suite !*

Ceci devrait vous afficher une sortie :
```
No resources found in u-XXX namespace.
```
Si vous avez une erreur, allez voir un professeur pour résoudre le problème.
8. Une fois que la dernière commande à fonctionné, vous êtes fin prêts pour démarrer le projet !

## Modalités de rendu du Projet & soutenance

Vous êtes répartis en groupes de 2 ou 3 personnes, et vous partagez l'espace de noms associé à votre groupe.
Le rendu final sera commun au membres du groupe : une seule personne du groupe le rendra sur Moodle, et précisera les noms des membres du groupe.
La note du Projet se basera sur votre avancée dans les **Défis** listés ci-après.

Votre rendu sera une archive `zip` ou `tar.gz` contenant, **pour chaque Défi** :
- Dans le cas où seules des commandes étaient utiles à la réalisation du Défi, un fichier contenant ligne par ligne les commandes que vous avez exécutées pour réussir le Contenu.
- Les fichiers de configuration que vous avez appliqués pour réussir un Défi. *Dans le cas où des fichiers de configurations ont été utilisés, il n'est pas nécessaire de repréciser les commandes que vous avez exécutées pour les appliquer.*
- Un schéma d'infrastructure représentant tous les composants réseau participant au fonctionnement du service. *Référez-vous aux les présentations et n'hésitez pas à poser des questions si vous avez des doutes sur certains points !*
- Les réponses aux questions de chaque Défi.

Chaque contenu de rendu de Défi sera dans un dossier séparé dans l'archive (`defi1`,`defi2`,...).

Pour la soutenance, vous devez laisser sur le cluster du cours et dans votre espace de noms tous les déploiements que vous avez fait. **Ne les supprimez pas après avoir rendu l'archive !!**

Le jour de la soutenance :
- **Venez 15mn avant l'horaire de passage, avec l'ordinateur prêt à présenter.**
- Annoncez le dernier Défi réalisé.
- Les deux premiers tiers de votre présentation serviront à présenter votre projet final (fonctionnalités web et infrastructure sur le cluster Kubernetes du cours).
- Le dernier tiers sera réservé aux questions.
- Chaque soutenance durera 15 minutes.

On espère que cette partie va vous plaire, et vous donner des idées plus claire sur la puissance de ce super outil qu'est Kubernetes !

## Conseils de travail en groupe

- Créez-vous un répo Git commun dans lequel vous allez travailler ensemble. Vous pourrez plus facilement suivre l'avancement des uns et des autres.
- Lorsque vous avancez dans votre travail, créez de nouvelles branches. Une fois que vous avez terminé, faites des Pull Requests.
- Commentez fréquement vos fichiers de code et de configuration pour les rendre plus clairs pour vos équipiers ou équipières.
- Communiquez !!

# Les Défis

## Premiers pas sur Kubernetes (Défi 1)

### Contenu
Tout d'abord, nous allons lancer un premier Pod, qui contiendra simplement un site web affichant une page.

Un Pod, c'est plus ou moins la version Kubernetes d'un conteneur de Docker.

- Pour créer ce Pod, il faut créer un Deployment et préciser l'image (Docker en l'occurence) utilisée pour créer le Deployment.
- La commande suivante vous permet de créer un Deployment :
```
kubectl create deployment [Nom du Deployment] --image=[chemin/vers/l'image/sur/Docker/Hub:tag]
```
- Pour récupérer des images, il est possible de les publier sur [Docker Hub](https://hub.docker.com). Celle que nous allons utiliser se trouve [ici](https://hub.docker.com/r/xhelozs/csc8567). Elle porte le tag "v1".
- Les informations sur la construction de l'image sont disponibles dans le dossier `csc8567-web-nodb` de ce même répo.
- Comparez votre objectif à la documentation pour réussir à créer le Pod : [votre premier Deployment](https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/).
- Ensuite, nous allons utiliser le `port-forward` permis par Kubernetes pour mapper le port du Pod du site sur un port de notre interface `localhost`.
```
kubectl port-forward pods/[Nom du Pod] [Port localhost]:[Port du Pod]
```
Alors, le site devrait être visible depuis `localhost:[Port localhost]`. Si c'est le cas, vous avez complété ce Contenu avec succès !

Petite commande supplémentaire qui pourrait vous aider en plus :
```
kubectl logs [Nom du Pod]
```

### Questions

Le schéma déjà ça sera bien ! Venez voir un prof quand vous (pensez) l'avoir fini.

## Deuxièmes pas sur Kubernetes (ça ne se dit pas ?) (Défi 2)

### Contenu

Bon, on a déployé un Pod, c'est sympa, mais ça nous avance pas beaucoup de Docker, c'est même plus compliqué...

Vous en faites pas : on va compliquer encore un peu plus les choses !

Vous allez créer maintenant votre premier Deployment, pour l'image `csc8567` utilisée lors du dernier Défi.

**Votre Deployment créera 3 répliques du Pod faisant tourner le site.**

Pour ce faire, il va falloir comprendre ce qu'est un Deployment, comment ça se configure. Pour ceci, vous pouvez visionner [cette vidéo](https://youtu.be/qmDzcu5uY1I?si=jeoMTcyKxxQ70jmG).

Ensuite, le soucis précédent va se réitérer : il faut trouver un moyen d'accéder au service. On va utiliser pour ça une combinaison gagnante : un service ClusterIP + un proxy.

Deux ressources sont alors intéréssantes à parcourir pour mieux comprendre :
- [Accéder à des services sur le Cluster](https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster-services/)
- [Construire des URLs personnalisés sur l'API](https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster-services/#manually-constructing-apiserver-proxy-urls)

Ensuite, on souhaite allouer des ressources particulières à chaque Pod du Deployment. En particulier :
- 1/10 CPU par pod 
- 100 Mo de mémoire RAM par pod

En revanche, on veut aussi limiter les ressources à :
- 1/5 CPU par pod
- 200 Mo de mémoire RAM par pod

Cette ressource va vous aider à arriver à vous fins :
- [Resource Management for Pods and Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

Vous pourrez alors vous connecter à votre service via le proxy :
```bash
kubectl proxy
```
Votre service devrait alors être disponible à l'adresse : 
`http://127.0.0.1:8001/api/v1/namespaces/[votre espace de noms]/services/[nom de votre service]/proxy/`

### Questions
1. Quel est le but d'un service ?
2. Quelle est la différence entre les service ClusterIP et NodePort ?
3. Et le schéma !!

## Connexions dangereuses (Défi 3)
### Contenu
Pas mal ! Maintenant l'étape suivante : on va reprendre votre projet Django.

Avant tout, vous aller le copier, et faire en sorte que **le site soit contenu avec les deux apps (public et api) dans une image Docker**, que vous allez publier sur [Docker Hub](https://hub.docker.com).

**Utilisez un Deployment pour déployer votre site Django similairement à celui créé précédemment.**

Sauf que c'est pas fini cette fois ! **Vous allez aussi créer un autre Deployment, contenant un unique Pod, pour déployer la base de données Postgresql. Le service que vous utiliserez est un ClusterIP.**

**Quelques indices sur la procédure pour s'en sortir :**

- Vous pouvez passer des variables d'environnement dans les conteneurs des Pods dans le fichier de Deployment (un peu comme on le faisait avec Docker Compose).
- Vous aller devoir créer une nouvelle image Docker contenant la totalité du site Django, avec vos applis. Il vous faut donc utiliser votre projet de la première partie du cours, écrire un nouveau `Dockerfile`, ajouter des fichiers (settings, urls) qui chargeront tout votre projet. Créez l'image avec la commande :
```
docker build -t [Nom d'utilisateur Docker Hub]/[Nom de votre image]:[version (v1,v2,...)] -f [Nom de votre Dockerfile] [chemin/vers/Dockerfile] 
```
Puis envoyez l'image sur Docker Hub :
```
docker push [Nom d'utilisateur Docker Hub]/[Nom de votre image]:[version (v1,v2,...)]
```
- Si jamais ça ne fonctionne pas du premier coup, il vous faudra souvent construire une nouvelle image Docker de votre site Django. Associez des versions dans le tag de votre image au fur et à mesure, et modifiez le tag dans votre fichier de déploiement (*ceci est nécessaire car, par défaut, le cluster va mettre les images Docker en cache, et va réutiliser ce cache une fois qu'une image est téléchargée : modifier le tag va faire en sorte qu'il récupère à nouveau l'image sur Docker Hub, car son tag est différent donc l'image est différente*).
- Parfois, le lancement des conteneurs peut être un peu long. Patientez une ou deux minutes avant de commencer à faire des requêtes vers le site via le proxy.
- Créez les Deployments pour Django et la base de données dans des fichiers différents !

Et un peu plus de documentation pour comprendre comment faire ! Bon courage, c'est un Défi assez difficile lorsqu'on le fait pour la première fois !

- [Connecter des Applications avec des Services](https://kubernetes.io/docs/tutorials/services/connect-applications-service/)

### Questions

- Pourquoi utilise-t-on un service type NodePort pour le site Django et un service type ClusterIP pour la base de données ?
- Quelle critique pouvez-vous donner vis-à-vis de l'utilisation d'un Pod pour la base de données ?
- Sur quel type de ressource KubeDNS crée des entrées ? Quelle information propre a la ressource est utilisée ?
- Le schéma !

## Internet ! Me voilà ! (Défi 4)

### Contenu

Vraiment pas mal !

Maintenant, on va faire en sorte que votre site soit accessible depuis Internet. Plus partique pour un site web, non ?

Vous allez donc créer ce que l'on appelle un Ingress.

Le but, c'est que votre site devienne accessible à l'adresse <https://django.votre_nom_de_groupe.csc8567.luxbulb.org/>

**Une fois que votre configuration d'Ingress est appliquée, allez voir un professeur pour qu'il crée l'entrée DNS qui vous permettra d'accéder à votre Ingress !**

Pour la documentation de ce défi :

- [Généralités sur les Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- [Utilisation d'un LoadBalancer MetalLB avec rke2-ingress-nginx-controller](https://www.adaltas.com/fr/2022/09/08/kubernetes-metallb-nginx/) (pour le schéma uniquement)

Petite information supplémentaire pour le schéma : ci-dessous ce que retourne la commande `kubectl get services -n kube-system` lorsque l'on dispose des permissions suffisantes.

```
NAME                                      TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                      AGE
rke2-ingress-nginx-controller             LoadBalancer   10.43.144.159   157.159.11.201   80:31324/TCP,443:30747/TCP   10h
```

### Questions

On met à jour le schéma, ça suffira !

## Au complet ! (Défi 5)

### Contenu

C'est enfin le moment : on va reproduire l'infrastructure qu'on avait sur Docker, mais version (presque) Kubernetes !

Pour récapituler, il faut que :

- Vous ayez deux images Docker permettant de faire tourner séparément les applications API et Public (ou l'équivalent de votre projet).
- Vous faites tourner ces deux images dans des Deployments (3 pods répliqués, même allocations/limitations de ressources qu'au Défi 2), derrière des services bien choisis.
- Vous faites tourner la base de données via un Deployement (1 pod, allocations/limitations idem que pour API et Public), derrière un service bien choisi.
- Vous utilisez l'Ingress pour diriger les requêtes (l'Ingress vient remplacer votre proxy Nginx de Docker).

Pas plus de documentation pour cette fois ! Vous avez déjà tout ce qu'il vous faut.

### Questions

Un beau schéma !

## Quelqu'un a dit "HELM" ?! (Défi 6)

### Contenu

Vous vous souvenez de docker compose ? Eh bien on a un peu l'équivalent sur Kubernetes : Helm, et surtout les chartes Helm.

L'objectif est de créer une charte Helm qui automatise le déploiement de l'infrastructure que vous avez mise en oeuvre au Défi précédent.

Également, vous aller utiliser ConfigMaps pour stocker les informations utiles à la connexion entre le site et la base de données.

Cette fois, on a de la doc à vous partager pour tout ça :

- [Bien débuter avec Helm](https://helm.sh/docs/chart_template_guide/getting_started/)
- [Utiliser ConfigMaps dans Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

### Questions

Rien ! Une belle charte Helm fera amplement l'affaire.

## Connexions moins dangereuses (Défi 7)

## ??? (Défi 8)
