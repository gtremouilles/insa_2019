<center><img src="https://cdn.ttgtmedia.com/visuals/LeMagIT/hero_article/Logo-Jenkins.jpg" alt="Jenkins" width="290"/></center>

# Installation du docker :  
``` 
docker pull frouland/myjenkins:0.2   
docker run -d --name JenkinsCI -e http_proxy='' -e https_proxy='' -p 8080:8080 -p 50000:50000  
docker exec -it JenkinsCI cat /var/jenkins_home/secrets/initialAdminPassword   
```

- Ajout du mot de passe admin pour débloquer Jenkins
- Mise à jour du proxy dans Jenkins pour les plugins : http://localhost:8080/pluginManager/advanced  
- Installation des plugins par défaut
- Administrer Jenkins :
1. JDK *(décocher Install automatically)* : Nom=java-1.8-openjdk JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk
2. Maven *(décocher Install automatically)* : Nom=M3 MAVEN_HOME=/usr/share/maven
		

# Création d'un projet Freestyle
- Créer un projet free-style nommé "Petclinic" qui devra :
1. Récupérer les sources de spring-framework-petclinic dans GitHub
2. Lancer la tâche de compilation maven : **mvn -B -DskipTests -DproxySet=true -DproxyHost=marc.proxy.corp.sopra -DproxyPort=8080 clean package**
3. Archiver l'artifact généré (petclinic.war)
4. Renommer le fichier petclinic.war généré dans le dossier target de la façon suivante : petclinic-NUM_BUILD-TIMESTAMP.war Exemple : 

# Création d'un projet Maven
- Installer les plugins suivants :
1. Maven integration
2. Parameterized Trigger

<center>![image1](./image.png)</center>

## Item Petclinic compile :
- Nom : Petclinic compile
- Type : Projet Maven
- Actions :
1. Récupère les sources sur GitHub 
2. Lance la tâche maven "clean compile"
3. Appel l'item Petclinic package avec passage du paramètre WORKSPACE_PARENT

## Item Petclinic package :
- Nom : Petclinic package
- Type : Projet Maven
- Actions :
1. Prends en paramètre le workspace du build parent (WORKSPACE_PARENT)
2. Lance la tâche maven "package"

## Item Petclinic deployQualification :
- Nom : Petclinic deployQualification
- Type : Projet Maven
- Actions :
1. Prends en paramètre le workspace du build parent (WORKSPACE_PARENT)
2. Lance la tâche maven "package"















 
