---
title: Adobe EchoSign per SugarCRM
description: Guida all’installazione per abilitare l’integrazione di Adobe Sign con SugarCRM
product: Adobe Sign
content-type: reference
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 0512f616-568a-4b96-9bd1-48e67bc3536b
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '2354'
ht-degree: 0%

---


# [!DNL SugarCRM] Guida all&#39;installazione {#sugarcrm-install-guide}

[Contatta l’Assistenza clienti](https://adobe.com/go/adobesign-support-center)

Adobe [!DNL EchoSign] per [!DNL SugarCRM] è una soluzione leader per la firma elettronica e la gestione di contratti via web che offre automazione delle firme elettroniche in [!DNL SugarCRM] per firme elettroniche e fax. Gli utenti possono inviare direttamente i contratti da SugarCRM, visualizzare la cronologia dei contratti e salvare i contratti firmati con account, contatti, preventivi e altro ancora associati.
Adobe [!DNL EchoSign] per [!DNL SugarCRM] è disponibile per tutte le versioni supportate di SugarCRM, tra cui 6.3 - 6.7 per soluzioni on demand o in sede.

Questo documento è una guida per [!DNL SugarCRM] per informazioni su come installare e configurare l’Adobe [!DNL EchoSign] per [!DNL SugarCRM] plugin.

## Installa questo plug-in {#install-plugin}

1. Adobe [!DNL EchoSign] per [!DNL SugarCRM]  file di archivio dal [Listino di SugarExchange](http://www.sugarexchange.com/product_details.php?product=1123).
1. Accedi a [!DNL SugarCRM] con il tuo account amministratore.
1. Vai a **[!UICONTROL Amministrazione]** > **[!UICONTROL Caricatore moduli]**.

   ![Immagine](images/module-loader.png)

1. Per caricare il file di archivio dell’Adobe [!DNL EchoSign] per [!DNL SugarCRM] plugin, seleziona **[!UICONTROL Sfoglia]**, quindi selezionare il file di archivio, quindi selezionare **[!UICONTROL Carica]**.
1. Dopo aver caricato il file di archivio, seleziona **[!UICONTROL Installa]** per avviare l&#39;installazione.
1. Rivedi i termini e le condizioni, quindi seleziona **[!UICONTROL Accetta]** > **[!UICONTROL Commit]**.
1. Se il plug-in viene installato correttamente, la barra di avanzamento indica che l’operazione è stata completata al 100%.  Se la barra di avanzamento non raggiunge il 100%, seleziona **[!UICONTROL Registro visualizzazione]** per visualizzare l&#39;errore riscontrato da SugarCRM.

   ![Immagine](images/display-log.png)

1. Dopo l’installazione, passa a **[!UICONTROL Amministrazione > Riparazione]** e Seleziona **[!UICONTROL Riparazione e ricostruzione rapide]**.

>[!NOTE]
>
>Se stai installando il plug-in su [!DNL SugarCRM] OnDemand, registra un ticket di supporto con [!DNL SugarCRM] per rimuovere temporaneamente le restrizioni della finestra di ispezione dei pacchetti per OnDemand in modo che il pacchetto possa essere installato. Questo è parte del processo standard.

## Aggiorna il plug-in {#upgrade-plugin}

Se state aggiornando l’Adobe [!DNL EchoSign] per [!DNL SugarCRM] plugin a una versione più recente, installate il plug-in senza disinstallare la versione precedente.
Dopo aver aggiornato il plug-in, passa a **[!UICONTROL Amministrazione]** > **[!UICONTROL Riparazione]** e seleziona **[!UICONTROL Riparazione e ricostruzione rapide]**.

**Nota:** Se disinstalli un plugin precedente, non rimuovere le tabelle durante la disinstallazione. In caso contrario, è possibile che [!DNL EchoSign] dati dell&#39;accordo.

## Configurare il plug-in {#configure-plugin}

1. Se sei già un Adobe [!DNL EchoSign] cliente, continua al passaggio 2.

   Se non si dispone di un [!DNL EchoSign] account, [iscriviti a una versione di prova GRATUITA valida 14 giorni](https://sugarcrmintegration.echosign.com/public/login) e segui i passaggi di registrazione online per abilitare il tuo Adobe [!DNL EchoSign] account.
1. Accedi a [Account Echo Sign](http://www.echosign.com) e segui questi passaggi:
   1. Seleziona **[!UICONTROL Account]** tab.
   1. Seleziona **[!UICONTROL API EchoSign]** in basso a sinistra.
   1. Seleziona **[!UICONTROL Abilita accesso API]** e ottieni la chiave API dalla pagina.

   ![Immagine](images/enable-api-access.png)

1. In SugarCRM, passare a **[!UICONTROL Amministrazione]** > **[!UICONTROL Impostazioni Adobe EchoSign]** e immettere la chiave API nel campo etichettato **[!UICONTROL Chiave API di EchoSign]**.
1. Facoltativamente, configura il plugin con le seguenti impostazioni:

   1. Allega automaticamente PDF durante la creazione di un accordo da un preventivo: Selezionare se allegare automaticamente un PDF del preventivo se [!DNL SugarCRM] l’utente crea un accordo EchoSign dal modulo Quote.
   1. Gestione elenco destinatari: Selezionare i moduli da visualizzare nel sottopannello Destinatario nel [!DNL EchoSign] Modulo Accordi. Questo aggiunge anche la proprietà [!DNL EchoSign] Gli accordi sono suddivisi in sottogruppi di tali moduli.
   1. Aggiungere i pulsanti di invio ai moduli seguenti: Selezionare se si desidera creare [!DNL EchoSign] Pulsante/azione dell’accordo da includere nelle azioni principali del modulo Preventivo.
   1. Seleziona **[!UICONTROL Salva]** per memorizzare le impostazioni.

**Nota:** L&#39;Adobe [!DNL EchoSign] per [!DNL SugarCRM] il plugin richiede la [Estensione SOAP PHP](http://www.php.net/manual/en/book.soap.php). Per abilitare il supporto SOAP, configurate PHP con enable-soap.

## Scarica gli aggiornamenti degli accordi (per [!DNL SugarCRM] versioni 6.3 o successive) {#get-agreement-updates}

Per le versioni 6.3 e successive, puoi utilizzare le due opzioni seguenti per ottenere gli aggiornamenti degli accordi. Nelle versioni precedenti di SugarCRM, il plug-in per impostazione predefinita offre solo il metodo di callback (Opzione 1).

### Opzione 1: Impostare il metodo di callback per l’invio degli aggiornamenti a EchoSign

Se il tuo sito Web è pubblico, puoi avere Adobe EchoSign ping [!DNL SugarCRM] ogni volta che si verifica un nuovo evento. [!DNL SugarCRM] quindi aggiorna lo stato dell’accordo, gli eventi e scarica il documento firmato (se firmato) automaticamente e in tempo reale. (Se si è in presenza di un firewall, è necessario autorizzare il [!DNL EchoSign] gli indirizzi IP del server o utilizzate il metodo Pianificed Job per aggiornare gli accordi EchoSign descritti nella sezione successiva di questa guida).

1. Vai a **[!UICONTROL Amministrazione]** > **[!UICONTROL Impostazioni Adobe EchoSign]**.
1. Seleziona la casella di controllo **[!UICONTROL Utilizzare il metodo di callback EchoSign]** per aggiornare gli eventi e gli stati degli accordi.
1. Seleziona **[!UICONTROL Salva]**.

### Opzione 2: Impostare un processo pianificato per [!DNL SugarCRM] Istanze dietro un firewall

Il [!DNL EchoSign] per [!DNL SugarCRM] Il plug-in può anche utilizzare un processo pianificato per eseguire query [!DNL EchoSign] per gli aggiornamenti agli accordi inviati per la firma. È possibile utilizzare il metodo di query del processo pianificato se si dispone di un [!DNL SugarCRM] l&#39;installazione è protetta da un firewall.

Per configurare:

1. Vai a **[!UICONTROL Amministrazione]** > **[!UICONTROL Pianificatore]**.
1. Dal menu a discesa della scheda, seleziona **[!UICONTROL Crea pianificazione]**.
1. Immetti un Nome processo.
1. Per il campo Processo, selezionare **[!UICONTROL Adobe EchoSign Status Updater]**.
1. Impostare il processo in modo che venga eseguito con la frequenza necessaria. Suggeriamo di impostarlo su 10 minuti, il che significa che dopo l’apertura, la lettura o la firma di un accordo, potrebbero essere necessari fino a 10 minuti per [!DNL SugarCRM] per essere aggiornato con tali informazioni.

   **Nota:** Se hai molti accordi pronti per la firma, questa operazione viene eseguita troppo frequentemente, il sistema potrebbe rallentare.

   ![Immagine](images/echosign-status-updater.png)

1. Vai a **[!UICONTROL Amministrazione]** > **[!UICONTROL Impostazioni Adobe EchoSign]**.
1. Deseleziona la casella **[!UICONTROL Utilizzare il metodo di callback EchoSign]** per aggiornare gli eventi e gli stati degli accordi.
1. Seleziona **[!UICONTROL Salva]**.
Nota: Attivare gli Utilità di pianificazione [!DNL SugarCRM] perché questo funzioni.

Per aggiungere accordi EchoSign ad altri [!DNL SugarCRM] moduli:

1. Vai a **[!UICONTROL Amministrazione]** > **[!UICONTROL Studio]**.
1. Nella struttura ad albero della cartella delle colonne a sinistra, selezionate il modulo da aggiungere [!DNL EchoSign] Accordi.
1. Seleziona **[!UICONTROL Relazioni]**> **[!UICONTROL Aggiungi relazioni]**.
1. Dal menu a discesa, seleziona Testo come **[!UICONTROL Uno a molti]** e Modulo come **[!UICONTROL Accordi EchoSign]**.
1. Seleziona **[!UICONTROL Salva e distribuisci]**.

   ![Immagine](images/save-and-deploy.png)

   [!DNL EchoSign] Gli accordi vengono ora visualizzati nel modulo e gli accordi possono essere creati e monitorati.

   ![Immagine](images/echosign-agreements.png)

**Altri passaggi di configurazione**

* **Nascondere [!DNL EchoSign] Moduli**: È possibile nascondere la proprietà [!DNL EchoSign] Destinatari e [!DNL EchoSign] Moduli Eventi accedendo a Schede e Sottopannelli del modulo Amministrazione&quot; e spostandoli nella colonna nascosta.
* **Disattivazione di packageScan**: Se hai attivato packageScan sul tuo sistema, devi disattivarlo durante l&#39;installazione. Se si utilizza [!DNL SugarCRM] On-demand, contatto [!DNL SugarCRM] supporto per disattivare packageScan.

## Disinstallare il plug-in {#uninstall-plugin}

1. Accedi a [!DNL SugarCRM] con il tuo account amministratore.
1. Vai a **[!UICONTROL Amministrazione]** > **[!UICONTROL Caricatore moduli]**.
1. Seleziona **[!UICONTROL Disinstallazione]** accanto al [!UICONTROL Plug-in EchoSign per SugarCRM].
1. Seleziona **[!UICONTROL Commit]** per avviare la disinstallazione. Potete anche scegliere di rimuovere le tabelle di database create per il plugin.

   ![Immagine](images/uninstall-plugin.png)

   Se il plug-in viene disinstallato correttamente, la barra di avanzamento indica che l’operazione è stata completata al 100%. Se la barra di avanzamento non raggiunge il 100%, seleziona [!UICONTROL Registro visualizzazione] per visualizzare l&#39;errore riscontrato da SugarCRM.

   ![Immagine](images/uninstall-display-log.png)

## Adobe [!DNL EchoSign] per [!DNL SugarCRM] {#use-echosign-for-sugarcrm}

È possibile creare un Adobe [!DNL EchoSign] accordo associato a un account, un contatto, un preventivo o altro [!DNL SugarCRM] moduli. Puoi allegare file, specificare i destinatari e inviarli per la firma. Adobe [!DNL EchoSign] aggiornamenti [!DNL SugarCRM] con lo stato corrente dell’accordo e memorizza il contratto firmato in [!DNL SugarCRM] una volta completata.

### Creare e modificare un Adobe [!DNL EchoSign] accordo {#create-edit-agreements}

È possibile creare accordi mediante il metodo [!DNL EchoSign] Modulo Accordi o tramite moduli configurati da un [!DNL SugarCRM] amministratore.

1. Dal [!UICONTROL Azioni] elenco nella [!UICONTROL Accordi EchoSign] , seleziona **[!UICONTROL Crea accordo EchoSign]**.
1. Nella sezione principale del [!DNL EchoSign] Accordo, immetti le seguenti informazioni o seleziona tra diverse opzioni dell’accordo:

   1. **[!UICONTROL Nome:]** Immetti un nome per l’accordo.
   1. **[!UICONTROL Tipo firma:]** Seleziona il tipo di firma accettato per il documento. Le opzioni sono Firma elettronica e Firma tramite fax.
   1. **[!UICONTROL Devo Anche Firmare Questo Accordo:]** Indica se anche il mittente deve firmare l’accordo.
   1. **[!UICONTROL Ordine firma:]** Se è selezionata l’opzione precedente Firmo anche questo accordo, seleziona anche l’ordine in cui il mittente e i destinatari devono firmare.
   1. **[!UICONTROL Ricorda ai destinatari di firmare:]** Seleziona la frequenza con cui ricordare a un destinatario di firmare un documento. Le opzioni sono giornaliere o settimanali.
   1. **[!UICONTROL Giorni alla scadenza per la firma:]** Specifica quanti giorni devono trascorrere prima che l’accordo venga firmato.
   1. **[!UICONTROL Visualizza in anteprima, posiziona firma o aggiungi campi modulo:]**  Seleziona questa opzione per visualizzare in anteprima l’accordo prima che venga inviato oppure trascina e rilascia i campi firma, i campi iniziali o altri campi modulo sull’accordo prima che venga inviato ai destinatari. Dopo aver visualizzato l’anteprima del documento o trascinato i campi che desideri inserire nel documento, ricorda di selezionare il pulsante Invia per inviare l’accordo al destinatario.
   1. **[!UICONTROL Firma in hosting per il primo firmatario:]** Indica se il mittente desidera ospitare di persona la firma dell’accordo.
      * **[!UICONTROL Messaggio:]** Includi un messaggio per il destinatario.
      * **[!UICONTROL Account, opportunità, preventivo:]** Seleziona o modifica l’account, l’opportunità o il preventivo associati a questo accordo.
      * **[!UICONTROL Lingua:]** Specifica la lingua in cui la pagina della firma e le notifiche e-mail vengono visualizzate ai destinatari.

      ![Immagine](images/create-agreements.png)


1. Nel [!UICONTROL Opzioni di protezione] sezione del [!UICONTROL Accordo EchoSign], immettere le seguenti informazioni:

   a) **[!UICONTROL Password necessaria per firmare:]** Indica se è necessario immettere una password prima che un destinatario possa firmare un documento.
b) **[!UICONTROL Password necessaria per l&#39;apertura:]** Indica se è necessario immettere una password prima che un destinatario possa aprire un PDF dell’accordo o dell’accordo firmato c) **[!UICONTROL Password:]** Specifica la password da utilizzare per firmare o aprire un documento.
d) **[!UICONTROL Conferma password:]** Confermare la password da utilizzare per firmare o aprire un documento.

1. Nella sezione Altro del [!DNL EchoSign] Accordo, inserisci le seguenti informazioni:

   a) **[!UICONTROL Utente:]** Specificare un [!DNL SugarCRM] utente. L’impostazione predefinita è l’utente che ha effettuato l’accesso al sistema.
b) **[!UICONTROL Team:]** Per modificare l’assegnazione del team principale, immetti il nome del nuovo team principale. Per assegnare altri team al record, fai clic su **[!UICONTROL Seleziona]** e seleziona un team dall’elenco Team, oppure seleziona **[!UICONTROL Aggiungi a]** per aggiungere campi team e immettere i nomi dei team. Per ulteriori informazioni, consulta Assegnazione di record a utenti e team nella [!DNL SugarCRM] Guida all&#39;applicazione.

