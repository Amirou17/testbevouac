# testbevouac
L’API https://www.emploi-store-dev.fr/portail-developpeur-cms/home/catalogue- des-api/documentation-des-api/api/api-la-bonne-boite-v1.html  Permet de récupérer une liste d’entreprises susceptibles de recruter, par ville et par secteur d’activité. Cette API permet à Bevouac d’estimer le dynamisme économique d’une zone géographique. Mais également de cibler le marketing digital en adaptant nos campagnes publicitaires en fonction des professions exercées localement.

Guide du Test :

1)Cloner le projet, lien git selon le module que vous souhaitez tester,
2)Ouvrir le projet dans un éditeur de texte (phpStorm, Xcode, Visual Studio Code, ...),
3)Générer un token dans dans le terminal de l'éditeur de texte,

  curl -X POST https://entreprise.pole-emploi.fr/connexion/oauth2/access_token?realm=%2Fpartenaire -d "grant_type=client_credentials&client_id=PAR_labonneboite_0e637e879694d9e34b0ed11f466262de9b25ec7d9807819f962c78e03573e092&client_secret=2f55ff53e35d0b345890634069ac3e5c56f0030b2e166ccec0c403f7f3ed9fa0&scope=application_PAR_labonneboite_0e637e879694d9e34b0ed11f466262de9b25ec7d9807819f962c78e03573e092%20api_labonneboitev1" 
  
4)Copier le token et coller-le à la place de l'ancien (le texte barré en rouge). Exemple : Ligne 25 dans 
src/components/Module1.vue,  : 'Authorization' : 'Bearer soBIFIOujn02VfgcDOCGtEZpt4I'
5)Lancer le server dans le terminal (yarn serve)
6)Cliquer sur le lien généré depuis le terminal (ça devrait normalement ouvrir votre navigateur par défaut)
