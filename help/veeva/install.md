---
title: '[!DNL Veeva Vault] Guida all’installazione'
description: Guida all'installazione per consentire l'integrazione di Adobe Sign con Veeva
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 5d61a428-06e4-413b-868a-da296532c964
source-git-commit: d8b7271cae9bcbe8b66311eba0317b8937ea855c
workflow-type: tm+mt
source-wordcount: '2839'
ht-degree: 2%

---

# [!DNL Veeva Vault] Guida all’installazione{#veeva-installation-guide}

[**Contatta il supporto di Adobe Sign**](https://adobe.com/go/adobesign-support-center_it)

## Panoramica {#overview}

Questo documento spiega come stabilire l&#39;integrazione di Adobe Sign con la piattaforma [!DNL Veeva Vault]. [!DNL Veeva Vault] è una piattaforma ECM (Enterprise Content Management) creata per le scienze della vita. Un &quot;insieme di credenziali&quot; è un repository di contenuti e dati con un utilizzo tipico per i file normativi, per i report di ricerca, per le applicazioni di concessione, per i contratti generali e altro ancora. Un&#39;unica impresa può disporre di più &#39;archivi&#39; che devono essere gestiti separatamente.

Le fasi di alto livello per completare l&#39;integrazione sono:

* Attiva il tuo account amministrativo in Adobe Sign (solo nuovi clienti)
* Creare oggetti per tenere traccia della cronologia di un ciclo di vita dei contratti nell&#39;insieme di credenziali.
* Crea un nuovo profilo di protezione.
* Configurare un gruppo in Adobe Sign per mantenere l&#39;utente di integrazione [!DNL Veeva Vault].
* Crea campi documento e copie trasformate.
* Configurare le azioni Web e aggiornare il ciclo di vita del documento.
* Crea impostazione utente e ruolo utente tipo di documento.

## Configura le seguenti opzioni [!DNL Veeva Vault]

Per configurare [!DNL Veeva Vault] per l&#39;integrazione con Adobe Sign, vengono creati alcuni oggetti che consentono di tenere traccia della cronologia di un ciclo di vita di un accordo nell&#39;insieme di credenziali. Gli amministratori devono creare i seguenti oggetti:

* Firma
* Firmatario
* Evento firma
* Elabora Locker

### Crea oggetto firma  {#create-signature-object}

L&#39;oggetto firma viene creato per memorizzare le informazioni relative al contratto. Un oggetto Signaure è un database che contiene informazioni nei campi specifici seguenti:

**Campi oggetto firma**

| Campo | Etichetta | Tipo | Descrizione |
| --- | --- | ---| --- | 
| id_esterno__c | ID accordo | Stringa (100) | Contiene l&#39;ID di accordo univoco di Adobe Sign |
| file_hash__c | Hash file | Stringa (50) | Contiene il chcksum md5 del file inviato ad Adobe Sign |
| nome_v | Nome | Stringa (128) | Contiene il nome del contratto |
| mittente__c | Mittente | Oggetto (utente) | Contiene il riferimento all&#39;utente dell&#39;insieme di credenziali che ha creato il contratto |
| status_firma__c | Stato firma | Stringa (75) | Contiene lo stato del contratto in Adobe Sign |
| tipo_firma__c | Tipo firma | Stringa (20) | Contiene il tipo di firma dell’accordo in Adobe Sign (SCRITTA o ESIGN) |
| data_inizio__c | Data di inizio | DataOra | Data di invio del contratto per la firma |
| annullamento_data__c | Data di annullamento | DataOra | Contiene la data di annullamento del contratto. |
| data_completamento__c | Data completamento | DataOra | Contiene la data in cui è stato completato il contratto. |
| visualizzabile_rendition_usato__c | Rendering visualizzabile utilizzato | Booleano | Flag che indica se la copia trasformata visualizzabile è stata inviata per la firma. (per impostazione predefinita, è true) |

![Immagine dei dettagli dell&#39;oggetto firma](images/signature-object-details.png)

### Crea oggetto firmatario {#create-signatory-object}

L&#39;oggetto firmatario viene creato per memorizzare le informazioni relative ai partecipanti di un contratto. Contiene informazioni nei seguenti campi specifici:

**Campi oggetto firmatario**

| Campo | Etichetta | Tipo | Descrizione |
| --- | --- | ---| --- | 
| email__c | E-mail | Stringa (120) | Contiene l&#39;ID di accordo univoco di Adobe Sign |
| id_esterno__c | ID partecipante | Stringa (80) | Contiene l’identificativo univoco del partecipante Adobe Sign |
| nome_v | Nome | Stringa (128) | Contiene il nome del partecipante Adobe Sign |
| ordine__c | Ordine | Numero | Detiene il numero di ordine del partecipante del contratto Adobe Sign |
| ruolo_c | Ruolo | Stringa (30) | Detiene il ruolo del partecipante al contratto Adobe Sign |
| firma__c | Firma | Oggetto (firma) | Contiene il riferimento al record padre della firma |
| status_firma__c | Stato firma | Stringa (100) | Detiene lo stato del partecipante al contratto Adobe Sign |
| utente__c | Utente | Oggetto (utente) | Contiene il riferimento al record utente del firmatario se il partecipante è un utente dell’insieme di credenziali |

![Immagine dei dettagli del firmatario](images/signatory-object-details.png)

### Crea oggetto evento firma  {#create-signature-event}

L&#39;oggetto Evento firma viene creato per memorizzare le informazioni relative all&#39;evento di un contratto. Contiene informazioni nei seguenti campi specifici:

| Campo | Etichetta | Tipo | Descrizione |
| --- | --- | ---| --- | 
| act_user_email__c | E-mail utente interessato | Stringa | Contiene l&#39;e-mail dell&#39;utente di Adobe Sign che ha eseguito l&#39;azione che ha causato la generazione dell&#39;evento |
| nome_utente_azione_azione_c | Nome utente facente funzione | Stringa | Contiene il nome dell&#39;utente di Adobe Sign che ha eseguito l&#39;azione che ha generato l&#39;evento |
| descrizione__c | Descrizione | Stringa | Contiene la descrizione dell&#39;evento Adobe Sign |
| data_evento__c | Data evento | DataOra | Contiene la data e l&#39;ora dell&#39;evento Adobe Sign |
| tipo_evento__c | Tipo di evento | Stringa | Contiene il tipo dell&#39;evento Adobe Sign |
| nome_v | Nome | Stringa | Nome evento generato automaticamente |
| commento_partecipante__c | Commento del partecipante | Stringa | Contiene il commento del partecipante a Adobe Sign, se disponibile |
| partecipante_email__c | Indirizzo e-mail partecipante | Stringa | Contiene l&#39;e-mail del partecipante Adobe Sign |
| partecipante_ruolo__c | Ruolo partecipante | Stringa | Detiene il ruolo del partecipante di Adobe Sign |
| firma__c | Firma | Oggetto (firma) | Contiene il riferimento al record padre della firma |

![Immagine dei dettagli dell&#39;evento della firma](images/signature-event-object-details.png)

### Crea oggetto Process Locker  {#create-process-locker}

Viene creato un oggetto Process Locker per bloccare il processo di integrazione di Adobe Sign. Non richiede campi personalizzati.

![Immagine dei dettagli dell&#39;evento della firma](images/process-locker-details.png)

## Crea profili di sicurezza{#security-profiles}

Per una corretta integrazione dell&#39;insieme di credenziali, viene creato un nuovo profilo di protezione denominato *Profilo di integrazione dei segni di Adobe* e viene impostata l&#39;autorizzazione per *Azioni di amministrazione dei segni di Adobe*. Il profilo di integrazione dei segni di Adobe viene assegnato all&#39;account di sistema e viene utilizzato dall&#39;integrazione quando si chiama l&#39;API dell&#39;insieme di credenziali. Questo profilo consente le autorizzazioni per:

* API dell&#39;insieme di credenziali
* Lettura, creazione, modifica ed eliminazione: Firma, firma, eventi firma e processo oggetti di blocco

![Immagine dei dettagli dell&#39;evento della firma](images/security-profiles.png)

Tutti i profili di sicurezza degli utenti che richiedono l&#39;accesso alla cronologia di Adobe Sign in Vault devono disporre dell&#39;autorizzazione Lettura per gli oggetti Signature, Firmatory e Signature Event.

![Immagine dei dettagli dell&#39;evento della firma](images/set-permissions.png)

## Crea gruppo {#create-group}

Per configurare Adobe Sign per [!DNL Vault], viene creato un nuovo gruppo denominato *Adobe Sign Admin Group*. Questo gruppo viene utilizzato per impostare la protezione a livello di campo del documento per i campi correlati a Adobe Sign e deve includere per impostazione predefinita *Profilo di integrazione dei segni di Adobe*.

![Immagine dei dettagli dell&#39;evento della firma](images/create-admin-group.png)

## Crea utente {#create-user}

L&#39;utente dell&#39;account del sistema Vault per l&#39;integrazione di Adobe Sign deve:

* Avere un profilo di integrazione di Adobe Sign
* Disporre di un profilo di sicurezza
* Dispone di criteri di sicurezza specifici che disattivano la scadenza della password
* Essere membro di Adobe Sign Admin Group.

Per garantire che l&#39;utente dell&#39;account di sistema appartenga al gruppo di amministrazione di Adobe Sign per per il ciclo di vita del documento specifico, è necessario creare record di impostazione ruolo utente.

## Crea ruoli applicazione {#create-application-roles}

È necessario creare un ruolo applicazione denominato *Ruolo amministratore firma Adobe*. Questo ruolo deve essere definito nel ciclo di vita di ogni tipo di documento idoneo per Adobe Signature. Per ciascuno degli stati del ciclo di vita specifici di Adobe Sign, Adobe Sign Admin Role viene aggiunto e configurato con le autorizzazioni appropriate.

![Immagine della creazione dei ruoli dell&#39;applicazione](images/create-application-roles.png)

## Crea campi documento {#create-fields}

Per stabilire l&#39;integrazione con Adobe Sign, gli amministratori devono creare due nuovi campi documento condivisi:

* Firma (firma__c)
* Consenti azioni utente di Adobe Sign (allow_adobe_sign_user_actions__c)

![Immagine dei dettagli del documento](images/create-document-fields.png)

Questi campi condivisi devono essere aggiunti a tutti i tipi di documento idonei per Adobe Signature. Entrambi i campi devono disporre di una protezione specifica che consenta solo ai membri di Adobe Sign Admin Group di aggiornare i propri valori.

![Immagine dei dettagli del campo firma](images/signature-field-details.png)

Gli amministratori devono aggiungere il campo condiviso esistente *Disabilita sovrapposizioni dell&#39;insieme di credenziali (disable_vault_overlay__v)* e impostarlo su Attivo per tutti i tipi di documento idonei per Adobe Signature. Se lo si desidera, il campo può disporre di una protezione specifica che consente solo ai membri del gruppo Adobe Sign Admin di aggiornarne il valore.

![Immagine delle azioni utente di Consenti firma adobe](images/allow-adobe-sign-user-actions.png)

## Crea copie trasformate documento {#create-renditions}

Gli amministratori devono creare un nuovo tipo di copia trasformata denominato *Adobe Sign Rendition (adobe_sign_rendition__c)*, utilizzato dall&#39;integrazione dell&#39;insieme di credenziali per caricare documenti PDF firmati in Adobe Sign. La copia trasformata di Adobe Sign deve essere dichiarata per ogni tipo di documento idoneo per Adobe Signature.

![Immagine dei tipi di rendering](images/rendition-type.png)

![Immagine dei tipi di rendering](images/edit-details-clinical-type.png)

## Configura azioni Web {#web-actions}

L&#39;integrazione di Adobe Sign e Vault richiede la creazione e la configurazione delle seguenti due azioni Web:

* **Crea simbolo** Adobe: Crea o visualizza Adobe Sign Agreement.

   Tipo: Documento
Destinazione: Visualizza nell&#39;insieme di credenziali
URL: <https://{integrationDomain}/adobe-sign-int/signature?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&sessionId=${Session.id}&vaultId=${Vault.Id>}

* **Annulla simbolo** Adobe: Annulla un accordo esistente in Adobe Sign e ripristina lo stato di un documento in quello iniziale.

   Tipo: Documento
Destinazione: Visualizza nell&#39;insieme di credenziali
URL: <https://{integrationDomain}/adobe-sign-int/cancel?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&sessionId=${Session.id}&vaultId=${Vault.Id>}

## Aggiorna ciclo di vita del documento {#document-lifecycle}

Per ogni tipo di documento idoneo per Adobe Signature, il ciclo di vita del documento corrispondente deve essere aggiornato aggiungendo nuovi ruoli e stati del ciclo di vita.

### Ruolo Ciclo di vita {#lifecycle-role}

È necessario aggiungere il ruolo dell&#39;applicazione Adobe Sign Admin in tutti i cicli di vita utilizzati dai documenti idonei per Adobe Signature. Questo ruolo deve essere creato con le seguenti opzioni:

* Attiva controllo di accesso dinamico
* Regole di condivisione documenti che includono solo il gruppo di tipi di documento

![Immagine dei ruoli di amministrazione del ciclo di vita](images/document-lifecycle-admin-role.png)

### Stati ciclo di vita {#lifecycle-states}

Il ciclo di vita del contratto di Adobe Sign ha i seguenti stati:

* PROGETTO
* AUTOMATIZZAZIONE O DOCUMENTI_NOT_YET_PROCESSED
* OUT_FOR_SIGNATURE o OUT_FOR_APPROVAL
* FIRMATA O APPROVATA
* ANNULLATA
* SCADUTO

Quando un documento dell&#39;insieme di credenziali viene inviato ad Adobe Sign, il relativo stato deve corrispondere allo stato in cui si trova il contratto. A tale scopo, è necessario aggiungere i seguenti stati in ogni ciclo di vita utilizzato dai documenti idonei per Adobe Signature:

* **Prima di Adobe Signature** (Reviewed): Nome segnaposto per lo stato da cui il documento può essere inviato ad Adobe Sign. In base al tipo di documento, può essere Stato Bozza o Revisionato. L&#39;etichetta dello stato del documento può essere personalizzata in base alle esigenze del cliente. Prima che lo stato Firma Adobe definisca le seguenti due azioni utente:

   * Azione che modifica lo stato del documento in *In Adobe Sign Draft*. Il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento per qualsiasi ciclo di vita. Se necessario, i criteri per questa azione possono essere impostati su &quot;Consenti azioni utente di Adobe Sign uguale a Sì&quot;.
   * Azione che chiama l&#39;azione Web ‘Adobe Sign’. Questo stato deve avere una protezione che consenta al ruolo di amministrazione di Adobe Sign di: visualizzare il documento, visualizzare il contenuto, modificare i campi, modificare le relazioni, scaricare l&#39;origine, gestire il rendering visualizzabile e modificare lo stato.

   ![Immagine dello stato del ciclo di vita 1](images/lifecycle-state1.png)

* **In Adobe Sign Draft**: Nome segnaposto per lo stato che indica che il documento è già caricato in Adobe Sign e che il relativo accordo è in stato DRAFT. È uno stato obbligatorio. Questo stato deve negare l&#39;accesso a cinque azioni utente:

   * Azione che modifica lo stato del documento in *In Adobe Sign Authoring* stato. Il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento per qualsiasi ciclo di vita. Se necessario, i criteri per questa azione possono essere impostati su &quot;Consenti azioni utente di Adobe Sign uguale a Sì&quot;.
   * Azione che modifica lo stato del documento in *In Adobe Signing state*. Il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento per qualsiasi ciclo di vita. Se necessario, i criteri per questa azione possono essere impostati su &quot;Consenti azioni utente di Adobe Sign uguale a Sì&quot;.
   * Azione che modifica lo stato del documento in *Adobe Sign Canceled* stato. Il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento per qualsiasi ciclo di vita. Se necessario, i criteri per questa azione possono essere impostati su &quot;Consenti azioni utente di Adobe Sign uguale a Sì&quot;.
   * Azione che chiama l&#39;azione Web ‘Adobe Sign’.
   * Azione che chiama l&#39;azione Web &#39;Annulla Adobe Sign&#39;. Questo stato deve avere una protezione che consenta al ruolo Amministrazione di Adobe Sign di: visualizzare il documento, visualizzare il contenuto, modificare i campi, modificare le relazioni, scaricare l&#39;origine, gestire il rendering visualizzabile e modificare lo stato.

   ![Immagine dello stato del ciclo di vita 2](images/lifecycle-state2.png)

* **In Adobe Sign Authoring**: Questo è un nome segnaposto per lo stato che indica che il documento è già caricato in Adobe Sign e che il relativo contratto è in stato AUTHORING o DOCUMENTS_NOT_YET_PROCESSED. È uno stato obbligatorio. Per questo stato devono essere definite quattro azioni utente:

   * Azione che modifica lo stato del documento in Adobe Sign Annullato. Il nome di questa azione utente deve essere uguale per tutti i tipi di documento indipendentemente dal ciclo di vita. Se necessario, i criteri per questa azione possono essere impostati su &quot;Consenti azioni utente di Adobe Sign uguale a Sì&quot;.
   * Azione che modifica lo stato del documento in In Adobe Signing. Il nome di questa azione utente deve essere uguale per tutti i tipi di documento indipendentemente dal ciclo di vita. Se necessario, i criteri per questa azione possono essere impostati su &quot;Consenti azioni utente di Adobe Sign uguale a Sì&quot;.
   * Azione che chiama l&#39;azione Web ‘Adobe Sign’
   * Azione che chiama l&#39;azione Web &#39;Annulla Adobe Sign&#39;. Questo stato deve avere una protezione che consenta al ruolo Amministrazione di Adobe Sign di: visualizzare il documento, visualizzare il contenuto, modificare i campi, modificare le relazioni, scaricare l&#39;origine, gestire il rendering visualizzabile e modificare lo stato.

   ![Immagine dello stato del ciclo di vita 3](images/lifecycle-state3.png)

* **In Adobe Signing**: Si tratta di un nome segnaposto per lo stato che indica che il documento è caricato in Adobe Sign e che il relativo accordo è già inviato ai partecipanti (stato OUT_FOR_SIGNATURE o OUT_FOR_APPROVAL). È uno stato obbligatorio. Per questo stato devono essere definite cinque azioni utente:

   * Azione che modifica lo stato del documento in Adobe Sign Annullato. Lo stato obiettivo di questa azione può essere qualsiasi requisito del cliente e può essere diverso per tipi diversi. Il nome di questa azione utente deve essere uguale per tutti i tipi di documento indipendentemente dal ciclo di vita. Se necessario, i criteri per questa azione possono essere impostati su &quot;Consenti azioni utente di Adobe Sign uguale a Sì&quot;.
   * Azione che modifica lo stato del documento in stato Rifiutato firma Adobe. Lo stato obiettivo di questa azione può essere qualsiasi requisito del cliente e può essere diverso per tipi diversi. Il nome di questa azione utente deve essere uguale per tutti i tipi di documento indipendentemente dal ciclo di vita. Se necessario, i criteri per questa azione possono essere impostati su &quot;Consenti azioni utente di Adobe Sign uguale a Sì&quot;.
   * Azione che modifica lo stato del documento nello stato di Adobe Signed. Lo stato obiettivo di questa azione può essere qualsiasi requisito del cliente e può essere diverso per tipi diversi. Tuttavia, il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento indipendentemente dal ciclo di vita. Se necessario, i criteri per questa azione possono essere impostati su &quot;Consenti azioni utente di Adobe Sign uguale a Sì&quot;.
   * Azione che chiama l&#39;azione Web *Adobe Sign*.
   * Azione che chiama Web Action *Annulla Adobe Sign*. Questo stato deve avere una protezione che consenta al ruolo Amministrazione di Adobe Sign di: visualizzare il documento, visualizzare il contenuto, modificare i campi, modificare le relazioni, scaricare l&#39;origine, gestire il rendering visualizzabile e modificare lo stato.

   ![Immagine dello stato del ciclo di vita 4](images/lifecycle-state4.png)

* **Adobe Fired (Approvato)**: Si tratta di un nome segnaposto per lo stato che indica che il documento è caricato in Adobe Sign e che il relativo accordo è stato completato (stato FIRMATO o APPROVATO). È uno stato obbligatorio e può essere uno stato del ciclo di vita esistente, come Approvato.
Questo stato non richiede azioni utente. Questo stato deve avere una protezione che consenta al ruolo Amministrazione di Adobe Sign di: visualizzare i documenti, visualizzare il contenuto e modificare i campi.

Nel diagramma seguente vengono illustrati i mapping tra gli stati del documento di Adobe Sign e di Vault, in cui lo stato &quot;Prima di Adobe Signature&quot; è Bozza.

![Immagine dei mapping di Adobe Sign Vault](images/sign-vault-mappings.png)

## Crea gruppo di tipi di documento e Imposta ruolo utente  {#document-type-group-user-role}

### Crea gruppo di tipi di documento {#create-document-type-group}

Gli amministratori devono creare un nuovo record del gruppo di tipi di documento denominato &quot;Adobe Sign Document&quot;. Questo gruppo di tipi di documento viene aggiunto per tutte le classificazioni di documenti idonee per il processo Adobe Sign. Poiché la proprietà del gruppo di tipi di documento non è ereditata dal tipo al sottotipo né dal sottotipo al livello di classificazione, è necessario impostarla per la classificazione di ciascun documento idonea per Adobe Sign.

![Immagine del tipo di documento](images/document-type.png)

### Crea impostazione ruolo utente {#create-user-role-setup}

Una volta configurato correttamente il ciclo di vita, il sistema deve garantire che l&#39;utente di Adobe Sign Admin sia aggiunto da DAC per tutti i documenti idonei per il processo di Adobe Sign. A tale scopo, è necessario creare il record di impostazione del ruolo utente appropriato che specifica:

* Gruppo di tipi di documento come &#39;Documento segni di Adobe&#39;,
* Ruolo applicazione come &#39;Ruolo di amministrazione di Adobe Sign&#39; e
* Utente di integrazione.

![Immagine dell&#39;impostazione del ruolo utente](images/user-role-setup.png)

>[!NOTE]
>
>Se l&#39;oggetto Impostazione ruolo utente non contiene il campo che fa riferimento all&#39;oggetto Gruppo tipi di documento, è necessario aggiungere questo campo.

## Ciclo di vita dell&#39;implementazione pacchetto {#deployment-lifecycle}

### Ciclo di vita dell&#39;implementazione generale {#general-deployment}

**Passaggio 1.** Creare un nuovo ruolo applicazione denominato &#39;Adobe Sign Admin Role&#39;.

**Passaggio 2.** Create un nuovo gruppo di tipi di documento denominato &#39;Adobe Sign Document&#39;.

**Passaggio 3.** Distribuire il pacchetto.

**- 4.** Creare un nuovo gruppo gestito dall&#39;utente denominato &#39;Adobe Sign Admin Group&#39;.

**Fase 5.** Creare un profilo utente di integrazione con il profilo di sicurezza &quot;Adobe Sign Integration Profile&quot; e assegnarlo al gruppo di amministrazione di Adobe Sign.

**- 6.** Assegnare le autorizzazioni di lettura per tutti i profili di protezione agli oggetti Signature, Firnatory e Signature Event per gli utenti che richiedono l&#39;accesso alla cronologia di Adobe Sign nell&#39;insieme di credenziali.

**- 7.** Definire il ruolo di amministrazione di Adobe Sign nel ciclo di vita di ogni tipo di documento idoneo per Adobe Signature. Per ogni stato del ciclo di vita specifico di Adobe Sign, questo ruolo viene aggiunto e configurato con le autorizzazioni appropriate.

**- 8.** Dichiarare Adobe Sign Rendition per ogni tipo di documento idoneo per Adobe Signature.

**- 9.** Per ogni tipo di documento idoneo per Adobe Signature, aggiornare il ciclo di vita del documento corrispondente aggiungendo nuovi ruoli e stati del ciclo di vita.

**Passaggio 10.** Aggiungere il gruppo di tipi di documento denominato &#39;Adobe Sign Document&#39; per tutte le classificazioni di documenti idonee per il processo Adobe Sign.

**Fase 11.** Una volta completate tutte le configurazioni, il sistema deve garantire che l&#39;utente di Adobe Sign Admin sia aggiunto da DAC per tutti i documenti idonei per il processo di Adobe Sign. A tale scopo, è necessario creare il record di impostazione del ruolo utente appropriato che specifica il gruppo di tipi di documento come &#39;Adobe Sign Document&#39;, il ruolo dell&#39;applicazione come &#39;Adobe Sign Admin Role&#39; e un utente di integrazione.

### Ciclo di vita di distribuzione specifico {#specific-deployment}

**Passaggio 1.** Creare un nuovo ruolo applicazione denominato &#39;Adobe Sign Admin Role&#39;.

**Passaggio 2.** Create un nuovo gruppo di tipi di documento denominato &#39;Adobe Sign Document&#39;.

**Passaggio 3.** Distribuire il pacchetto.

**- 4.** Creare un nuovo gruppo gestito dall&#39;utente denominato &#39;Adobe Sign Admin Group&#39;.

**Fase 5.** Creare un profilo utente di integrazione con profilo di sicurezza denominato &#39;Profilo di integrazione di Adobe Sign&#39; e assegnarlo al gruppo di amministrazione di Adobe Sign.
