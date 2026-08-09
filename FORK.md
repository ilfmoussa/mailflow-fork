# MailFlow Fork — Tags IMAP & Unified Inbox

Fork de [MailFlow v2.8.0](https://github.com/maathimself/mailflow) par [@fifounet75](https://github.com/fifounet75).

Ce fork ajoute l'affichage et le filtrage des **tags IMAP (keywords/flags custom)** poses par des outils externes (ex: mail-classifier), ainsi que des ameliorations visuelles pour la boite unifiee.

## Changements par rapport a upstream

### Backend

- **`GET /api/mail/tags`** : nouvel endpoint qui retourne les tags custom presents sur les messages (exclut les flags systeme `\Seen`, `\Flagged`, `$Junk`, etc.)
- **`GET /api/mail/messages?tag=...`** : filtre les messages par tag via containment JSONB (`flags @> $tag::jsonb`)

### Frontend

- **Sidebar — section Tags** : section depliable entre les favoris et les dossiers. Chaque tag est cliquable pour filtrer la liste de messages. Re-fetch automatique au changement de compte.
- **Store** : nouveaux champs `selectedTag`, `availableTags`, action `fetchTags`
- **MessageList** : le filtre `tag` est passe a l'API dans tous les chemins de chargement (initial, pagination, refresh background)
- **Unified inbox — couleur de compte** : barre d'accent laterale (3px) coloree par compte dans la vue unifiee
- **Unread styling** : remplacement du point non-lu par un fond teinte (`color-mix()`) + graisse sur date/sujet/snippet. Le fond change reactively quand un email est marque lu.

## Utilisation avec mail-classifier

Ce fork est concu pour fonctionner avec [mail-classifier](https://github.com/fifounet75/mail-classifier), qui pose des tags IMAP sur les emails via des regles IA ou techniques. Les tags apparaissent automatiquement dans la sidebar de MailFlow.

## Installation

```bash
git clone https://github.com/fifounet75/mailflow-fork.git /opt/mailflow-fork
cd /opt/mailflow-fork
cp .env.example .env
nano .env  # configurer APP_URL, SESSION_SECRET, DB_PASSWORD, ENCRYPTION_KEY
docker compose up -d --build
```

## Licence

Meme licence que MailFlow upstream : [AGPL-3.0](LICENSE).
