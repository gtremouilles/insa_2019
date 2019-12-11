<center><img src="images/sonarqube.png" alt="Sonarqube" width="300"/></center>


# Installation du docker
- Lancer le docker Sonarqube :   
```
docker run -d --name sonarqube -p 9000:9000 sonarqube
```
- Dans un navigateur, aller sur l'URL : [http://localhost:9000](http://localhost:9000)
- Se connecter avec le compte "admin" (mdp: admin)

# Analyse du projet spring-framework-petclinic

- Se connecter sur le docker JenkinsCI avec la commande bash :  
```
docker exec -it JenkinsCI bash
``` 
- Récupérer les sources du projet spring-framework-petclinic (remplacer XXXXXXX par votre compte GitHub) :  
```
git clone https://github.com/XXXXXXX/spring-framework-petclinic.git
```
- Lancer un build du projet :   
```
mvn -B -DskipTests clean compile
```
- Lancer une analyse sonar :   
```
mvn sonar:sonar -Dsonar.host.url=http://<IP_SERVEUR_SONAR>:9000
```

- Consulter les résultats sur Sonarqube :

<img src="images/sonar1.png" alt="Sonarqube" width="1042"/>

- Consulter la liste des bugs :

<img src="images/sonar2.png" alt="Sonarqube" width="1042"/>

----------
# Correction d'un bug

- Dans Sonarqube, consulter le 1er bug rencontré dans le fichier "**src/main/webapp/WEB-INF/jsp/owners/ownerDetails.jsp**"
- Corriger ce bug dans le projet spring-framework-petclinic
- Relancer une analyse Sonar
- Vérifier que le bug a bien disparu dans l'analyse

# Ajout d'un nouveau bug
- A partir du menu "**Rules**", sélectionner une règle de type "**Bug**" dans le langage "**Java**"
- Copier la partie "**Noncompliant Code Example**" de cette règle et coller les lignes dans un fichier source Java du projet spring-framework-petclinic
- Relancer une analyse Sonar
- Vérifier que votre nouveau bug est bien remonté dans l'analyse Sonar