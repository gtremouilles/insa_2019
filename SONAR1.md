<center><img src="images/sonarqube.png" alt="Sonarqube" width="300"/></center>

# Quality Profiles
But : Ajouter un nouveau profil "**Java**" qui est une copie du profil "**Sonar Way**" mais qui contient des règles en moins.   

- Ouvrir le menu "**Quality profiles**"  
- Filtrer sur le profil "**Java**"   
- Faire une copie du profil "**Sonar way**" et la nommer "**Petclinic**"

<center><img src="images/sonar3.png" alt="Sonarqube" width="1042"/></center>

- Afficher la liste des règles de type "**Bugs**"
- Désactiver la règle que vous avez utilisé dans le TP précedent

<center><img src="images/sonar4.png" alt="Sonarqube" width="1042"/></center>

- Définir ce nouveau profil Java comme profil par défaut
- Relancer une analyse Sonar
- Vérifier que le bon "Quality profil" a été utilisé :
<center><img src="images/sonar7.png" alt="Sonarqube" width="130"/></center>
- Que se passe-t-il au niveau du nombre de bugs ?


# Quality Gates
But : Ajouter une condition pour faire échouer le résultat de l'analyse Sonar.   
- Ouvrir le menu "**Quality Gates**"  
- Créer une nouvelle "**Quality Gate**" et la nommer "**Petclinic**"  
- La positionner par défaut
- Ajouter une condition avec la métrique "**Reliability/Bugs**" et positionner la valeur "**Error**" à 3  
- Relancer une analyse Sonar  
- Vérifier que l'analyse est en bien à l'état "**Failed**"

<center><img src="images/sonar5.png" alt="Sonarqube" width="300"/></center>
- Vérifier que le bon "**Quality gate**" a été utilisé :
<center><img src="images/sonar6.png" alt="Sonarqube" width="130"/></center>

