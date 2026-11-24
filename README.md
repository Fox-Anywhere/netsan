# netsan

Nasconde i dati riservati di configurazioni, log e output CLI di apparati di rete (FortiGate/FortiOS e Cisco IOS/ASA)
prima di darli a un'IA, e rimette i valori reali nella risposta. Lavora sul tuo PC e non usa la rete.

**Download:** pagina [Releases](https://github.com/Fox-Anywhere/netsan/releases). Windows a 64 bit, nessuna installazione.

Questo repository distribuisce i programmi: il codice sorgente non è pubblicato. I file non hanno una firma digitale, quindi
Windows può mostrare un avviso: confronta prima lo SHA-256 con quello di `SHA256SUMS.txt`.

## Uso

Doppio clic su `netsan.exe` per la finestra. Da terminale si usa `netsan-cli.exe`:

```
netsan-cli anon config.conf -p cliente-a -t "Nome Cliente,Nome Sede"   # crea config.anon.conf
netsan-cli restore risposta.txt -p cliente-a                            # crea risposta.restored.txt
netsan-cli anon --clip -p cliente-a --prompt                            # lavora sugli appunti
netsan-cli show -p cliente-a                                            # tabella di corrispondenza
netsan-cli forget -p cliente-a parola                                   # non nascondere più una parola
```

Codici di uscita: 0 tutto bene; 1 errore; 2 un controllo ha fermato il testo o il ripristino non è esatto.

## Limiti da conoscere

- È pseudonimizzazione, non anonimizzazione: la struttura della rete resta leggibile di proposito, e chi ha la mappa torna
  ai valori reali.
- I nomi scelti da persone (oggetti, policy, VPN) e la prosa non si riconoscono con certezza: netsan elenca quelli che trova,
  ma l'ultimo controllo è di chi usa il programma.
- Il file di mappa contiene i valori reali in chiaro. I segreti rimossi non ci sono, tranne una password scritta
  dentro un commento, che resta insieme al commento. Va custodito come la configurazione originale.
- Le sottoreti pubbliche più larghe di /24 e gli intervalli privati a cavallo di più /24 non conservano l'ordine.

## Licenza

Uso gratuito, anche per lavoro: vedi [LICENZA.txt](LICENZA.txt). Componenti di terzi in
[THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt). Contatto: contatti@damicodavide.com