1. Seleziona **[!UICONTROL Salva]**.

### [!DNL EchoSign] vista dettagli accordo {#agreement-detail-view}

Dopo un [!DNL EchoSign] L’accordo viene salvato, la vista Dettagli dell’accordo include i seguenti sottopannelli:

* **[!UICONTROL Destinatari:]** I contatti elencati in questo pannello secondario ricevono i documenti specificati nel pannello secondario Documenti. Prima di inviare l’accordo, devi aggiungere uno o più destinatari.
* **[!UICONTROL Documenti:]** Carica un nuovo documento o seleziona un documento già caricato in [!DNL SugarCRM] per l&#39;invio per la firma.
* **[!UICONTROL Eventi:]** Qualsiasi azione relativa all’accordo, ad esempio quando l’accordo è stato inviato per la firma, visualizzato o firmato, è elencata in questo sottopannello.
Per modificare un [!DNL EchoSign] Accordo, seleziona la [!UICONTROL Modifica] sul pulsante [!UICONTROL Vista dettagli] dell&#39;accordo.

![Immagine](images/agreement-detail-view.png)

**Nota:** Dopo che un accordo è stato inviato per la firma, la proprietà [!UICONTROL Modifica] viene rimosso dalla vista Dettagli per mantenere la registrazione degli eventi. Tuttavia, potete attivare il pulsante Modifica. A tale scopo, passare a [!UICONTROL Amministratore] > [!UICONTROL Impostazioni Adobe EchoSign] e deseleziona l’opzione *[!UICONTROL Dopo che un accordo è stato inviato per la firma, disattiva la possibilità di modificare o eliminare]*.

