# Tuto — Créer une adresse mail pro à bas coût sur OVH (avec gestion anti-spam)

**Pour qui :** l'administrateur / webmaster.

**Objectif :** créer une vraie boîte aux lettres professionnelle sur un domaine
OVH existant, et garantir que ses envois ne tombent pas en spam grâce au trio
**SPF + DKIM + DMARC**.

**Prérequis :** un nom de domaine géré chez OVH (ex. `votre-domaine.org`), avec
sa zone DNS chez OVH.

---

## Principe et coût

OVH facture l'e-mail **à la boîte**, pas au forfait — inutile d'acheter un
« pack ».

| Élément | Coût |
|---|---|
| 1ʳᵉ boîte Zimbra Starter (15 Go) | **offerte** tant que le domaine est chez OVH |
| Chaque boîte Starter suivante | **~0,30 € HT/mois** (0,36 € TTC) |
| Alias / redirection | **gratuit**, illimité (voir tuto dédié) |

> On reste sur **Starter** : pour de l'e-mail branché dans Gmail, les offres Pro
> (ActiveSync) / Business (bureautique) n'apportent rien.

---

## Étape 1 — Créer la boîte

1. Manager OVH → **Zimbra Mail** → onglet **« Compte email »**.
   *(Si le service Zimbra n'existe pas encore sur ce domaine, suivre d'abord
   l'assistant « Ajouter une organisation » → rattacher le domaine.)*
2. Clique **« + Configurer »** (pas « Commander », réservé aux achats de boîtes
   payantes).
3. Renseigne :
   - **Partie locale** de l'adresse (avant le `@`). **Conseil :** choisis un nom
     **stable** (ex. `prenom.nom`) plutôt qu'un rôle (`admin`, `contact`) —
     le nom de boîte est difficile à changer ensuite ; les rôles se gèrent en
     **alias**.
   - **Mot de passe** (à transmettre à l'utilisateur de façon sécurisée).
   - **Offre : `Starter`**.
4. Valide. La boîte apparaît en statut **Actif**.

---

## Étape 2 — Vérifier que la zone est prête à recevoir

Depuis un terminal :

```bash
# Serveurs mail (doit renvoyer les mx*.mail.ovh.net)
dig +short votre-domaine.org MX

# SPF (doit contenir v=spf1 include:mx.ovh.com ~all)
dig +short votre-domaine.org TXT
```

Si les MX et le SPF répondent, la boîte peut **recevoir**. (OVH les pose
automatiquement.)

---

## Étape 3 — L'authentification anti-spam (le cœur du tuto)

Trois enregistrements travaillent ensemble pour que tes mails soient **acceptés**
plutôt que classés en spam.

### SPF — déjà en place (auto)
`v=spf1 include:mx.ovh.com ~all` — autorise les serveurs OVH à envoyer pour ton
domaine. Rien à faire.

### DKIM — déjà en place (auto)
OVH publie deux sélecteurs en CNAME et maintient les clés lui-même. Vérifier :

```bash
dig +short ovhmo-selector-1._domainkey.votre-domaine.org
```

Doit renvoyer un CNAME vers `…dkim.mail.ovh.net`. Si c'est vide, vérifier dans
la zone DNS que les lignes `ovhmo-selector-1._domainkey` et
`ovhmo-selector-2._domainkey` existent (sinon activer DKIM côté service Zimbra).

### DMARC — à créer à la main
C'est le maillon manquant par défaut, et le principal responsable des passages
en spam d'un domaine neuf.

1. OVH → **Noms de domaine → `votre-domaine.org` → Zone DNS** →
   **« Ajouter une entrée »** → type **DMARC** (formulaire guidé).
2. Renseigner **seulement** :
   - **Sous-domaine** : `_dmarc` (déjà pré-rempli).
   - **Règle pour le domaine** (= `p`) : **`none`**.
   - **URI de création de rapports globaux** (= `rua`) :
     **`mailto:prenom.nom@votre-domaine.org`**
   - Laisser le reste par défaut.

> ⚠️ **Piège classique :** l'adresse de rapport doit être une **URI mailto**.
> Il faut écrire `mailto:adresse@domaine`, **pas** l'adresse seule. Sans le
> préfixe `mailto:`, OVH refuse l'entrée.

3. Vérifier l'**aperçu** en bas :
   ```
   v=DMARC1; p=none; rua=mailto:prenom.nom@votre-domaine.org; aspf=r
   ```
   puis **Ajouter**.

4. Confirmer après propagation :
   ```bash
   dig +short _dmarc.votre-domaine.org TXT
   ```

### Durcir le DMARC plus tard
Démarrer en `p=none` (observation seule, ne bloque rien). Après quelques semaines
d'observation sans faux positif :
```
p=none   →   p=quarantine   →   p=reject
```

---

## Étape 4 — Mesurer la délivrabilité

Envoyer un mail (depuis Gmail, en « De » = l'adresse pro) vers l'adresse jetable
fournie par **mail-tester.com**, puis lire la note /10 et le détail
SPF/DKIM/DMARC.

> Écrire un **vrai contenu** (objet + quelques phrases). Un message vide fait
> chuter le score pour des raisons de contenu, **pas** d'authentification.
> Un domaine neuf a peu de réputation au départ : marquer « Non spam » les
> premiers mails accélère la mise en confiance.

---

## Rappel important

- Le **nom de boîte** est pénible à changer → le choisir stable du premier coup.
- Les **adresses de rôle** (`admin@`, `contact@`…) se font en **alias gratuits**
  (voir *Tuto — Créer un alias*), pas en boîtes payantes.
- Chaque domaine a **ses propres** SPF/DKIM/DMARC : refaire l'étape 3 sur chaque
  nouveau domaine.
