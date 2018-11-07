# spid-wordpress-example-roles

Esempio di sito wordpress con login SPID e pagine visibili e/o modificabili per gruppi di utenti SPID.

Dimostra come è possibile definire, prima che abbiano fatto il primo login sul sito wordpress, che gli **utenti SPID** o **specifici gruppi** di utenti SPID possano visualizzare e/o modificare specifiche pagine o articoli.

Utilizza SPID per l'**authentication** e il [sistema di ruoli predefinito di wordpress](https://codex.wordpress.org/Roles_and_Capabilities) per l'**authorization**.

## Use case

Questa funzione potrebbe essere utile:

- ad una **scuola**:
  - per creare un'area del sito accessibile a tutti i genitori, ma non al resto del pubblico
  - per creare delle aree separate per ogni anno scolastico, accessibili ai genitori di alunni che hanno frequentato in quell'anno scolastico, ma non al resto del pubblico
- ad un'**associazione sportiva dilettantistica**: per creare delle aree del sito separate visibili solo agli allenatori o solo ai genitori dei bambini iscritti
- ad un **sito di informazione locale**:
  - per creare un'area del sito accessibile solo agli abbonati
  - per permettere solo agli abbonati di commentare gli articoli
  - per accettare in bozza articoli scritti da chiunque si sia autenticato son SPID, permettendo poi alla redazione di approvarli e renderli pubblici
- ad un'**università**: per dividere il sito in sezioni (es. in base ai dipartimenti: http://example.com/matematica, http://example.com/chimica, http://example.com/fisica), poi raggruppare gli utenti in ruoli (es. DipMatematica, DipChimica, DipFisica) e infine permettere solo agli utenti appartenenti al ruolo corrispondente di creare / modificare pagine o articoli nella sezione rispettiva. 

## Funzionamento

Nella pagina di configurazione del plugin [spid-wordpress](https://github.com/simevo/spid-wordpress) occorre abilitare l'attributo **Codice fiscale** (`fiscalNumber`), in modo che quando un utente fa il login con SPID il plugin aggiunge l'attributo SPID **codice fiscale** nel database di Wordpress, nella tabella wp_usermeta, col nome `spid_fiscalNumber`.

### Ruoli

Se non bastano i 6 ruoli pre-definiti di wordpress (_Super Admin_, _Administrator_, _Editor_, _Author_, _Contributor_, _Subscriber_) è possibile aggiungerne di nuovi col plugin [Members](https://wordpress.org/plugins/members/).

### Associazione utenti SPID / ruoli

Se **tutti** gli utenti loggati con SPID devono acquisire gli stessi diritti (cioè assere assegnati tutti allo **stesso ruolo**), è sufficiente impostare nella pagina di configurazione del plugin [spid-wordpress](https://github.com/simevo/spid-wordpress) a quale ruolo Wordpress devono essere assegnati (ad esempio _Contributor_).

Se invece bisogna poter decidere a priori un'associazione tra i codici fiscali degli utenti SPID e i ruoli Wordpress, è più complicato: serve una _lookup table_. Idealmente questa tabella dovrebbe essere accessibile nella UI di wordpress.

Questa parte si potrebbe implementare ai fini del demo in prima battuta con del codice ad-hoc.

Successivamente qualcuno (!) potrebbe creare un plugin **spid-wordpress-roles** ...

### Controllo di accesso

Per il controllo di accesso in lettura (cioè per rendere **visibili** pagine / articoli per utenti SPID appartenenti ad un certo ruolo) si rimanda all'esempio [spid-wordpress-example-private](https://github.com/simevo/spid-wordpress-example-private).

Per il controllo di accesso in scrittura (cioè per rendere **modificabili** pagine / articoli per utenti SPID appartenenti ad un certo ruolo) si potrebbe usare il plugin [BU Section Editing](https://wordpress.org/plugins/bu-section-editing/) che è compatible con i ruoli creati con Members.

## Demo

TODO
