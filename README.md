# Projet_Python_IGL3
Système de Recherche Documentaire avec Méthodes Basées sur les Matrices
Ce projet implémente un système de recherche documentaire qui compare différentes méthodes pour calculer la similarité entre documents et requêtes : la Méthode Classique, la Décomposition en Valeurs Singulières (SVD) et la Bidiagonalisation + Décomposition QR. Le système traite un ensemble de documents et de requêtes, construit une matrice terme-document, et évalue la pertinence des documents par rapport aux requêtes en utilisant ces méthodes.

Aperçu du Projet
Le notebook Jupyter (projet algo num.ipynb) présente un système de recherche documentaire qui :

Construit une matrice terme-document binaire à partir d'un vocabulaire et d'un ensemble de documents.
Transforme les requêtes textuelles en vecteurs binaires.
Calcule la similarité entre documents et requêtes à l'aide de trois méthodes :
Méthode Classique : Utilise le produit scalaire normalisé (similarité cosinus) sur la matrice terme-document.
Méthode SVD : Applique la décomposition en valeurs singulières pour une analyse sémantique latente, réduisant la dimensionnalité de la matrice (par défaut k=5).
Méthode Bidiag + QR : Utilise la bidiagonalisation suivie d'une SVD et d'une décomposition QR pour une approximation de rang faible alternative.
Visualise les métriques de performance, incluant :
L'erreur de reconstruction pour la SVD en fonction du nombre de valeurs singulières (k).
Le temps d'exécution des trois méthodes en fonction du nombre de documents (Nd).
Traite des fichiers texte externes (documents.txt) pour démontrer une applicabilité réelle.
Prérequis
Pour exécuter le notebook, installez les packages Python suivants :

bash

Réduire

Envelopper

Exécuter

