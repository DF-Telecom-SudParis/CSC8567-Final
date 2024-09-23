# CSC8567-Kube
Template de répo pour le projet Kubernetes de CSC8567 (Projet final)

## Auteurs

Timothée Mathubert
Gatien Roujanski
Arthur Jovart

## Démarrage des projets

Pour cette partie du cours, vous aurez besoin d'installer le programme `kubectl`.
Veuillez suivre les instructions disponibles sur ce [tuto d'installation de `kubectl`](https://kubernetes.io/fr/docs/tasks/tools/install-kubectl/).

Venez ensuite voir un professeur : donnez la composition de votre groupe. Un namespace vous sera alors créé sur le cluster du cours (`groupe-X` où X est le numéro de votre groupe). Un compte vous sera aussi créé sur le cluster.

Une fois votre compte créé, [connectez-vous au site de gestion du cluster](https://kube.luxbulb.org) avec vos identifiants, et créez vous un mot de passe personnel. Allez ensuite dans la rubrique "Cluster Management". Sélectionnez le cluster "csc8567", et cliquez sur "Download KubeConfig". Déplacez le fichier téléchargé à l'adresse `~/.kube/config` (`config` n'est pas un répertoire, c'est bien le fichier de configuration que vous avez téléchargé : il faut le renommer).

Essayez la commande dans un terminal :
```
kubectl cluster-info -n groupe-X
```
Ceci devrait vous afficher une sortie :
```
Kubernetes control plane is running at https://kube.luxbulb.org/k8s/clusters/local

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```
Si vous avez une erreur, allez voir un professeur.

Une fois que la dernière commande à fonctionné, vous êtes fin prêts pour démarrer le projet !