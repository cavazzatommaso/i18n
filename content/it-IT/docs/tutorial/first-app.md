# Scrivi la tua prima app Electron

Electron consente di creare applicazioni desktop in JavaScript fornendo un eseguibile inclusivo di numerose API native (sistema operativo). Puoi immaginarlo come una variante di Node.js che si focalizza su applicazioni desktop invece dei web server.

Questo non significa che Electron è un legame tra JavaScript e le librerie della interfaccia grafica (GUI). Al contrario, Electron utilizza pagine web come GUI, quindi puoi immaginarlo come un browser Chromium minimale, controllato da JavaScript.

**Note**: Questo esempio lo puoi trovare anche: [download and run immediately](#trying-this-example).

Per quanto riguarda lo sviluppo, un'applicazione Electron è essenzialmente un'applicazione Node.js. Inizia tutto dal file `package.json` Che è identico a quello dei moduli NodeJs. Un app Electron avrebbe di base queste cartelle:

```text
tua-app/
├── package.json
├── main.js
└── index.html
```

Crea una nuova cartella Per la tua prima applicazione Electron. Apri un terminale e digita `npm init` dentro alla cartella principale.

```sh
npm init
```

npm ti aiuterà a creare una versione base del file `package.json`. Lo script `main` è lo script di avvio della tua app, che eseguirà il processo principale. Un esempio per il tuo pacchtto `package.json` può essere simile a questo:

```json
{
  "name": "your-app",
  "version": "0.1.0",
  "main": "main.js"
}
```

**Note**: Se il campo `main` non è presente nel file `package.json`, Electron cercherà di caricare il file `index.js` (Come NodeJs). Se si trattava in realtà di una semplice applicazione Node, dovresti aggiungere uno script `start` che ordina a` node` di eseguire il pacchetto corrente:

```json
{
  "name": "your-app",
  "version": "0.1.0",
  "main": "main.js",
  "scripts": {
    "start": "node ."
  }
}
```

Trasformare questa applicazione Node in una applicazione Electron è abbastanza semplice - sostituiamo il parametro `node` con il parametro electron`.

```json
{
  "name": "your-app",
  "version": "0.1.0",
  "main": "main.js",
  "scripts": {
    "start": "electron ."
  }
}
```

## Installare Electron

A questo punto, devi installare `electron`. Consigliamo di installarlo in modo indipendente nella tua applicazione, che ti permetterà di lavorare in piu applicazioni con differenti versioni di Electron. Per farlo, esegui questo comando dal terminale dalla tua cartella dell'app:

```sh
npm install --save-dev electron
```

Esistono comunque altri metodi per installare Electron. Consulta [installation guide](installation.md) per installarlo tramite proxies, mirrors, e custom caches.

## Sviluppo Electron in breve

Le applicazioni Electron sono sviluppate in JavaScript usando gli stessi principi e metodi che troviamo nella programmazione di Node.js. Tutte le APIs e funzioni in Electron sono accessibili tramite il modulo `electron`, Che può esserre richiesto come un normale modulo Node.js:

```javascript
const electron = require('electron')
```

Il modulo `electron` espone delle funzionalità nei namespace. Ad esempio, il ciclo di vita di un app è gestito da `electron.app`, le finestre vengono create dalla classe `electron.BrowserWindow`. Un semplice file `main.js` può aspettare che la finestra sia pronta e poi creare il contenuto:

```javascript
const {app, BrowserWindow} = require('electron')

function createWindow () {
  // Create the browser window.
  win = new BrowserWindow({width: 800, height: 600})

  // e viene caricato il file index.html della nostra app.
  win.loadFile('index.html')
}

app.on('ready', createWindow)
```

Il file `main.js` dovrebbe creare la finestra e gestire tutti gli eventi che possono intercorrere. Una versione più completa di questa potrebbe permettere l'apertura della console developer, oppure riaprire la finestra se usando macOs clicchiamo l'icona nella barra.

```javascript
const {app, BrowserWindow} = require('electron')

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let win

function createWindow () {
  // Creazione della finestra del browser.
  win = new BrowserWindow({width: 800, height: 600})

  // e viene caricato il file index.html della nostra app.
  win.loadFile('index.html')

  // Open the DevTools.
  win.webContents.openDevTools()

  // Emesso quando la finestra viene chiusa.
  win.on('closed', () => {
    // Eliminiamo il riferimento dell'oggetto window;  solitamente si tiene traccia delle finestre
    // in array se l'applicazione supporta più finestre, questo è il momento in cui 
    // si dovrebbe eliminare l'elemento corrispondente.
    win = null
  })
}

// Questo metodo viene chiamato quando Electron ha finito
// l'inizializzazione ed è pronto a creare le finestre browser.
// Alcune API possono essere utilizzate solo dopo che si verifica questo evento.
app.on('ready', createWindow)

// Terminiamo l'App quando tutte le finestre vengono chiuse.
app.on('window-all-closed', () => {
  // Su macOS è comune che l'applicazione e la barra menù 
  // restano attive finché l'utente non esce espressamente tramite i tasti Cmd + Q
  if (process.platform !== 'darwin') {
    app.quit()
  }
})

app.on('activate', () => {
  // Su macOS è comune ri-creare la finestra dell'app quando
  // viene cliccata l'icona sul dock e non ci sono altre finestre aperte.
  if (win === null) {
    createWindow()
  }
})

// in questo file possiamo includere il codice specifico necessario 
// alla nostra app. Si può anche mettere il codice in file separati e richiederlo qui.
```

Infine il file `index. html` è la pagina web che si desidera visualizzare:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    Stiamo utilizzando Node.js <script>document.write(process.versions.node)</script>,
    Chrome <script>document.write(process.versions.chrome)</script>,
    ed Electron <script>document.write(process.versions.electron)</script>.
  </body>
</html>
```

## Esecuzione della tua App

Quando hai creato i file `main.js`, `index.html`, e `package.json`, puoi provare la tua app digitando `npm start` dalla cartella della tua applicazione.

## Prova questo esempio

Clona ed esegui il codice mostrato in questo tutorial utilizzando il repository [`electron/electron-quick-start`](https://github.com/electron/electron-quick-start).

**Nota:** l'esecuzione di questi comandi richiede [Git](https://git-scm.com).

```sh
# Clona la repository
$ git clone https://github.com/electron/electron-quick-start
# Vai nella repository
$ cd electron-quick-start
# Installa le dependencies
$ npm install
# Avvia l'app
$ npm start
```

For a list of boilerplates and tools to kick-start your development process, see the [Boilerplates and CLIs documentation](./boilerplates-and-clis.md).
