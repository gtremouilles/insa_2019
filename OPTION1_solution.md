<center><img src="images/jenkins.png" alt="Sonarqube" width="300"/></center>

# Solution [[Version PDF]](pdf/OPTION1_solution.md.pdf "Ouvrir la version PDF")

# Utilisation du plugin "promoted builds"
But : utiliser le plugin "**promoted builds**" pour valider manuellement le déploiement sur le serveur de qualification

- Cible à atteindre :
<center><img src="images/jenkins5.png" alt="Jenkins" width="800"/></center>

- Installer le plugin "**promoted builds**"
<img src="images/option1_sol1.png" alt="Jenkins" width="1042"/>  

## Création de l'item Petclinic_promoteQualification
- Description : cet item doit permettre de stopper la chaine du build après la génération du package et obliger l'utilisateur à approuver manuellement le démarrage de la dernière étape du build.
- Nom : Petclinic_promoteQualification
- Type : Projet free-style
- Paramètre string : WORKSPACE\_PARENT
- Actions :
1. Prends en paramètre le workspace du build parent (WORKSPACE\_PARENT)  

<img src="images/jenkins1_sol8.png" alt="Jenkins" width="1042"/>

2. Activer l'option "**Promote builds when...**" :
	- Sélectionner le critère "**Only when manually approved**"

	<img src="images/option1_sol2.png" alt="Jenkins" width="1042"/>

	- Ajouter une action de type "**Trigger parameterized build on other projects**" qui appelle l'item "**Petclinic\_deployQualification**" avec le "**Predefined parameters**" "**WORKSPACE\_PARENT=$WORKSPACE**"

	<img src="images/option1_sol3.png" alt="Jenkins" width="1042"/>

3. Modifier l'item "**Petclinic_package**" qui doit maintenant appeler ce nouvel item.

	<img src="images/option1_sol4.png" alt="Jenkins" width="1042"/>

4. Lancer un build de l'item "**Petclinic\_compile**" manuellement

	<img src="images/option1_sol5.png" alt="Jenkins" width="1042"/>  

> Astuce : pour regrouper 2 items dans le même groupe de la vue "**Delivery pipeline**", ajouter le même "**Stage name**" sur les 2 items :
><img src="images/option3.png" alt="Jenkins" width="1042"/>  
>A faire pour les items "**Petclinic\_promoteQualifiaction**" et "**Petclinic\_deployQualification**"


- Lorsque le build arrivera à l'étape "**Petclinic_promoteQualification**", il faudra alors approuver manuellement le "**Promotion Status**"

<img src="images/option1.png" alt="Jenkins" width="200"/>

<img src="images/option2.png" alt="Jenkins" width="1042"/>

