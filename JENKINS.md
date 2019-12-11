<center><img src="images/jenkins.png" alt="Jenkins" width="290"/></center>

# Installation du docker
``` 
docker pull frouland/myjenkins:0.2   
docker run -d --name JenkinsCI -e http_proxy='' -e https_proxy='' -p 8080:8080 -p 50000:50000  
docker exec -it JenkinsCI cat /var/jenkins_home/secrets/initialAdminPassword   
```

- Ajout du mot de passe admin pour débloquer Jenkins
- Mise à jour du proxy dans Jenkins pour les plugins : http://localhost:8080/pluginManager/advanced  
- Installation des plugins par défaut
- Administrer Jenkins > Configuration globale des outils :
1. JDK *(décocher Install automatically)* : 
	- Nom : java-1.8-openjdk 
	- JAVA\_HOME : /usr/lib/jvm/java-1.8-openjdk
2. Maven *(décocher Install automatically)* : 
	- Nom : M3 
	- MAVEN\_HOME : /usr/share/maven
		

# Création d'un projet free-style
- Créer un projet free-style nommé "Petclinic" qui devra :
1. Récupérer les sources de **spring-framework-petclinic** dans GitHub
2. Lancer la tâche de compilation maven : **mvn -B -DskipTests -DproxySet=true -DproxyHost=marc.proxy.corp.sopra -DproxyPort=8080 clean package** en executant un scipt shell
3. Ajouter une tâche pour renommer le fichier **petclinic.war** généré dans le dossier target de la façon suivante : petclinic-NUM_BUILD-TIMESTAMP.war Exemple : petclinic-4-20191210102322.war 
> Astuce :  
> DATE\_WITH\_TIME=`date "+%Y%m%d-%H%M%S"`;   
> NEW\_NAME="petclinic\_$BUILD\_NUMBER-$DATE\_WITH\_TIME.war";

4. Ajouter une action à la suite du build pour archiver l'artifact généré (petclinic.war)
5. Lancer le build manuellement
6. Consulter le log du build et l'espace de travail
7. (Option) Ajouter une action pour supprimer le workspace une fois le build terminé

# Création d'un projet Maven
- Installer les plugins suivants :
1. Maven integration
2. Parameterized Trigger
3. Delivery Pipeline Plugin

Cible :
<center> 
<img src="images/image1.png"/>
</center>


## Item "Petclinic compile"
- Nom : Petclinic compile
- Type : Projet Maven
- Actions :
1. Récupère les sources sur GitHub 
2. Lance la tâche maven "clean compile"

## Création d'une vue de type "Delivery Pipeline View"
- Nom de la vue : Petclinic pipeline
- Dans la zone "Pipelines", ajouter un component avec :
 - Name=Petclinic pipeline
 - Initial Job=Petclinic compile
- Afficher la nouvelle vue

## Item Petclinic package
- Nom : Petclinic package
- Type : Projet Maven
- Paramètre string : WORKSPACE_PARENT
- Actions :
1. Prends en paramètre le workspace du build parent (WORKSPACE\_PARENT)
2. Lance la tâche maven "package"
3. Dans la section build, spécifier le répertoire de travail spécifique avec la valeur $WORKSAPCE\_PARENT
- Modifier l'item "Petclinic compile" pour ajouter l'appel à l'item "Petclinic package" après le lancement de la tâche maven "clean compile". Initialiser la variable WORKSPACE\_PARENT avec le workspace de l'item "Petclinic compile"
> Astuce : Chaîner les items en utilisant une action "Trigger parameterized build on other projects"

## Item "Petclinic deployQualification" :
- Nom : Petclinic deployQualification
- Type : Projet free-style
- Actions :
1. Prends en paramètre le workspace du build parent (WORKSPACE\_PARENT)
2. Copie le fichier petclinic.war du workspace (répertoire target) dans /var/tmp
3. Modifier l'item "Petclinic compile" pour ajouter l'appel à l'item "Petclinic package" après le lancement de la tâche maven "clean compile". Initialiser la variable WORKSPACE\_PARENT avec le workspace de l'item "Petclinic compile"















 