### Aggiungere un documento a un [!DNL EchoSign] accordo {#add-document}

[!DNL SugarCRM] gli utenti possono caricare un nuovo documento o selezionare un documento già caricato in [!DNL SugarCRM] mediante il pannello secondario Documenti di un record di accordo EchoSign.
Per caricare un documento, seleziona **[!UICONTROL Carica documento]** nel [!UICONTROL Documenti] sottogruppo.

Vedere la sezione &quot;Modulo documenti&quot; del [!DNL SugarCRM] Guida all’applicazione per ulteriori informazioni sui singoli campi di quel modulo.

Per selezionare un documento, fare clic su **[!UICONTROL Seleziona]** nel sottopannello Documenti. Vedere &quot;Visualizzazione e gestione delle informazioni di registrazione&quot; nella [!DNL SugarCRM] Guida all’applicazione per ulteriori informazioni su come gestire le informazioni correlate nei sottopannelli.

![Immagine](images/add-document-to-agreement.png)

### Specificare un destinatario per un [!DNL EchoSign] accordo {#specify-recipient}

1. Dal [!UICONTROL Destinatario] sottogruppo di un [!DNL EchoSign] Accordo, seleziona **[!UICONTROL Aggiungi destinatario]**.
1. Immettere le informazioni seguenti: a) [!UICONTROL Destinatario:] Seleziona il tipo di destinatario dal menu a discesa. Digita il nome o l’indirizzo e-mail del destinatario nel campo di testo. [!DNL SugarCRM] cerca il nome mentre digiti e offri un elenco di selezioni. Selezionate un nome se viene trovata una corrispondenza. Potete anche selezionare l’icona freccia per selezionare un nome da una finestra a comparsa. Per cancellare il nome dal campo, seleziona la proprietà **[!UICONTROL X]** icona.
b) [!UICONTROL Ruolo:] Seleziona un ruolo dal menu a discesa. Le opzioni sono Firmatario e CC e Approvatore. Un approvatore non deve firmare il documento.
1. Selezionate Salva.

