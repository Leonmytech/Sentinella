# Privacy

Sentinella è progettata per funzionare interamente in locale.

## Cosa raccoglie

- Fotocamera e microfono in uso, per mostrare lo stato di attività.
- Elementi di avvio (`LaunchAgents` e `LaunchDaemons`) per rilevare aggiunte e rimozioni.
- Porte TCP/UDP in ascolto e processo responsabile.
- Cronologia degli eventi generati da questi controlli.

## Dove restano i dati

Tutti i dati restano su questo Mac:

- `~/Library/Application Support/Sentinella/history.store`
- `~/Library/Application Support/Sentinella/launch-baseline.json`

Le preferenze (moduli attivi, notifiche, avvio al login, sezione della dashboard) sono salvate nelle preferenze utente di macOS.

## Cosa non fa

- Non invia dati a server esterni.
- Non richiede un account.
- Non usa il network.
- Non condivide dati con terze parti.

## Cancellare i dati

Da **Impostazioni → Dati e diagnostica** puoi:

- svuotare la cronologia;
- aprire nel Finder la cartella dati;
- rimuovere manualmente l'intera cartella `~/Library/Application Support/Sentinella/`.

## Notifiche

Le notifiche sono generate localmente tramite il framework di sistema e mostrano solo il titolo e il messaggio dell'evento. Puoi disattivarle in qualsiasi momento da **Impostazioni → Notifiche**.
