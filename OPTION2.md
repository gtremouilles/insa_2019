<center><img src="images/jenkins.png" alt="Sonarqube" width="300"/></center>

# Utilisation d'un Jenkinsfile
- Modifier le fichier Jenkinsfile de votre projet spring-framework-petclinic sous GitHub de la façon suivante :   
```groovy   
pipeline {  
    agent any  

    stages {  
        stage('Checkout') {  
            steps {  
                echo 'Checkout...'  
                git 'https://github.com/XXXXXX/spring-framework-petclinic.git' 
                
            }  
        }  
        stage('Build') {  
            steps {  
                parallel(  
                  build: {  
                    echo 'Building...'  
                    sh 'mvn clean install'  
                    archiveArtifacts 'target/*.war'  
                  },  
                  sonar: {  
                    echo "Analyse Sonar..."  
                  }  
                )                 
            }  
            
        }  
        stage('Deploy') {  
            steps {  
                echo 'Deploying...'  
                sh 'cp target/*.war /var/tmp'  
            }  
        }  
    }  
}  
```   

- Remplacer XXXXXX dans l'URL Git par votre compte GitHub
- Lancer le build manuellement
- Ouvrir le pipeline avec OpenBlueOcean pour voir le résultat

> Pour plus d'informations sur la construction du Jenkinsfile, aller à l'adresse suivante : [https://jenkins.io/doc/book/pipeline/jenkinsfile/](https://jenkins.io/doc/book/pipeline/jenkinsfile/)