![Immagine](images/add-recipient-to-agreement.png)

### Inviare accordi per la firma {#send-for-signature}

Quando gli accordi sono pronti per essere inviati per la firma, seleziona **[!UICONTROL Send for Signature]** dal menu a discesa in alto a sinistra della pagina. I destinatari riceveranno quindi un messaggio e-mail che li informerà dei documenti in attesa della firma. Dopo che i destinatari firmano il documento, il mittente riceve una notifica e-mail.
Se la proprietà [!UICONTROL Firma in hosting per il primo firmatario] è selezionata, è possibile selezionare **[!UICONTROL Send for Signature]** per consentire al firmatario di firmare il documento con il mittente presente.

![Immagine](images/send-for-signature.png)

A **[!UICONTROL Firma in hosting per firmatario corrente]** accanto al [!UICONTROL Firma in hosting per il primo firmatario] , accessibile fino alla firma del documento. Puoi utilizzare questo collegamento per ospitare la firma dell’accordo per più firmatari o per riaprire la finestra a comparsa se è stata chiusa accidentalmente.
Se [!UICONTROL Visualizzare in anteprima, posizionare la firma o aggiungere campi modulo] è selezionata, seleziona **[!UICONTROL Send for Signature]** per consentire al mittente di visualizzare in anteprima il documento o trascinare i campi sul documento prima che venga inviato. È necessario selezionare **[!UICONTROL Invia]** in quella finestra per inviare l’accordo al destinatario.

