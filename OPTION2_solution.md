<center><img src="images/jenkins.png" alt="Jenkins" width="300"/></center>

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
                    sh 'mvn clean package'  
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
> Pour plus d'informations sur la construction du Jenkinsfile, aller à l'adresse suivante : [https://jenkins.io/doc/book/pipeline/jenkinsfile/](https://jenkins.io/doc/book/pipeline/jenkinsfile/)

## Création de l'item Petclinic_pipeline
- Description : cet item va récupérer automatiquement le Jenkinsfile à la racine du projet et va permettre de lancer les différentes tâches pour le déploiement.
- Nom : Petclinic_deployQualification
- Type : Pipeline

<img src="images/option2_sol2.png" alt="Jenkins" width="1042"/>

- Déclarer un pipeline avec la définition "**Pipeline script from SCM**"  
- Choisir le SCM "**Git**" et renseigner les informations du repository
<img src="images/option2_sol1.png" alt="Jenkins" width="1042"/>

- Ouvrir le pipeline avec "**Open Blue Ocean**"

<center><img src="images/jenkins6.png" alt="Jenkins" width="200"/></center>

 - Lancer le build  
 
<center><img src="images/jenkins7.png" alt="Jenkins" width="300"/></center>

 - Build en cours de construction :  

<center><img src="images/jenkins8.png" alt="Jenkins" width="1042"/></center>

 - Fin de la construction :  

<center><img src="images/jenkins9.png" alt="Jenkins" width="1042"/></center>

