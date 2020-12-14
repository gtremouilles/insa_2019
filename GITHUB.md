# Récupération du projet de test
- Récupération du projet petclinic via un fork : https://github.com/spring-petclinic/spring-framework-petclinic
- Dans les settings > Options > cocher Issues pour pouvoir créer des tickets sur le fork
- Créer une branche develop depuis la branche master


# Ajout d'une fonctionnalité
- Créer une branche feature/exo1 depuis la branche develop
- Créer une nouvelle issue "exo 1"
- S'affecter cette nouvelle issue
- Lui donner un label documentation
- Dans la branche feature/exo1, modifier le fichier Readme.MD et ajouter le texte "# TP INSA" en début de fichier
- Lors du commit, s'assurer que la branche sélectionnée est bien "feature/exo1" et ajouter un lien avec l'issue associée. Pour cela la référencer dans le message de commit avec "#ID_ISSUE"
- Créer une nouvelle Pull Request : * Bien spécifier les branches de destination et d'origine !* : 
  - destination : bien choisir son projet et la branche develop
  - origine : la branche feature/exo1
- Inspecter la Pull Request et la valider avec un commentaire particulier
  - Préfixer le commentaire par la mention "Fixes #ID_ISSUE"
  - Accepter la fusion (attention à ne pas cloturer la Pull Request)
- Regarder le contenu des branches develop, master et feature
- Regarder le statut de l'issue associée

# Un petit conflit
- Créer deux issues "Exo2" et "Exo2bis"
- Depuis la branche develop éditer le fichier Readme.MD et ajouter le texte "Exo2"
- Sauvegarder les modification mais indiquer qu'on vise une nouvelle branche (feature/exo2) et pas la branche develop
- Cela crée automatiquement une Pull Request qu'on ne valide pas pour le moment
- Depuis la branche develop éditer de nouveay le fichier Readme.MD et ajouter le texte "Exo2bis"
- Sauvegarder les modification mais indiquer qu'on vise une nouvelle branche (feature/exo2bis) et pas la branche develop
- Valider une des deux Pull Request (en profiter pour cloturer l'issue associée)
- Essayer de valider la seconde et constater le conflit
- Résoudre le conflit
- Revenir sur la Pull Request et expliquer le nombre de commits
- Valider la Pull Request (en profiter pour cloturer l'issue associée)