Figura 5: Seleziona Send for Signature per inviare un documento a un destinatario per la firma.

### Inviare da un record di preventivo {#send-from-quote-record}

Adobe [!DNL EchoSign] è integrato direttamente con Quotes in [!DNL SugarCRM] in modo che il PDF del preventivo venga generato automaticamente e allegato al record dell’accordo.
Quando visualizzi un preventivo, seleziona **[!UICONTROL Crea accordo EchoSign]** per generare il preventivo e allegarlo automaticamente all’accordo. Il nuovo accordo associa inoltre automaticamente qualsiasi opportunità, account o preventivo correlato.

![Immagine](images/create-echosign-agreement.png)

Per disattivare l’allegato automatico del PDF preventivo all’accordo, passa a **[!UICONTROL Amministrazione]** > **[!UICONTROL Impostazioni Adobe EchoSign]** e deseleziona la casella *[!UICONTROL Allega automaticamente PDF durante la creazione di un accordo da un preventivo]*.

### Annullare un accordo {#cancel-agreement}

È possibile annullare un [!DNL EchoSign] Accordo dopo che è stato inviato per la firma se tutti i destinatari non hanno ancora firmato il documento. A [!UICONTROL Annulla accordo] viene visualizzato nella vista Dettagli di un accordo dopo che un documento è stato inviato per la firma. Seleziona **[!UICONTROL Annulla accordo]** per annullare l’accordo.

![Immagine](images/cancel-agreement.png)

Nota: Se un [!DNL EchoSign] L’accordo viene inviato per la firma e il record viene eliminato; devi annullarlo prima di eliminarlo.

### Monitorare le firme {#track-signatures}

Il [!UICONTROL Eventi] sottogruppo di un [!DNL EchoSign] L’accordo tiene traccia dello stato degli accordi inviati per la firma. Per visualizzare gli ultimi aggiornamenti su un [!DNL EchoSign] Accordo, seleziona **[!UICONTROL Stato aggiornamento]**. Il [!UICONTROL Stato aggiornamento] è disponibile solo dopo che un accordo è stato inviato per la firma.

![Immagine](images/update-cancel-status.png)

Dopo aver inviato un accordo per la firma, seleziona **[!UICONTROL Stato aggiornamento]** per recuperare lo stato più recente.

![Immagine](images/events-subpanel.png)

### Invia promemoria {#send-reminders}

Per inviare un promemoria al firmatario corrente dopo l’invio dell’accordo, seleziona **[!UICONTROL Invia promemoria]**. Invia immediatamente un promemoria e-mail al firmatario corrente relativo all’accordo in attesa di firma.

![Immagine](images/send-reminder.png)
