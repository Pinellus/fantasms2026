# Fanta SMS Engineering

Sito statico della lega di fantacalcio: squadre e rose, calendario, classifiche di Campionato e Coppa, commenti di giornata.
Non serve nessuna installazione: è una sola pagina (`index.html`) con le immagini nella cartella `img/`.

## Pubblicazione su GitHub Pages
1. Crea un repository su GitHub (per esempio `fanta-sms-engineering`) e carica tutti i file di questa cartella.
2. Vai in **Settings → Pages**, scegli **Deploy from a branch**, branch `main` e cartella `/ (root)`, poi **Save**.
3. Dopo un minuto il sito è online su `https://TUO-UTENTE.github.io/NOME-REPOSITORY/`.

## Come si aggiornano i dati
Tutti i dati stanno in un unico blocco `<script id="dati">` in cima a `index.html`. Classifica e statistiche si ricalcolano da soli.

- **Risultato di una partita**: nella partita compila `gc` e `gf` (gol casa e fuori) e `pc` e `pf` (fantapunti casa e fuori). Esempio: `"gc": 2, "gf": 1, "pc": 75.5, "pf": 70`.
- **Commento di giornata**: aggiungi un elemento a `commenti`, con `titolo`, `data` (AAAA-MM-GG), `giornata`, `testo` (elenco di paragrafi) e, se c'è, `video` con `titolo` e `url` (link YouTube).
- **Spareggi in classifica**: l'ordine è in `criteri` (`pt` punti, `dr` differenza reti, `gf` gol fatti, `ptt` punti totali).
- **Rose**: elenco `rosa` di ogni squadra, nel formato [ruolo, nome, club, Q.att., FVMp, pagato]. Le figurine sono in `img/rosa-<squadra>.webp`, nello stesso ordine dell'elenco.

Dati e figurine provengono dall'app di fantacalcio.it.
