# Tuto — Créer un alias pour une adresse mail Zimbra (OVH)

**Pour qui :** l'administrateur / webmaster.

**Objectif :** faire pointer une adresse supplémentaire (ex. `admin@votre-domaine.org`,
`contact@…`) vers une **boîte existante**, gratuitement.

---

## Comprendre ce qu'est un alias

Un alias (ou **redirection**) est une simple **étiquette** posée sur une boîte
réelle : plusieurs adresses, une seule boîte derrière.

- Il **ne stocke rien** par lui-même → la **boîte de destination doit déjà
  exister**.
- Il est **gratuit** et **illimité** (contrairement à une vraie boîte, facturée).
- Il gère la **réception**. Pour *écrire depuis* l'alias, voir la note en fin de
  tuto.

```
Boîte réelle : prenom.nom@votre-domaine.org   (payante / offerte)
   ├── alias admin@votre-domaine.org     → tombe dans cette boîte
   └── alias contact@votre-domaine.org   → tombe dans cette boîte
```

---

## Prérequis

La **vraie boîte de destination** doit être créée (onglet « Compte email » →
« + Configurer »). Si ce n'est pas fait, voir *Tuto — Créer une adresse mail
pro sur OVH*.

---

## Étapes

1. Manager OVH → **Zimbra Mail** (menu de gauche).
2. Sélectionne ton domaine **`votre-domaine.org`**.
3. Onglet **« Redirections »** (dans la barre d'onglets, à côté de
   « Compte email »).
4. Crée une redirection en renseignant :
   - **Source** : l'adresse-alias à créer, ex. `admin@votre-domaine.org`.
   - **Destination** : une boîte réelle existante
     (ex. `prenom.nom@votre-domaine.org`) — ou directement une adresse Gmail.
5. Valide.

✅ Tout courrier envoyé à l'alias tombe désormais dans la boîte de destination.

---

## Vérifier

Depuis une autre adresse, envoie un mail à l'alias (`admin@votre-domaine.org`).
Il doit arriver dans la boîte de destination. Si tu rediriges vers un Gmail et
que le premier message atterrit en spam, marque-le **« Non spam »** une fois.

---

## Écrire *depuis* l'alias (optionnel)

La réception par alias est **automatique**. Mais pour **envoyer** sous l'alias
(ex. répondre en tant que `admin@votre-domaine.org` depuis Gmail), il faut
l'ajouter séparément en **« Envoyer en tant que »** dans Gmail — même procédure
que pour une boîte normale (voir *Tuto — Envoyer en tant que depuis Gmail*),
en utilisant les identifiants de la **boîte de destination**.

---

## Bonnes pratiques

- Réserve les **vraies boîtes** aux personnes (lecture/stockage propre) et mets
  toutes les **adresses de fonction** (`admin@`, `contact@`, `devis@`…) en
  **alias** → tu couvres beaucoup d'adresses pour le prix de quelques boîtes.
- Fais converger plusieurs alias vers une même **boîte pivot** pour centraliser
  le courrier de rôle.
- Un alias se **supprime ou se re-dirige** à tout moment, sans impact sur les
  mails de la boîte de destination.
