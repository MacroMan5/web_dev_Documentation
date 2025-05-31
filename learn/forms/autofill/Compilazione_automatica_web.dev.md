# Compilazione automatica  |  web.dev

**Source URL:** [https://web.dev/learn/forms/autofill?hl=it](https://web.dev/learn/forms/autofill?hl=it)  
**Last Updated:** 2025-05-23T01:33:37.248Z  
**Extracted:** 2025-05-31 16:58:10

---

# Compilazione automatica  |  web.dev

Dover reinserire l'indirizzo per la decima volta è faticoso. Browser e tu, in qualità di sviluppatore, può aiutare gli utenti a inserire i dati più velocemente ed evitare di reinserirli. Questo modulo insegna come funziona la compilazione automatica, come `autocomplete` e altre possono garantire che i browser offrano opzioni di compilazione automatica appropriate.

## Come funziona la compilazione automatica?

Nell'[introduzione alla compilazione automatica](https://web.dev/learn/forms/auto?hl=it) hai già appreso le nozioni di base la compilazione automatica. Perché i browser offrono la compilazione automatica?

La compilazione di moduli non è un'attività interessante, ma è comunque un'attività da svolgere spesso. Con il passare del tempo compili molti moduli e spesso inserisci gli stessi dati. Un modo per aiutare gli utenti a compilare più velocemente i moduli è offrire loro la possibilità di compilare automaticamente i campi dei moduli con i dati precedentemente inseriti. Si tratta di compilazione automatica.

Come fanno i browser a sapere quali dati compilare automaticamente? Dai un'occhiata a un modulo di esempio campo per scoprirlo.

```
<label for="name">Name</label>
<input name="name" id="name">
```

Se invii questo campo del modulo, i browser memorizzano il valore (i dati inseriti) insieme al valore dell'attributo `name` (nome). Alcuni browser esaminano anche l'attributo `id` durante l'archiviazione e la compilazione dei dati.

Supponiamo che settimane dopo compili un altro modulo su un altro sito web. Questo sito include inoltre contiene un campo del modulo con `name="name"`. Ora il browser può offrire la compilazione automatica, perché esiste già un valore per il nome.

La compilazione automatica è particolarmente utile nei moduli che utilizzi regolarmente, ad esempio i moduli di registrazione accesso, pagamento, pagamento e moduli in cui devi inserire il tuo nome o .

Puoi aiutare i browser a offrire le migliori opzioni di compilazione automatica usando valori per l'attributo `autocomplete`. Esistono molti valori possibili per `autocomplete`. Ecco un esempio di indirizzi.

  CodePen Embed - Learn forms – autocomplete address  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Nel tuo browser è già salvato un indirizzo? Bene. Dopo interagisci con il primo campo del modulo dell'indirizzo, il browser mostra un elenco di indirizzi salvati. Puoi sceglierne una e il browser compila tutti i campi correlati all'indirizzo. Compilazione automatica dei moduli è semplice e veloce.

Non tutti i moduli di indirizzo contengono gli stessi campi e anche l'ordine dei campi varia. L'utilizzo dei valori corretti per `autocomplete` garantisce che il browser compili i valori corretti per un modulo. Esistono valori per `country`, `postal-code`, e [molti altro ancora](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values).

## Assicurati che gli utenti possano accedere rapidamente e utilizzare password sicure

Molte persone non sanno ricordare le password. Il metodo [più comune password](https://en.wikipedia.org/wiki/List_of_the_most_common_passwords) è "123456", seguito da altre combinazioni facili da ricordare. Come puoi utilizzare password sicure e univoche senza memorizzarle tutte?

I browser dispongono di gestori delle password integrati per generare, salvare e compilare password per te. Scopri come aiutare i browser con la compilazione automatica delle email e la gestione delle password.

  CodePen Embed - Learn forms – autocomplete sign-up  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Puoi utilizzare `autocomplete="email"` per un campo email, in modo che gli utenti ricevano la compilazione automatica per un indirizzo email.

Poiché si tratta di un modulo di registrazione, gli utenti non dovrebbero avere la possibilità di compilarlo in precedenza le password usate. Puoi utilizzare `autocomplete="new-password"` per assicurarti che i browser offrono la possibilità di generare una nuova password.

Nel modulo di accesso, puoi usare `autocomplete="current-password"` per comunicare browser per offrire la possibilità di inserire le password salvate in precedenza per questo sito web.

Puoi configurare l'autenticazione a due fattori su molti siti web. Oltre alla sezione una password, viene inviato un codice monouso tramite SMS o un'app di autenticazione a due fattori.

Non sarebbe fantastico se ti venisse suggerito il codice che hai ricevuto nell'SMS con la tastiera sullo schermo e puoi selezionarla direttamente per compilare ? Su Safari 14 o versioni successive, puoi utilizzare [`autocomplete="one-time-code"`](https://developer.apple.com/documentation/security/password_autofill/enabling_password_autofill_on_an_html_input_element) per raggiungere questo obiettivo. In Chrome su Android, puoi utilizzare lo strumento [WebOTP API](https://developer.chrome.com/docs/identity/web-apis/web-otp?hl=it) per ottenere usando JavaScript.

Scopri di più su come verificare i numeri di telefono sul web con il [modulo OTP via SMS best practice](https://web.dev/articles/sms-otp-form?hl=it).

## Aiuta gli utenti a inserire i dati della carta di credito

Su molti siti web di e-commerce, puoi utilizzare la carta di credito per acquistare prodotti. I siti possono utilizzare piattaforme di pagamento di terze parti che forniscono i propri moduli, ma se devi creare le tue forme di pagamento, assicurati che gli utenti possano compilare dati di pagamento.

Puoi utilizzare nuovamente l'attributo `autocomplete` per assicurarti che i browser offrano l'attributo le opzioni di compilazione automatica corrette.

Esistono valori per il numero della carta di credito `cc-number`, la scadenza della carta di credito data `cc-exp` e [tutte le altre informazioni necessaria](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) per un pagamento con carta di credito.

Utilizza un'unica immissione per numeri come numeri di carte di credito e numeri di telefono numeri, per assicurarti che i browser offrano la compilazione automatica. Utilizza elementi di modulo standard, ad esempio, un `<select>` per le date delle carte di pagamento, anziché gli elementi personalizzati, per per assicurarsi che il completamento automatico sia disponibile.

Scopri di più su come [aiutare gli utenti a evitare di inserire nuovamente il pagamento i tuoi dati](https://web.dev/learn/forms/payment?hl=it#help_users_enter_their_payment_details).

## Assicurati che la compilazione automatica funzioni per tutti i campi

Oltre a indirizzi, dati dell'account e dati della carta di credito, ci sono molti altri campi in cui i browser possono aiutare gli utenti con la compilazione automatica.

Quando aggiungi il campo del numero di telefono al modulo, verifica se puoi utilizzare uno dei [disponibile](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) per il completamento automatico. Hai trovato un valore appropriato per il campo del modulo? Aggiungilo.

L'utilizzo di valori adatti per l'attributo `autocomplete` consente ai browser di offrire la migliore opzione di compilazione automatica e aiuta gli utenti a compilare i moduli più velocemente.

## Aiuta i browser a capire che un campo non deve essere compilato automaticamente

Hai imparato come funziona la compilazione automatica, come aiutare i browser con la compilazione automatica e perché la compilazione automatica consente agli utenti di compilare facilmente i moduli. A volte, però, vuoi che i browser offrano la compilazione automatica.

```
<label for="one-time-code">One-time code</label>
<input autocomplete="off" type="text" name="one-time-code" id="one-time-code">
```

Una posizione in cui la compilazione automatica non è utile è quando si inseriscono valori univoci una tantum ad esempio un campo monouso. Il valore è sempre diverso e il browser non deve salvare i valori né offrire un'opzione di compilazione automatica. Puoi utilizzare `autocomplete="off"` per questi campi per impedire la compilazione automatica.

Un altro caso d'uso di `autocomplete="off"` è il campo honeypot (vedi [precedente del modulo](https://web.dev/learn/forms/security-privacy?hl=it#a_honeypot)). Anche se il campo non è visibile, i browser potrebbero compilarlo automaticamente con gli altri campi. Attivazione della compilazione automatica la disattivazione garantisce che un utente reale non venga identificato come bot, poiché il campo vengono completate automaticamente.

Dovresti disattivare la compilazione automatica solo se hai la certezza che aiuterà gli utenti.

### Verifica le tue conoscenze

Verifica le tue conoscenze sulla compilazione automatica

Quale valore di completamento automatico dovresti usare per il campo della password in un modulo di registrazione?

`autocomplete="current-password"`

`autocomplete="new-password"`

## Risorse

*   La finestra di [completamento automatico .](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete)
    *   [Il miglior formato per il pagamento e l'indirizzo pratiche](https://web.dev/articles/payment-and-address-form-best-practices?hl=it)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
