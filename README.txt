INTIQAL
Livre de souvenirs personnalisé : on répond à 12 questions, on ajoute des photos,
et on reçoit un livre à offrir à un proche.

Dernière mise à jour de ce fichier : 18 octobre 2026 (ajout de l'écriture des textes par IA)


1. ÉTAT ACTUEL : VERSION DE DÉMONSTRATION
-----------------------------------------
- Site statique (HTML / CSS / JS), pas de serveur, pas de base de données.
- Aucun paiement, aucune commande : la dernière étape du parcours est une simulation,
  annoncée comme telle.
- Les réponses, le prénom, les photos (réduites), le style et les textes écrits restent dans
  le navigateur du visiteur (localStorage).
- Seule exception : si le visiteur clique sur "Écrire les textes de mon livre" (étape 5),
  son prénom, le lien et ses réponses écrites (jamais les photos) sont envoyés à l'IA
  (Google Gemini, offre gratuite) via api/ecrire.js. Rien n'est enregistré sur le serveur.
  Attention : avec l'offre gratuite, Google peut réutiliser ces textes. Démo uniquement.
- Offre affichée : livre relié de 15 pages, 4 styles, 3 à 10 photos,
  à partir de 29 EUR + 4,90 EUR de livraison.
- En ligne : https://intiqal.vercel.app (déployé depuis GitHub deen-tag/intiqal).


2. FICHIERS
-----------
index.html              Accueil
creer.html              Parcours de création (12 questions, photos, style, récapitulatif)
exemple.html            Exemple fictif de livre
api/ecrire.js           Fonction serveur Vercel : demande à l'IA d'écrire les textes du livre
vercel.json             Durée maximale de la fonction (30 s)
mentions-legales.html   Modèle à compléter (voir point 6)
confidentialite.html    Modèle à compléter (voir point 6)
site.css                Styles partagés par toutes les pages
assets/                 Images : hero, book, book-wide, book-spread, intention-flatlay,
                        logo-mark, favicon, favicon-32
README.txt              Ce fichier


3. METTRE EN MARCHE L'ÉCRITURE PAR IA (une seule fois)
-----------------------------------------------------
Sans clé, le bouton affiche : "L'écriture automatique n'est pas encore activée".
  1. Créer une clé gratuite : aistudio.google.com > se connecter > "Get API key" > créer
     une clé > la copier. (Ne jamais la mettre dans un fichier du site ni la partager.)
  2. Vercel > projet intiqal > Settings > Environment Variables : ajouter
       Name  = GEMINI_API_KEY
       Value = la clé copiée
     puis enregistrer. (Les intitulés peuvent varier légèrement.)
  3. Pousser les fichiers (point 4) ou, si c'est déjà fait : Deployments > Redeploy.
     Une variable d'environnement ne compte que pour les déploiements faits après son ajout.
  4. Tester : intiqal.vercel.app/creer.html > répondre à quelques questions > aller jusqu'à
     l'étape 5 > "Écrire les textes de mon livre".
Options : GEMINI_MODEL (défaut gemini-2.5-flash), ALLOWED_ORIGINS (autres adresses autorisées).
Limites : 15 demandes par heure et par visiteur (approximatif). Le quota gratuit de Google
est limité ; tout visiteur peut le consommer. Pour de vrais clients, passer à un service
payant ou hébergé en Europe en remplaçant seulement la fonction callModel() de api/ecrire.js.


4. METTRE À JOUR LE SITE DEPUIS TERMUX
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


5. OBJECTIF : UN SYSTÈME AUTOMATIQUE
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

Ordre de travail prévu (l'étape 3 est faite en version de démonstration) :
  1. Commander un livre test chez un imprimeur (qualité, prix réel, format de fichier).
  2. Serveur qui reçoit et stocke réponses et photos.
  3. Rédaction par IA + validation/correction par le client (FAIT en démo : étape 5 du parcours).
  4. Génération automatique du PDF.
  5. Paiement (Stripe).
  6. Envoi automatique à l'imprimeur.

Points de vigilance : photos trop floues, textes trop longs qui débordent, adresse
incomplète (prévoir des contrôles avant impression). Le site promet des textes
"retravaillés, jamais réécrits sans validation" : le client doit valider avant impression.
CGV à faire relire : un produit personnalisé n'a en général pas de droit de rétractation.

Choix actuel : l'IA rédige une page par souvenir à partir des réponses, sans rien inventer,
et le client peut tout corriger. À ajuster selon les tests (ton, longueur).


6. À FAIRE (par ordre de priorité)
-----------------------------------
[ ] Créer la clé Google AI Studio et l'ajouter dans Vercel (point 3), puis tester l'écriture.
[ ] Créer un compte gratuit Gelato et un compte Peecho.
[ ] Relever le prix d'un livre relié de 15 pages livré en France (vérifier que 29 EUR
    laissent une marge) et le format de fichier demandé.
[ ] Commander un livre test.
[ ] Créer le statut pour vendre (micro-entreprise, SIRET).
[ ] Compléter mentions-legales.html et confidentialite.html (champs "[à compléter]" :
    éditeur, statut / SIRET, adresse, e-mail de contact, directeur de la publication).
[ ] Rédiger les CGV avant l'ouverture des commandes.
[ ] Afficher le délai de livraison avant la commande.


7. COÛTS
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
