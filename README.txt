INTIQAL
Livre de souvenirs personnalisé : on répond à 12 questions, on ajoute des photos,
et on reçoit un livre à offrir à un proche.

Dernière mise à jour de ce fichier : 18 octobre 2026


1. ÉTAT ACTUEL : VERSION DE DÉMONSTRATION
-----------------------------------------
- Site statique (HTML / CSS / JS), pas de serveur, pas de base de données.
- Aucun paiement, aucune commande : la dernière étape du parcours est une simulation,
  annoncée comme telle.
- Les réponses, le prénom, les photos (réduites) et le style restent dans le navigateur
  du visiteur (localStorage). Rien n'est envoyé nulle part.
- Offre affichée : livre relié de 15 pages, 4 styles, 3 à 10 photos,
  à partir de 29 EUR + 4,90 EUR de livraison.
- En ligne : https://intiqal.vercel.app (déployé depuis GitHub deen-tag/intiqal).


2. FICHIERS
-----------
index.html              Accueil
creer.html              Parcours de création (12 questions, photos, style, récapitulatif)
exemple.html            Exemple fictif de livre
mentions-legales.html   Modèle à compléter (voir point 5)
confidentialite.html    Modèle à compléter (voir point 5)
site.css                Styles partagés par toutes les pages
assets/                 Images : hero, book, book-wide, book-spread, intention-flatlay,
                        logo-mark, favicon, favicon-32
README.txt              Ce fichier


3. METTRE À JOUR LE SITE DEPUIS TERMUX
--------------------------------------
Le dépôt est dans ~/intiqal. Après avoir téléchargé les fichiers modifiés dans
Téléchargements :

  cd ~/intiqal
  cp ~/storage/downloads/NOM_DU_FICHIER .
  git add -A
  git commit -m "Description du changement"
  git push

Si on envoie un zip : unzip -o ~/storage/downloads/NOM.zip (dans ~/intiqal), puis
les 3 dernières commandes. Vercel redéploie tout seul en 1 à 2 minutes.


4. OBJECTIF : UN SYSTÈME AUTOMATIQUE
------------------------------------
Ce que doit faire le système final :
  1. Le client finit le parcours : réponses et photos envoyées sur un serveur.
  2. Une IA rédige des textes courts à partir des réponses ; le client les valide.
  3. Le client paie (Stripe).
  4. Le serveur génère le PDF du livre, l'envoie à un service d'impression à la demande
     par API, puis prévient le client par e-mail avec le suivi.

Services d'impression à la demande à étudier (ils impriment et expédient chez le client) :
  - Gelato (impression en France, livres photo, marque blanche)
  - Peecho (API d'impression, expédie au destinataire)
  - Un imprimeur français local pour de petites séries
Ces informations viennent de leurs sites ; les prix ne sont pas vérifiés.

Ordre de travail prévu :
  1. Commander un livre test chez un imprimeur (qualité, prix réel, format de fichier).
  2. Serveur qui reçoit et stocke réponses et photos.
  3. Rédaction par IA + page de validation pour le client.
  4. Génération automatique du PDF.
  5. Paiement (Stripe).
  6. Envoi automatique à l'imprimeur.

Points de vigilance : photos trop floues, textes trop longs qui débordent, adresse
incomplète (prévoir des contrôles avant impression). Le site promet des textes
"retravaillés, jamais réécrits sans validation" : le client doit valider avant impression.
CGV à faire relire : un produit personnalisé n'a en général pas de droit de rétractation.

Question encore ouverte : l'IA rédige tout puis le client corrige, ou elle ne fait que de
légères corrections sur les mots du client ?


5. À FAIRE (par ordre de priorité)
-----------------------------------
[ ] Créer un compte gratuit Gelato et un compte Peecho.
[ ] Relever le prix d'un livre relié de 15 pages livré en France (vérifier que 29 EUR
    laissent une marge) et le format de fichier demandé.
[ ] Commander un livre test.
[ ] Créer le statut pour vendre (micro-entreprise, SIRET).
[ ] Compléter mentions-legales.html et confidentialite.html (champs "[à compléter]" :
    éditeur, statut / SIRET, adresse, e-mail de contact, directeur de la publication).
[ ] Rédiger les CGV avant l'ouverture des commandes.
[ ] Afficher le délai de livraison avant la commande.


6. COÛTS
--------
Gratuit pour l'instant :
  - Site en démo sur Vercel (offre gratuite Hobby).
  - Comptes Gelato / Peecho (on paie seulement à la commande).
  - Stripe : pas d'abonnement, une commission par paiement.
  - Serveur et stockage de photos : des offres gratuites existent pour démarrer.

Dès les premières ventes :
  - Hébergement Vercel : 20 USD/mois (plan Pro). L'offre gratuite Hobby interdit l'usage
    commercial. Un hébergeur gratuit autorisant la vente est une alternative à vérifier.
  - Stripe : environ 1,5 % + 0,25 EUR par paiement carte européenne (de mémoire,
    à confirmer sur le site de Stripe).
  - IA de rédaction : quelques centimes par livre.
  - Impression + expédition : payées à chaque commande, c'est le vrai coût à connaître.
  - Statut micro-entreprise : inscription gratuite, obligatoire avant de vendre.
  - Nom de domaine (optionnel) : environ 10 à 15 EUR/an.

Dépense incompressible : un livre test.
