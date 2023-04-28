<div style="display:flex; align-items:center;">
  <h1 style="margin-right:auto;">Projet-AWS-terraform</h1>
 <img src="https://img.shields.io/badge/Made%20with-terraform-blue" alt="Terraform badge">
</div>


Dans le cadre de notre semaine de formation sur les outils terraform et puppet nous avons un projet terraform à créer

## Sujet

Dans le cadre du projet nous devons déployer une infrastructure complète AWS avec Terrafom, les prérequis sont :
- un module pour créer une instance ec2 utilisant la dernière version de ubuntu bionic, cette version n'étant pas disponible nous avons opté pour focal, dont la taille et le tag sont variabilisés.
- un module pour créer un volume ebs dont la taille est variabilisée.
- un module pour créer une security qui ouvrira le 80 et 443.
- un dossier app qui va utiliser les 4 modules pour déployer une ec2.
- installer nginx et enregistrer l’ip publique dans un fichier nommé ip_ec2.txt (ces éléments sont à intégrer dans le rôle ec2)

Nous devons également, si possible :

- pousser le projet sur GitHub et partager le lien du repo à o.nebie@ecole-ipssi.net (Optionnel)
- faire un rapport pour accompagner notre solution (le readme) 

## Architecture

Voici l'arboressence de notre projet :

![image](https://user-images.githubusercontent.com/38227021/235158938-753323ec-d605-4aba-bb8e-aa6956523604.png)

## Fichier Terraform de base pour créer une instance

Dans chacun de nos modules terraform nous avons 2 fichiers :
- main.tf permet de définir les ressources à créer, les modifier ou les supprimer pour provisionner une infrastructure.
- variable.tf permet de définir les variables qui seront utilisées dans la configuration principale (main.tf) ou dans d'autres fichiers de configuration, afin de rendre la configuration plus modulaire et facilement adaptable aux différents environnements.

Dans le fichier principal de notre application se trouve un troisième fichier venant se rajouter au deux précédents. :
- terraform.tfvars permet de définir des valeurs alternatives pour les variables, ces valeurs peuvent être appellées en utilisant un -var-file=terraform.tfvars lors d'un apply ou d'un plan. 


## Execution du projet

Afin de lancer notre projet Terraform, nous allons avoir besoin d'exécuter plusieurs commandes.

Commencez par renseigner les variables avec les informations correspondant à vos besoins.

Terraform init : Cette commande permet de mettre en place un environnement de travail et l'adapter à Terraform. Cela permet de télécharger les plugins requis liés aux différents providers.

Terraform plan : Cette commande permet d'avoir une prévisualisation des modifications qui vont être apportées à l'infrastructure. Ainsi, on peut voir facilement quelles sont les parties de notre infrastructure qui sont affectées.

Terraform apply : Cette commande permet d'appliquer les modifications apportées au fichier de configuration.

En résumé, pour exécuter un projet Terraform, il faut initialiser le répertoire de travail en exécutant la commande "terraform init", générer le plan d'exécution en exécutant la commande "terraform plan" et appliquer les modifications en exécutant la commande "terraform apply".
## Variables

Ci dessous se trouvent les diverses variables modifiables de ce projet, il est conseillé de les modifier en fonction de vos besoins.

app/Variables.tf :

```terraform
#Variables Provider

variable access_key {
  default = "Mettez votre propre clé"
}

variable secret_key {
  default = "Mettez votre propre clé"
}

variable regionaws {
  default = "us-east-1"
}

#Surcharge des variables 

#EC2
variable "instance_name" {
  default = "Custom-Name"
}
variable "instance_type" {
  default = "t2.micro"  
}
#EBS
variable "size" {
  default =20
}
```
ec2/Variables.tf :

Variables par défaut

```terraform
variable "instance_name" {
    default = "Default-Name"
}
variable "instance_type" {
    default = "t2.nano"
}
```
ebs/Variables.tf :

Variables par défaut

```terraform
variable "size" {
    default = 10
}
```
## Surcharger les variables

Pour surcharger les variables par défaut vous pouvez modifier le fichier variables.tf disponible dans le dossier principal, les valeurs de ce dernier écrasent les valeurs par défaut des modules. Les lignes de code ci-dessous correspondent a la surcharge des variables instance_name et instance_type dans l'appel de module ec2.

```terraform
  #Surcharge des variables
  instance_name = var.instance_name
  instance_type = var.instance_type
  ```
  
Pour utiliser les valeurs par défaut, vous pouvez commenter les déclarations de surcharge dans les appels de module.

```terraform
  #Surcharge des variables
  #instance_name = var.instance_name
  #instance_type = var.instance_type
  ```
