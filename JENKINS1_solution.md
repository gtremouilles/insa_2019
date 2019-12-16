<center><img src="images/jenkins.png" alt="Jenkins" width="290"/></center>

# Solution [[Version PDF]](pdf/JENKINS1_solution.md.pdf "Ouvrir la version PDF")

# Création d'un projet Maven
- Installer les plugins suivants :
1. Maven integration
2. Parameterized Trigger
3. Delivery Pipeline Plugin

<img src="images/jenkins1_sol1.png" alt="Jenkins" width="1042"/>

----------

- Cible à atteindre :
<center> 
<img src="images/image1.png"/>
</center>

----------

## Création de l'item "Petclinic_compile"
- Description : cet item se chargera de récupérer les sources du projet sur GitHub et lancera la compilation sous Maven.  
- Nom : Petclinic_compile  
- Type : Projet Maven  

<img src="images/jenkins1_sol2.png" alt="Jenkins" width="1042"/>

- Actions :  
1. Récupère les sources sur GitHub  

<img src="images/jenkins_sol3.png" alt="Jenkins" width="1042"/>

2. Lance la tâche maven "**clean compile**"  

<img src="images/jenkins1_sol3.png" alt="Jenkins" width="1042"/>


## Création d'une vue de type "Delivery Pipeline View"
- Description : cette vue permmettra d'afficher les enchaînements entre les items.  
- Nom de la vue : Petclinic pipeline  

<img src="images/jenkins1_sol4.png" alt="Jenkins" width="1042"/>

- Dans la zone "**Pipelines**", ajouter un component avec :  
 - Name : Petclinic pipeline  
 - Initial Job : Petclinic\_compile  
 
<img src="images/jenkins1_sol5.png" alt="Jenkins" width="1042"/>

- Afficher la nouvelle vue  

<img src="images/jenkins1_sol6.png" alt="Jenkins" width="600"/>

## Création de l'item Petclinic_package
- Description : cet item doit construire le package WAR du projet. Il doit pouvoir utiliser le workspace de l'item précédent.  
- Nom : Petclinic\_package  
- Type : Projet Maven  

<img src="images/jenkins1_sol7.png" alt="Jenkins" width="600"/>

- Paramètre string : WORKSPACE\_PARENT  
- Actions :  
1. Prends en paramètre le workspace du build parent (WORKSPACE\_PARENT)  

<img src="images/jenkins1_sol8.png" alt="Jenkins" width="1042"/>

2. Lance la tâche maven "**package**"  
<img src="images/jenkins1_sol9.png" alt="Jenkins" width="1042"/>

- Dans la section build, spécifier le répertoire de travail spécifique avec la valeur $WORKSPACE\_PARENT  

<img src="images/jenkins1_sol10.png" alt="Jenkins" width="1042"/>

- Modifier l'item "**Petclinic\_compile**" pour ajouter l'appel à l'item "**Petclinic\_package**" après le lancement de la tâche maven "**clean compile**". Initialiser la variable WORKSPACE\_PARENT avec le workspace de l'item "**Petclinic\_compile**" ("**Predefined parameters**" avec le paramètre : **WORKSPACE_PARENT=$WORKSPACE**)

> Astuce : Chaîner les items en utilisant une action "**Trigger parameterized build on other projects**"  

<img src="images/jenkins1_sol11.png" alt="Jenkins" width="1042"/>

## Création de l'item "Petclinic_deployQualification"
- Description : cet item doit copier le WAR généré dans un répertoitre sur le serveur  
- Nom : Petclinic_deployQualification  
- Type : Projet free-style  

<img src="images/jenkins1_sol12.png" alt="Jenkins" width="1042"/>

- Paramètre string : WORKSPACE\_PARENT  
- Actions :  
1. Prends en paramètre le workspace du build parent (WORKSPACE\_PARENT)  

<img src="images/jenkins1_sol8.png" alt="Jenkins" width="1042"/>

2. Copie le fichier "**$WORKSPACE_PARENT/target/petclinic.war**" du workspace dans le répertoire **/var/tmp**

<img src="images/jenkins1_sol13.png" alt="Jenkins" width="1042"/>

- Modifier l'item "**Petclinic\_package**" pour ajouter l'appel à l'item "**Petclinic\_deployQualification**" après le lancement de la tâche maven "**package**". Initialiser la variable WORKSPACE\_PARENT avec le workspace de l'item "**Petclinic\_package**"  

<img src="images/jenkins1_sol14.png" alt="Jenkins" width="1042"/>

## Lancement du build 
- Lancer le build manuellement et vérifier que le WAR est bien déployé dans le répertoire "**/var/tmp**"  
- Optimiser le démarrage du build en scrutant l'outil de gestion de version toutes les minutes  
> Astuce : Utiliser l'expression * * * * * pour exécuter la tâche toutes les minutes 

<img src="images/jenkins1_sol15.png" alt="Jenkins" width="1042"/>

- Faire une modification sur le projet dans GitHub puis un commit  
- Vérifier que le build se lance bien automatiquement  











 
