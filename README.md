[README.md](https://github.com/user-attachments/files/33736294/README.md)
<p align="center">
  <img src="docs/brand/sentinella-banner.png" alt="Sentinella — Monitoraggio locale per macOS" width="820">
</p>

# Sentinella

**Nome ufficiale:** Sentinella
**Claim:** Monitoraggio locale per macOS. Nessun cloud, nessun account.
**Versione:** 0.1.0 (build 1)

Sentinella è un'app da barra dei menu per macOS che osserva ciò che accade sul tuo Mac e ti avvisa quando qualcosa merita attenzione: fotocamera e microfono, elementi di avvio e porte in ascolto. Tutto avviene in locale: nessun dato viene inviato a servizi esterni.

## Funzioni

- **Attività media** — segnala quando fotocamera o microfono sono in uso.
- **Avvio automatico** — osserva `LaunchAgents` e `LaunchDaemons`, con baseline per distinguere ciò che è nuovo.
- **Porte in ascolto** — elenca le porte TCP/UDP in ascolto e il processo responsabile.
- **Cronologia locale** — eventi filtrabili, ricerca, eliminazione singola o completa.
- **Notifiche di sistema** — avvisi discreti quando viene rilevata un'attività rilevante.
- **Avvio al login** — opzionale, gestito da macOS.
- **Dashboard** — panoramica dello stato, cronologia e impostazioni in un'unica finestra.

## Screenshot

| Dashboard | Barra dei menu |
| --- | --- |
| ![Dashboard di Sentinella](docs/screenshots/dashboard.png) | ![Menu di Sentinella](docs/screenshots/menu-bar.png) |

## Privacy

Sentinella non invia dati a servizi esterni, non richiede un account e non usa il network. Cronologia e baseline restano in `~/Library/Application Support/Sentinella/`. Dettagli in [PRIVACY.md](PRIVACY.md).

## Requisiti

- macOS 14 (Sonoma) o successivo
- Mac Apple Silicon o Intel

## Installazione

1. Sposta `Sentinella.app` in `/Applications`.
2. Al primo avvio, se macOS blocca l'app perché non firmata: clic destro sull'app → **Apri**.
3. Cerca lo scudo di Sentinella nella barra dei menu e apri **Impostazioni** per configurare i moduli.

> Nota: questa build locale non è firmata né notarizzata. Notifiche e avvio al login possono risultare limitati finché l'app non viene firmata con un certificato Apple.

## Sviluppo

Il progetto usa Swift 6, SwiftUI e SwiftData, con target macOS 14.0.

```sh
xcodebuild -project Sentinella.xcodeproj -scheme Sentinella \
  -configuration Debug -destination 'platform=macOS' \
  -derivedDataPath build build CODE_SIGNING_ALLOWED=NO

xcodebuild -project Sentinella.xcodeproj -scheme Sentinella \
  -configuration Debug -destination 'platform=macOS' \
  -derivedDataPath build test CODE_SIGNING_ALLOWED=NO
```

I test coprono `SentinellaKit` (diff di baseline, tipi di evento, store, modelli) e sono eseguiti senza code signing. Lo scheme condiviso disabilita il debugger per il Test action: con LLDB attivo, `xcodebuild test` può bloccarsi durante l'avvio della sessione in ambienti senza GUI.

## Struttura

- `Sentinella/` — app SwiftUI: scene, vista menu bar, dashboard, impostazioni.
- `SentinellaKit/` — logica: monitor, modelli, store e servizi.
- `SentinellaTests/` — test unitari.
- `docs/brand/` — logo, wordmark e banner (SVG + PNG).
- `docs/screenshots/` — screenshot per documentazione e README.

## Logo

Il marchio ufficiale è uno scudo minimale con una fessura di scansione e un punto di segnale. Sorgente vettoriale: [`docs/brand/sentinella-icon.svg`](docs/brand/sentinella-icon.svg).

<p align="left">
  <img src="docs/brand/sentinella-icon.png" alt="Icona di Sentinella" width="96">
</p>

## Limitazioni note

- Su macOS 14 e successivi il monitoraggio delle porte può avere visibilità parziale se l'accesso è limitato dalle impostazioni di sistema.
- Sentinella segnala, non blocca: non impedisce a un'app di usare fotocamera, microfono o rete.
- Il monitoraggio non copre processi eseguiti fuori dalla sessione utente.
- L'avvio al login richiede una build firmata per funzionare in modo affidabile.

## Changelog

Vedi [CHANGELOG.md](CHANGELOG.md).

## Crediti

Sviluppato da Sentinella contributors. © 2026 Sentinella contributors.
