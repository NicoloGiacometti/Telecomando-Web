# Telecomando LG (web)

Telecomando per TV LG webOS che gira interamente nel browser del telefono: nessun server, nessun PC acceso.
Il telefono parla direttamente con la TV sulla rete di casa (WebSocket sicuro, porta 3001).

## Primo utilizzo
1. Telefono e TV sullo stesso Wi-Fi, TV accesa.
2. Apri la pagina: cerca la TV da sola.
3. La prima volta dice "TV non trovata": tocca **Primo collegamento**, nella pagina di avviso scegli
   *Avanzate → Procedi*, poi torna indietro. La ricerca riparte da sola.
4. Sulla TV compare una richiesta: accettala con il telecomando fisico. Da lì in poi si collega da solo.
5. Dal menu del browser: *Aggiungi a schermata Home* per averla come un'app.

## Ricerca automatica
Un browser non può fare una scansione della rete come un programma sul PC, quindi la pagina cerca la TV
per **nome**: il router di casa la registra come `LGwebOSTV` (con il router TIM:
`lgwebostv.homenet.telecomitalia.it`). Il nome resta lo stesso anche quando l'IP cambia.
Se il tuo router usa un altro nome, inseriscilo in *Inserisci nome o IP a mano*.

## Limiti (dovuti al browser)
- Non può accendere la TV (serve Wake-on-LAN, che un browser non può inviare).
- Solo TV LG: Panasonic e Fire TV non accettano comandi da una pagina web.
- Il telefono deve usare il DNS del router (se in Android è attivo un "DNS privato" fisso, il nome della TV non si trova).

## Come funziona
`index.html` carica `app.html` in un iframe isolato (`sandbox` senza `allow-same-origin`).
La TV ignora le connessioni da un sito web ma accetta quelle con origine `null`, che è l'origine dell'iframe isolato.
Nome della TV e chiave di pairing restano solo nel browser del telefono (localStorage della pagina esterna).
