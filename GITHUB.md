# Récupération du projet de test
- Récupération du projet petclinic via un fork : https://github.com/spring-petclinic/spring-framework-petclinic
- Dans les settings > Options > cocher Issues pour pouvoir créer des tickets sur le fork
- Créer une branche develop depuis la branche master
- Dans Settings > Branches, indiquer que la branche develop est la branche principale

# Un peu de suivi de projet
- Dans Issues > Milestones, créer une nouvelle milestone "TP Git"
- Créer une nouvelle issue "exo 1"
- S'affecter cette nouvelle issue
- Lui donner un label documentation
- Créer deux issues "exo 2" et "exo 2 bis"
- Affecter les 3 issues à la milestone "TP Git"

# Ajout d'une fonctionnalité
- Créer une branche feature/exo1 depuis la branche develop
- Dans la branche feature/exo1, modifier le fichier Readme.MD et ajouter le texte "# TP INSA" en début de fichier
- Lors du commit, s'assurer que la branche sélectionnée est bien "feature/exo1" et ajouter un lien avec l'issue associée. Pour cela la référencer dans le message de commit avec "#ID_ISSUE"
- Créer une nouvelle Pull Request : * Bien spécifier les branches de destination et d'origine !* : 
  - destination : bien choisir son projet et la branche develop
  - origine : la branche feature/exo1
  - Préfixer le commentaire par la mention "Fixes #ID_ISSUE"
- Inspecter la Pull Request et la valider avec un commentaire particulier
  - Accepter la fusion (attention à ne pas cloturer la Pull Request)
- Regarder le contenu des branches develop, master et feature
- Regarder le statut de l'issue associée

# Un petit conflit
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

# Quelques livraisons
- Créer une branche release depuis la branche develop
- Un bug a été détecté durant la recette, le corriger sur la branche release en ajoutant le texte "fix release" dans le Readme.md.
- [facultatif] En même temps un bug en production a été détecté...
  - depuis la branche master, créer une branche hotfix1
  - sur cette nouvelle branche, modifier le Readme.md pour ajouter "hotfix prod"
  - fusionner la branche hotfix sur la master
 - Fusionner la branche release avec la branche master (gérer un éventuel conflit...)
 - Créer un tag sur la master pour marquer la mise en production
 - Faire une comparaison entre la branche develop et la branche master
 - Et enfin, on resynchronise la branche develop avec la nouvelle version de la master (permet de se mettre à jour des derniers hotfix et bug fixes de release)
 