Copier
pip install numpy matplotlib rapidfuzz
Version de Python : 3.13.1 (ou versions compatibles)
Dépendances :
numpy : Pour les opérations matricielles et les calculs numériques.
matplotlib : Pour tracer les graphiques d'erreur de reconstruction et de temps d'exécution.
rapidfuzz : Pour la correspondance floue des chaînes dans le traitement des requêtes.
time : Pour mesurer le temps d'exécution.
Structure des Fichiers
projet algo num.ipynb : Le notebook Jupyter principal contenant l'implémentation et les résultats.
documents.txt : Un fichier texte optionnel contenant des documents (un par ligne) pour tester le système de recherche.
execution_time.png : Image de sortie du graphique de temps d'exécution (générée par le notebook).
Utilisation
Configuration :
Assurez-vous que tous les packages requis sont installés.
Placez le fichier documents.txt dans le même répertoire que le notebook (optionnel pour les tests sur documents externes).
Exécution du Notebook :
Ouvrez projet algo num.ipynb dans Jupyter Notebook ou JupyterLab.
Exécutez toutes les cellules pour lancer les exemples et générer les visualisations.
Le notebook traite trois exemples :
Exemple 1 : Documents mathématiques avec la requête "matrice algèbre".
Exemple 3 : Documents économiques avec les requêtes "dépression croissance" et "bassin fiscalité".
Fichier Externe : Traite documents.txt avec une requête aléatoire basée sur un mot-clé (par exemple, "apple").
Fonctions Principales :
construire_matrice(termes, docs) : Construit une matrice terme-document binaire.
transformer_requete(termes, requete) : Convertit une requête textuelle en vecteur binaire en utilisant la correspondance floue (rapidfuzz).
similarite_classique(matrice, vect_q) : Calcule la similarité cosinus entre la requête et les documents.
similarite_svd(matrice, vect_q, k=5) : Calcule la similarité en utilisant l'analyse sémantique latente basée sur SVD.
similarite_bidiag_qr(matrice, vect_q, k=5) : Calcule la similarité en utilisant la bidiagonalisation et la décomposition QR.
afficher_scores(scores, docs, méthode, seuil=0.0) : Affiche les documents avec des scores de similarité supérieurs à un seuil.
reconstruction_error(matrice, k) : Calcule l'erreur de reconstruction pour la SVD avec k valeurs singulières.
load_documents(file_path) : Charge les documents à partir d'un fichier texte.
extract_keywords(documents) : Extrait les mots-clés uniques des documents.
Sortie :
Sortie Console : Affiche les scores de similarité pour chaque méthode et requête, ainsi que la matrice bidiagonalisée pour l'Exemple 1.
Visualisations :
Un graphique de l'erreur de reconstruction en fonction de k pour la méthode SVD (Exemple 1).
Un graphique du temps d'exécution en fonction du nombre de documents (Nd) pour les trois méthodes.
Résultats du Fichier Externe : Scores de similarité pour une requête aléatoire à partir de documents.txt.
Résultats
Exemple 1 : Documents Mathématiques
Requête : "matrice algèbre"
Documents :
Doc 1 : "Algèbre linéaire et matrices"
Doc 4 : "Matrices et déterminants"
Résultats :
Méthode Classique :
Doc 1 : Score 1.00
Doc 4 : Score 0.50
Méthode SVD :
Doc 1 : Score 0.97
Doc 4 : Score 0.26
Méthode Bidiag + QR :
Doc 4 : Score 0.75
Doc 1 : Score 0.20
Observation : La méthode classique attribue des scores parfaits pour les correspondances exactes, tandis que les méthodes SVD et Bidiag + QR ajustent les scores en fonction des relations sémantiques latentes, Bidiag + QR priorisant Doc 4.
Exemple 3 : Documents Économiques
Requête 1 : "dépression croissance"
Méthode Classique : Doc 1 (Score : 1.00)
Méthode SVD : Doc 1 (Score : 0.97)
Méthode Bidiag + QR : Aucun document pertinent (sous le seuil de 0.5)
Requête 2 : "bassin fiscalité"
Toutes les Méthodes : Doc 2 (Score : 1.00)
Observation : Toutes les méthodes concordent sur les correspondances exactes pour "bassin fiscalité", mais Bidiag + QR est plus conservatrice pour "dépression croissance".
Fichier Externe : documents.txt
Requête : "apple"
Document : "apple banana orange"
Résultats :
Méthode Classique : Doc 2 (Score : 0.58)
Méthode SVD : Doc 2 (Score : 1.00)
Méthode Bidiag + QR : Doc 2 (Score : 1.00)
Observation : Les méthodes SVD et Bidiag + QR attribuent une confiance plus élevée aux correspondances exactes par rapport à la méthode classique.
Visualisations
Graphique de l'Erreur de Reconstruction : Montre que l'erreur diminue lorsque k augmente, indiquant une meilleure approximation de la matrice avec plus de valeurs singulières.
Graphique du Temps d'Exécution : Compare le temps d'exécution des trois méthodes lorsque le nombre de documents (Nd) passe de 5 à 200. La méthode classique est généralement plus rapide pour les petits ensembles de données, tandis que SVD et Bidiag + QR ont des comportements différents en raison de la surcharge des décompositions matricielles.
Remarques
La bibliothèque rapidfuzz est utilisée pour la correspondance floue (seuil > 85) afin de gérer les légères variations dans les termes des requêtes.
La méthode Bidiag + QR utilise une implémentation personnalisée de la bidiagonalisation, ce qui peut introduire des différences numériques par rapport à la SVD standard.
Le graphique de l'erreur de reconstruction aide à évaluer le compromis entre la réduction de dimensionnalité (k) et la précision de l'approximation de la matrice.
Les comparaisons de temps d'exécution sont basées sur des matrices binaires aléatoires, simulant différents nombres de documents.
Limites
Le système suppose une présence binaire des termes (0 ou 1) dans la matrice terme-document, ce qui ne prend pas en compte la fréquence ou l'importance des termes.
La correspondance floue peut introduire des faux positifs pour des termes très similaires.
La méthode Bidiag + QR peut être numériquement moins stable que la SVD pour certaines matrices en raison de son implémentation personnalisée.
Le notebook suppose que documents.txt existe pour les tests sur fichiers externes ; sinon, cette section est ignorée sans erreur.
Améliorations Futures
Intégrer la fréquence des termes (TF-IDF) dans la matrice terme-document pour des scores de similarité plus nuancés.
Optimiser l'algorithme de bidiagonalisation pour une meilleure stabilité numérique et performance.
Ajouter la prise en charge de plusieurs requêtes en mode batch.
Inclure des métriques d'évaluation supplémentaires (par exemple, précision, rappel) pour comparer l'efficacité des méthodes.
Licence
Ce projet est destiné à des fins éducatives et n'inclut pas de licence spécifique. Veuillez contacter l'auteur pour les autorisations d'utilisation.
