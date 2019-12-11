<center><img src="images/jenkins.png" alt="Jenkins" width="290"/></center>

# Installation du docker
``` 
docker pull frouland/myjenkins:0.2   
docker run -d --name JenkinsCI -e http_proxy='' -e https_proxy='' -p 8080:8080 -p 50000:50000  
docker exec -it JenkinsCI cat /var/jenkins_home/secrets/initialAdminPassword   
```

- Dans un navigateur, ouvrir l'URL : [http://localhost:8080/](http://localhost:8080/)
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
















 
