<center><img src="https://upload.wikimedia.org/wikipedia/commons/e/e6/Sonarqube-48x200.png" alt="Sonarqube" width="300"/></center>


# Sonar - Analyse du projet spring-fremework-petclinic

- Se connecter sur le docker JenkinsCI avec la commande bash : 
```
docker exec -it JenkinsCI bash
``` 
- Récupérer les sources du projet spring-framework-petclinic :
```
git clone https://github.com/XXXXXXX/spring-framework-petclinic.git
```
- Lancer un build du projet :   
```
mvn -B -DskipTests clean compile
```
- Lancer une analyse sonar :   
```
mvn sonar:sonar -Dsonar.java.binaries=target/classes -Dsonar.projectKey=Petclinic -Dsonar.host.url=http://192.168.0.49:9000 -Dsonar.login=731514228828f596efb99b42f59d94b14f6f1863
```