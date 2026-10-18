# Poster Reading Room

*[English below](#english)*

**Poster Reading Room** è un prototipo sperimentale per la descrizione, l'analisi e l'esplorazione di corpora di manifesti storici, anche provenienti da archivi digitalizzati, attraverso modelli visione-linguaggio (*Vision-Language Models*, VLM).

La piattaforma integra metadati documentari, campi analitici a vocabolario controllato e descrizioni testuali aperte. La griglia considera le caratteristiche visive, tipografiche e compositive degli artefatti, con particolare attenzione alle relazioni tra testo e immagine. Il modello propone una prima analisi che il ricercatore può verificare, correggere e validare.

Sviluppato come strumento di ricerca nell'ambito della storia della comunicazione visiva, il prototipo intende esplorare le possibilità e i limiti dei VLM come supporto alla descrizione e all'interpretazione degli artefatti grafici, senza sostituire la lettura critica dello studioso.

L'applicazione è contenuta in un unico file HTML: **non richiede installazione né un server dedicato**. Per usare le funzioni AI sono necessari una connessione Internet e una chiave API.

## Funzionalità

- **Importazione** di metadati da CSV/JSON o di immagini dal computer.
- **Analisi assistita da VLM** di singoli manifesti o di più record in sequenza, con campi strutturati e osservazioni descrittive.
- **Revisione manuale e validazione** delle schede. Alcune descrizioni validate possono essere riutilizzate come esempi per le analisi successive (*few-shot prompting*).
- **Esplorazione del corpus** attraverso raggruppamenti e frequenze di caratteristiche documentarie, visive e tipografiche, oltre al confronto affiancato tra due manifesti.
- **Lettura interna al fondo**: il modello mette in relazione l'immagine del manifesto selezionato con un campione di schede analitiche di altri record già analizzati. Non confronta direttamente tutte le immagini del corpus.
- **Esportazione** dei record in JSON o CSV.

## Come si usa

1. Apri la demo dal link GitHub Pages indicato nel repository, oppure scarica `index.html` e aprilo nel browser.
2. In **AI · Impostazioni**, seleziona un modello e inserisci la chiave API del provider corrispondente:
   - **Google AI Studio** (Gemini): https://aistudio.google.com
   - **OpenRouter** (diversi modelli, anche con eventuali piani gratuiti): https://openrouter.ai
3. Importa un file **CSV/JSON** contenente i record, oppure carica direttamente le **immagini** dal computer.
4. Compila o modifica manualmente i campi, oppure avvia l'analisi AI di un record o di un lotto. Controlla e, se opportuno, valida le schede.
5. Usa la sezione **Relazioni** per esplorare e confrontare i record; salva periodicamente il lavoro esportandolo in **JSON** o **CSV**.

La compilazione e la revisione manuale non richiedono una chiave API. La disponibilità dei modelli e delle eventuali quote gratuite dipende dai provider.

## Formato di importazione

Il CSV accetta come separatore la virgola, il punto e virgola o la tabulazione. Le colonne elencate sono facoltative; per eseguire un'analisi AI è però necessaria un'immagine accessibile, tramite URL o caricamento locale.

| Colonna | Contenuto |
| --- | --- |
| `source_id` | Codice identificativo del record nella fonte |
| `title` | Titolo |
| `date_display` | Data (se presente, viene estratto il primo anno a quattro cifre) |
| `creator` | Autore / designer |
| `client_name` | Committente |
| `institution`, `source_url` | Istituzione conservatrice e link alla scheda nella fonte |
| `image_url` | URL diretto dell'immagine |
| `dimensions` | Dimensioni (es. `Altezza: 100 Larghezza: 70`) |
| `technique` | Materia e tecnica, mantenute nella formulazione della fonte |
| `historical_notes` | Note storico-critiche |
| `subject` | Descrizione iconografica della fonte, usata come contesto e non come risultato dell'analisi visiva |

Il file `esempio_import.csv` illustra la struttura. Un JSON esportato dalla piattaforma può essere reimportato per recuperare i record e le analisi: **le immagini caricate localmente non vengono incorporate nell'esportazione**, quindi dovranno essere rese nuovamente disponibili.

## Provenienza dei dati e validazione

Per i principali **campi documentari**, la piattaforma distingue i valori importati dalla fonte (**metadati**) da quelli proposti dal modello (**dall'immagine**, **stimato**, **inferito**). I campi inseriti o modificati manualmente non riportano queste etichette. Le note storico-critiche generate in assenza di informazioni documentarie sono segnalate come **da verificare**.

I valori documentari già importati o corretti manualmente sono protetti dalle successive analisi AI. Questa protezione **non si estende a tutti i campi analitici**: una nuova analisi può sostituire descrizioni e classificazioni già corrette. È quindi opportuno esportare una copia del lavoro prima di rianalizzare una scheda.

Le schede validate possono fornire al modello esempi del lessico e del livello di dettaglio attesi nei campi descrittivi. La validazione è un'azione del ricercatore, non una verifica automatica dell'esattezza dei contenuti; inoltre, una successiva rianalisi non azzera necessariamente lo stato di validazione.

## Privacy, dati e costi

- La chiave API viene inserita e mantenuta nella pagina aperta: non è scritta nel file HTML né salvata nel `localStorage`.
- Durante l'analisi, immagini e dati pertinenti al record vengono trasmessi al provider selezionato (**Google AI Studio** oppure **OpenRouter**, che può a sua volta inoltrarli al fornitore del modello).
- Se il browser non riesce a leggere direttamente un'immagine remota, il flusso Gemini può utilizzare il proxy pubblico di terze parti `api.allorigins.win` per recuperarla.
- Alcuni modelli sono a pagamento oppure soggetti a quote e limiti d'uso. Prima di usare materiali riservati o soggetti a restrizioni, verifica le condizioni applicabili ai provider e agli eventuali servizi intermediari.
- Le schede non vengono salvate automaticamente su un server del progetto: **esporta il lavoro prima di ricaricare o chiudere la pagina**. Il browser può conservare alcune preferenze e contatori locali, ma non un backup del corpus.

## Limiti metodologici e tecnici

Le analisi generate dai VLM sono **proposte da verificare**, non dati storici accertati. I risultati dipendono dal modello, dalle istruzioni e dalle caratteristiche della riproduzione digitale (risoluzione, resa cromatica, ritagli, riflessi e altri artefatti). Le proprietà materiali e le tecniche di stampa non possono essere considerate documentate sulla sola base di una riproduzione digitale.

Le categorie a vocabolario controllato sono strumenti interpretativi definiti per specifiche finalità di ricerca, non classificazioni neutrali o universali. L'uso di schede validate come esempi nei prompt può influenzare le risposte successive: un'eventuale valutazione quantitativa dell'accordo tra annotazioni umane e modelli richiede perciò un campione di verifica indipendente dagli esempi forniti al modello.

Alcune immagini remote possono non essere accessibili a causa delle restrizioni del server di origine o del browser (ad esempio CORS). Il funzionamento dei modelli e delle API dipende dai servizi esterni.

## Citazione

Se utilizzi Poster Reading Room, cita la **release effettivamente usata** e il contributo che presenta il progetto:

> Polo, L. (2026). *Analizzare l'archivio grafico con l'AI: Poster Reading Room, un prototipo per la descrizione e l'esplorazione critica di un corpus di manifesti*. *Progetto Grafico*, 43.

I metadati di citazione del software sono riportati anche in `CITATION.cff`.

---

## English

**Poster Reading Room** is an experimental prototype for describing, analysing and exploring corpora of historical posters, including materials from digitised archives, using *Vision-Language Models* (VLMs).

The platform combines documentary metadata, controlled-vocabulary analytical fields and open-text descriptions. Its analytical grid addresses visual, typographic and compositional features, with particular attention to relationships between text and image. A model proposes an initial analysis that researchers can review, correct and validate.

Developed as a research tool in the history of visual communication, the prototype explores both the possibilities and the limitations of VLMs in supporting the description and interpretation of graphic artefacts. It is not intended to replace critical human analysis.

The application consists of a **single HTML file** and requires neither installation nor a dedicated server. AI features require an Internet connection and an API key.

### Features

- **Import** metadata from CSV/JSON files or images from your computer.
- **VLM-assisted analysis** of individual posters or batches, combining structured fields and descriptive observations.
- **Manual review and validation** of records. Selected validated descriptions may be reused as examples in subsequent analyses (*few-shot prompting*).
- **Corpus exploration** through grouping and frequency summaries of documentary, visual and typographic features, plus side-by-side comparison of two posters.
- **Collection-based reading**: the model relates the currently selected poster image to a sample of analytical records from other previously analysed items. It does not directly compare every image in the corpus.
- **Export** records to JSON or CSV.

### Getting started

1. Open the demo using the GitHub Pages link in the repository, or download `index.html` and open it in your browser.
2. Under **AI · Settings**, select a model and enter the relevant provider's API key:
   - **Google AI Studio** (Gemini): https://aistudio.google.com
   - **OpenRouter** (multiple models, some potentially available on free tiers): https://openrouter.ai
3. Import a **CSV/JSON** file containing your records, or upload **images** directly from your computer.
4. Enter or edit fields manually, or run an AI analysis on an individual record or a batch. Review the output and validate records where appropriate.
5. Use **Relations** to explore and compare records. Export your work regularly to **JSON** or **CSV**.

Manual entry and review do not require an API key. Model availability and free-tier limits are determined by the providers.

### Import format

CSV files may use commas, semicolons or tabs as separators. All columns are optional; however, AI analysis requires an accessible image, either from a URL or a local upload.

| Column | Content |
| --- | --- |
| `source_id` | Source record identifier |
| `title` | Title |
| `date_display` | Date (the first four-digit year is extracted, if available) |
| `creator` | Creator / designer |
| `client_name` | Client / commissioner |
| `institution`, `source_url` | Holding institution and source record URL |
| `image_url` | Direct image URL |
| `dimensions` | Dimensions (e.g. `Altezza: 100 Larghezza: 70`) |
| `technique` | Material and technique, preserved as provided by the source |
| `historical_notes` | Historical and critical notes |
| `subject` | Source iconographic description, used as context rather than as the outcome of visual analysis |

See `esempio_import.csv` for an example. A JSON file exported by the application can be reimported to restore records and analyses. **Locally uploaded images are not embedded in exports**, so they must be made available again.

### Data provenance and validation

For the main **documentary fields**, the application distinguishes imported values (**metadata**) from model-generated proposals (**from image**, **estimated**, **inferred**). Manually entered or modified values do not carry these labels. Historical notes generated without documentary metadata are marked **to be verified**.

Existing imported or manually corrected documentary values are protected against subsequent AI analyses. This protection **does not apply to all analytical fields**: running another analysis may overwrite previously corrected descriptions or classifications. Export a backup before reanalysing a record.

Validated records can provide examples of the expected vocabulary and level of detail for descriptive fields. Validation is a researcher action, not an automatic accuracy check. A subsequent analysis also does not necessarily reset the record's validation status.

### Privacy, data and costs

- API keys are entered and held in the open page; they are not written into the HTML file or stored in `localStorage`. 
- During analysis, images and relevant record data are sent to the selected provider (**Google AI Studio** or **OpenRouter**, which may forward them to the underlying model provider).
- If a remote image cannot be retrieved directly by the browser, the Gemini workflow may use the public third-party proxy `api.allorigins.win` to retrieve it.
- Some models charge for usage or impose rate and quota limits. Before processing restricted materials, check the applicable conditions of the provider and any intermediary services.
- Records are not automatically saved on a project server. **Export your work before reloading or closing the page.** The browser may retain some local preferences and counters, but not a backup of the corpus.

### Methodological and technical limitations

VLM outputs are **proposals requiring verification**, not established historical evidence. Results depend on the model, the instructions and the quality of the digital reproduction (resolution, colour fidelity, cropping, reflections and other artefacts). Material properties and printing techniques cannot be considered documented on the basis of a digital image alone.

Controlled-vocabulary categories are interpretative tools developed for specific research purposes; they are neither neutral nor universal classifications. Reusing validated records as prompt examples may influence subsequent outputs. Any quantitative evaluation of agreement between human annotations and model outputs therefore requires an independent evaluation sample, separate from the examples provided to the model.

Some remote images may be inaccessible due to restrictions imposed by their host servers or browsers (such as CORS). Model and API functionality depends on external services.

### Citation

If you use Poster Reading Room, cite the **specific release used** and the article presenting the project:

> Polo, L. (2026). *Analizzare l'archivio grafico con l'AI: Poster Reading Room, un prototipo per la descrizione e l'esplorazione critica di un corpus di manifesti*. *Progetto Grafico*, 43.

Software citation metadata is also available in `CITATION.cff`.
