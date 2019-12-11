<center><img src="images/jenkins.png" alt="Jenkins" width="290"/></center>

# Création d'un projet Maven
- Installer les plugins suivants :
1. Maven integration
2. Parameterized Trigger
3. Delivery Pipeline Plugin

----------

- Cible à atteindre :
<center> 
<img src="images/image1.png"/>
</center>

----------

## Item "Petclinic_compile"
- Description : cet item se chargera de récupérer les sources du projet sur GitHub et lancera la compilation sous Maven.
- Nom : Petclinic_compile
- Type : Projet Maven
- Actions :
1. Récupère les sources sur GitHub 
2. Lance la tâche maven "clean compile"

## Création d'une vue de type "Delivery Pipeline View"
- Description : cette vue permmettra d'afficher les enchaînements entre les items.
- Nom de la vue : Petclinic pipeline
- Dans la zone "**Pipelines**", ajouter un component avec :
 - Name : Petclinic pipeline
 - Initial Job : Petclinic\_compile
- Afficher la nouvelle vue

## Item Petclinic_package
- Description : cet item doit faite le package WAR du projet. Il doit pouvoir utiliser le workspace de l'item précédent.
- Nom : Petclinic\_package
- Type : Projet Maven
- Paramètre string : WORKSPACE_PARENT
- Actions :
1. Prends en paramètre le workspace du build parent (WORKSPACE\_PARENT)
2. Lance la tâche maven "**package**"
3. Dans la section build, spécifier le répertoire de travail spécifique avec la valeur $WORKSAPCE\_PARENT
- Modifier l'item "**Petclinic\_compile**" pour ajouter l'appel à l'item "**Petclinic\_package**" après le lancement de la tâche maven "**clean compile**". Initialiser la variable WORKSPACE\_PARENT avec le workspace de l'item "**Petclinic\_compile**"
> Astuce : Chaîner les items en utilisant une action "Trigger parameterized build on other projects"

## Item "Petclinic_deployQualification" :
- Nom : Petclinic_deployQualification
- Type : Projet free-style
- Actions :
1. Prends en paramètre le workspace du build parent (WORKSPACE\_PARENT)
2. Copie le fichier **petclinic.war** du workspace (répertoire target) dans **/var/tmp**
3. Modifier l'item "Petclinic\_package" pour ajouter l'appel à l'item "Petclinic\_deployQualification" après le lancement de la tâche maven "**package**". Initialiser la variable WORKSPACE\_PARENT avec le workspace de l'item "**Petclinic\_package**"















 
