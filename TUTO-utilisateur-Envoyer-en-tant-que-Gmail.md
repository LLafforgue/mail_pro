# Tuto — Envoyer un mail *en tant que* ton adresse pro depuis Gmail

**Pour qui :** tout membre de l'équipe disposant d'une adresse professionnelle
(ex. `prenom.nom@votre-domaine.org`) et voulant l'utiliser depuis son **Gmail
habituel**.

**Objectif :** quand tu écris depuis ton Gmail, que le destinataire voie
`prenom.nom@votre-domaine.org` comme expéditeur (et non ton `@gmail.com`).

**Durée :** 5 minutes, à faire **une seule fois**.

---

## Avant de commencer

Demande ces informations à ton administrateur :

| Information | À remplir |
|---|---|
| Ton adresse pro | `............................@votre-domaine.org` |
| Le mot de passe de cette boîte | `............................` |
| L'accès webmail | `https://zimbra1.mail.ovh.net` |

> Ce mot de passe est celui de ta **boîte pro**. Il n'a rien à voir avec ton mot
> de passe Google.

---

## Étapes (sur Gmail version ordinateur)

1. Gmail → roue dentée en haut à droite → **« Voir tous les paramètres »**.
2. Onglet **« Comptes et importation »**.
3. Ligne **« Envoyer des e-mails en tant que »** → clique
   **« Ajouter une autre adresse e-mail »**.
4. Renseigne :
   - **Nom** : ce qui s'affichera (ex. `Prénom Nom`).
   - **Adresse e-mail** : ton adresse pro.
   - **Décoche** « Traiter comme un alias ».
5. Écran suivant — serveur d'envoi (SMTP) :

   | Champ | Valeur |
   |---|---|
   | Serveur SMTP | `ssl0.ovh.net` |
   | Port | `465` (si refus, essaie `587`) |
   | Sécurité | SSL (ou TLS sur le port 587) |
   | Nom d'utilisateur | ton adresse pro **complète** |
   | Mot de passe | celui de ta boîte pro |

6. Gmail envoie un **code de confirmation** à ta boîte pro. Pour le lire :
   connecte-toi au **webmail** `https://zimbra1.mail.ovh.net` (avec ton adresse
   pro + son mot de passe), ouvre le message de Google, récupère le lien/code et
   valide dans la fenêtre Gmail.

✅ C'est fait : ton adresse pro est désormais disponible comme expéditeur.

---

## Envoyer un mail au quotidien (le geste à retenir)

Quand tu rédiges un message, une ligne **« De »** apparaît sous le destinataire.

> ⚠️ Gmail garde **ton `@gmail.com` par défaut**. Pour écrire sous ton adresse
> pro, clique sur **« De »** et choisis **`prenom.nom@votre-domaine.org`**
> à chaque message.

---

## Problèmes fréquents

| Symptôme | Cause | Solution |
|---|---|---|
| Pas de ligne « De » à la rédaction | Adresse pas encore confirmée | Reclique le lien de confirmation reçu dans le webmail (étape 6) |
| Le destinataire voit mon `@gmail.com` | Champ « De » resté sur Gmail | Clique « De » → choisis l'adresse pro avant d'envoyer |
| Gmail refuse le mot de passe | Espace parasite / mauvais mot de passe | Ressaisis sans espace ; c'est le mot de passe **de la boîte pro** |
| Le port 465 ne passe pas | Réseau bloquant ce port | Utilise `587` en TLS |
| Mon mail part en spam chez le destinataire | Message vide/trop court, ou domaine récent | Écris un vrai contenu ; ça s'améliore avec l'usage |

---

## Besoin d'aide ?

Contacte ton **administrateur** : lui seul peut réinitialiser le mot de passe de
ta boîte ou créer de nouvelles adresses.
