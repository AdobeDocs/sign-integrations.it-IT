---
title: Guida all'installazione di Veeva Vault
description: Guida all'installazione per l'attivazione dell'integrazione di Adobe Sign con Veeva
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 5d61a428-06e4-413b-868a-da296532c964
source-git-commit: 76f1be575130e89d96dfe45f7343382b3a519903
workflow-type: tm+mt
source-wordcount: '4171'
ht-degree: 0%

---

# [!DNL Veeva Vault] Guida all&#39;installazione{#veeva-installation-guide}

[**Contatta il supporto Adobe Acrobat Sign**](https://adobe.com/go/adobesign-support-center)

## Panoramica {#overview}

Questo documento spiega come stabilire l&#39;integrazione di Adobe Acrobat Sign con [!DNL Veeva Vault] piattaforma. [!DNL Veeva Vault] È una piattaforma ECM (Enterprise Content Management) sviluppata per le scienze della vita. Un &quot;Vault&quot; è un repository di contenuti e dati con l&#39;uso tipico per documenti normativi, rapporti di ricerca, richieste di sovvenzioni, appalti generali e altro ancora. Una singola azienda può avere più &quot;caveau&quot; che devono essere mantenuti separatamente.

I passaggi di alto livello per completare l&#39;integrazione sono:

* Attiva il tuo account amministrativo in Adobe Acrobat Sign (solo per i nuovi clienti).
* Create oggetti per monitorare la cronologia del ciclo di vita di un accordo nel Vault.
* Crea un nuovo profilo di sicurezza.
* Configura un gruppo in Adobe Acrobat Sign per contenere la proprietà [!DNL Veeva Vault] utente di integrazione.
* Creare campi documento ed interpretazioni.
* Configura le azioni web e aggiorna il ciclo di vita del documento.
* Crea la configurazione del tipo di documento utente e del ruolo utente.
* Collegate Veeva Vault a Adobe Acrobat Sign utilizzando il middleware.

>[!NOTE]
>
>L’amministratore di Adobe Sign deve eseguire i passaggi di configurazione di Adobe Acrobat Sign in Adobe Acrobat Sign.

## Configura [!DNL Veeva Vault] {#configure-veeva}

Per configurare [!DNL Veeva Vault] per l’integrazione con Adobe Acrobat Sign, è necessario implementare i passaggi elencati di seguito.

### Passaggio 1. Crea gruppo {#create-group}

Per configurare Adobe Acrobat Sign per [!DNL Vault], un nuovo gruppo denominato *Adobe Sign Admin Group* viene creato. Questo gruppo viene utilizzato per impostare la sicurezza a livello di campo del documento per i campi correlati a Adobe Acrobat Sign e deve includere *Profilo di integrazione Adobe Sign* per impostazione predefinita.

![Immagine dei dettagli dell’evento della firma](images/create-admin-group.png)

### Passaggio 2. Distribuire il pacchetto {#deploy-package}

[Distribuire il pacchetto](https://helpx.adobe.com/content/dam/help/en/sign-integrations-new/veeva-vault/PKG-AdobeSign-Integration-Veeva.zip) e segui i passaggi. Una volta distribuito, il pacchetto crea:

* Oggetti personalizzati: Oggetto Signature, oggetto Signature, oggetto evento Signature, oggetto Process Locker
* Layout di pagina dell’oggetto firma
* Layout di pagina dell’oggetto evento firma
* Layout di pagina dell’oggetto firmatario
* Layout di pagina dell’oggetto Process Locker
* Layout di pagina dell&#39;oggetto Registro attività di integrazione Adobe Sign
* Tipo di rendering Adobe Sign
* Tipo di rendering originale
* Campo condiviso signature__c
* Azione Web di Adobe Sign
* Annullare l’azione Web di Adobe Sign
* Insieme di autorizzazioni Azioni amministratore Adobe Sign
* Profilo di sicurezza di Adobe Sign Integration Profile
* Ruolo di amministratore Adobe Sign ruolo applicazione
* Gruppo di tipi di documento &quot;Adobe Sign documento&quot;
* Oggetto di registro delle attività di integrazione Adobe Sign

#### Oggetto Signature {#signature-object}

L’oggetto Firma viene creato per memorizzare le informazioni relative all’accordo. Un oggetto Signature è un database che contiene informazioni nei seguenti campi specifici:

**Campi oggetto firma**

| Campo | Etichetta | Tipo | Descrizione |
|:---|:---|:---|:------- | 
| external_id__c | ID accordo | Stringa (100) | Contiene l’ID accordo univoco del Adobe Acrobat Sign |
| file_hash__c | Hash file | Stringa (50) | Contiene il checksum md5 del file inviato a Adobe Acrobat Sign |
| name__v | Nome | Stringa (128) | Contiene il nome dell’accordo |
| sender_c | Mittente | Oggetto (utente) | Contiene il riferimento all’utente Vault che ha creato l’accordo. |
| signature_status__c | Stato firma | Stringa (75) | Conserva lo stato dell’accordo in Adobe Acrobat Sign |
| signature_type__c | Tipo firma | Stringa (20) | Conserva il tipo di firma dell’accordo in Adobe Acrobat Sign (SCRITTO o ESIGN) |
| start_date__c | Data di inizio | DateTime | Data in cui l’accordo è stato inviato per la firma |
| cancellation_date__c | Data di annullamento | DateTime | Consente di mantenere la data in cui l’accordo è stato annullato. |
| completed_date__c | Data di completamento | DateTime | Indica la data in cui l’accordo è stato completato. |
| viewable_rendition_used_c | Rendition visualizzabile utilizzata | Booleano | Flag che indica se il rendering visualizzabile è stato inviato per la firma. (per impostazione predefinita, è true) |
| plugin_version__c | Versione plug-in | Testo (10) | Viene utilizzato per consentire l’elaborazione appropriata di tutti gli accordi creati prima della distribuzione di una nuova versione 4.0. Nota: Dopo la distribuzione della versione dell&#39;applicazione Web 4.0 personalizzata, questo campo verrà impostato su 4.0 ogni volta che viene creato un record di firma. |
| external_environment__c | Ambiente esterno | Testo (20) | Contiene il nome dell’ambiente dell’Adobe Sign in cui è stato creato l’accordo. |

![Immagine dei dettagli dell’oggetto firma](images/signature-object-details.png)

#### Oggetto firmatario {#signatory-object}

L’oggetto firmatario viene creato per memorizzare le informazioni relative ai partecipanti di un accordo. Contiene informazioni nei seguenti campi specifici:

**Campi oggetto firmatario**

| Campo | Etichetta | Tipo | Descrizione |
|:---|:---|:---|:------- | 
| email__c | E-mail | Stringa (120) | Contiene l’ID accordo univoco del Adobe Acrobat Sign |
| external_id__c | ID partecipante | Stringa (80) | Contiene l’identificatore univoco del partecipante a Adobe Acrobat Sign |
| name__v | Nome | Stringa (128) | Contiene il nome del partecipante a Adobe Acrobat Sign |
| order__c | Ordine | Numero | Contiene il numero d’ordine del partecipante all’accordo Adobe Acrobat Sign |
| role_c | Ruolo | Stringa (30) | Conserva il ruolo dei partecipanti agli accordi Adobe Acrobat Sign |
| signature__c | Firma | Oggetto (firma) | Contiene il riferimento al record principale della firma |
| signature_status__c | Stato firma | Stringa (100) | Contiene lo stato del partecipante all’accordo Adobe Acrobat Sign |
| user__c | Utente | Oggetto (utente) | Contiene il riferimento al record utente del firmatario se il partecipante è un utente Vault |

![Immagine dei dettagli dei firmatari](images/signatory-object-details.png)

#### Oggetto evento firma {#signature-event}

L&#39;oggetto evento firma viene creato per memorizzare le informazioni relative agli eventi di un accordo. Contiene informazioni nei seguenti campi specifici:

Campi Oggetto evento firma

| Campo | Etichetta | Tipo | Descrizione |
|:---|:---|:---|:-------- | 
| acting_user_email__c | E-mail utente attivo | Stringa | Contiene l’e-mail dell’utente di Adobe Acrobat Sign che ha eseguito l’azione che ha causato la generazione dell’evento |
| acting_user_name__c | Nome utente attivo | Stringa | Contiene il nome dell&#39;utente di Adobe Acrobat Sign che ha eseguito l&#39;azione che ha causato la generazione dell&#39;evento |
| description__c | Descrizione | Stringa | Contiene la descrizione dell&#39;evento Adobe Acrobat Sign |
| event_date__c | Data evento | DateTime | Contiene la data e l&#39;ora dell&#39;evento Adobe Acrobat Sign |
| event_type__c | Tipo di evento | Stringa | Contiene il tipo di evento Adobe Acrobat Sign |
| name__v | Nome | Stringa | Nome evento generato automaticamente |
| participant_comment__c | Commento del partecipante | Stringa | Contiene il commento del partecipante a Adobe Acrobat Sign, se presente |
| participant_email__c | E-mail partecipante | Stringa | Contiene l’e-mail del partecipante a Adobe Acrobat Sign |
| participant_role_c | Ruolo partecipante | Stringa | Il ruolo del partecipante a Adobe Acrobat Sign |
| signature__c | Firma | Oggetto (firma) | Contiene il riferimento al record principale della firma |
| external_id__c | ID esterno | Testo (200) | Contiene l’identificatore evento accordo generato da Adobe Sign. |

![Immagine](images/signature-event-object-details.png)

#### Oggetto Process Locker {#process-locker}

Viene creato un oggetto Process Locker per bloccare il processo di integrazione di Adobe Acrobat Sign. Non richiede alcun campo personalizzato.

![Immagine dei dettagli dell’evento della firma](images/process-locker-details.png)

#### Oggetto Registro attività integrazione Adobe Sign {#task-log}

Create Adobe Sign Integration Task Log (as_int_task_log__c). È un oggetto con un volume elevato che viene utilizzato per tracciare l&#39;esecuzione di AgreementsEventsSynchronizerJob e AgreementsEventsProcessingJob.
AgreementsEventsSynchronizerJob: Questa attività garantisce che tutti gli eventi degli accordi mancanti da Adobe Sign siano creati come eventi di firma attivi in Vault per tutte le firme create in Vault negli ultimi N giorni.
AgreementsEventsProcessingJob: Questa attività garantisce che tutti i documenti con record evento firma attivi vengano elaborati in base al tipo di evento.

Campi Oggetto Registro Attività Integrazione Adobe Sign

| Campo | Etichetta | Tipo | Descrizione |
|:--|:--|:--|:---------| 
| start_date__c | Data di inizio | DateTime | Data di inizio attività |
| end_date__c | Data di fine | DateTime | Data di fine attività |
| task_status__c | Stato attività | Lista Picklist | Contiene lo stato delle attività: <br /> Completato (task_completed__c) Completato con errori (task_completed_with_errors__c) Non riuscito (task_failed__c) |
| task_type__c | Tipo di attività | Lista Picklist | Contiene il tipo di attività: <br><br> Sincronizzazione degli eventi degli accordi (agreements_events_synchronization__c) Elaborazione degli eventi degli accordi (agreements_events_processing__c) |
| messages_c | Messaggio | Lunga (32000) | Contiene il messaggio dell&#39;attività |

![Immagine dei dettagli dell&#39;oggetto registro attività](images/task-log.png)

![Immagine dei campi oggetto registro attività](images/task-log-fields.png)

Gli oggetti Signature, Signatory, Signature Event, Process Locker e Task Log che fanno parte del pacchetto di distribuzione hanno la proprietà &quot;Audit data changes for this object&quot; attivata per impostazione predefinita.

**Nota:** È possibile fare in modo che il Vault acquisisca le modifiche dei dati dei record di oggetto nei registri di controllo abilitando l&#39;impostazione di verifica delle modifiche dei dati. Questa impostazione è disattivata per impostazione predefinita. Dopo aver attivato questa impostazione e creato i record, non è più possibile disattivarla. Se questa impostazione è disattivata e sono presenti dei record, solo il proprietario dell’archivio può aggiornarla.

#### **Visualizzare i partecipanti e la cronologia per l’oggetto firma** {#display-participants-history}

L&#39;oggetto Signature che fa parte del pacchetto di distribuzione viene fornito con la proprietà [Layout di pagina Dettagli firma](https://vvtechpartner-adobe-rim.veevavault.com/ui/#admin/content_setup/object_schema/pagelayout?t=signature__c&amp;d=signature_detail_page_layout__c). Il layout di pagina contiene sezioni per i partecipanti e la cronologia.

* Il *Partecipanti* la sezione Oggetti correlati è configurata come nell&#39;immagine seguente.

   ![Immagine](images/edit-related-objects.png)

* Potete modificare le colonne da visualizzare per i partecipanti, come illustrato di seguito.

   ![Immagine](images/set-columns-to-display.png)

* Il *Storia* la sezione Oggetti correlati è configurata come nell&#39;immagine seguente.

   ![Immagine](images/edit-related-object-in-history.png)

* Potete modificare le colonne da visualizzare per la Cronologia, come illustrato di seguito.

   ![Immagine](images/select-columns-to-display.png)

#### **Visualizzare i partecipanti e la cronologia di audit per il documento Adobe Acrobat Sign** {#view-participants-audit-history}

* Per visualizzare i partecipanti e la cronologia di audit per il documento Adobe Acrobat Sign, seleziona il collegamento nella sezione &quot;Adobe firma&quot; del documento.

   ![Immagine](images/view-participants-audit-history.png)

* La pagina che si apre visualizza i partecipanti e la cronologia del documento Adobe Acrobat Sign, come illustrato di seguito.

   ![Immagine](images/participants-and-history.png)

* Visualizza la traccia di verifica per la firma come illustrato di seguito.

   ![Immagine](images/audit-trail.png)

### Passaggio 3. Configurazione dei profili di protezione {#security-profiles}

La distribuzione del pacchetto riuscita al Passaggio 2 crea il profilo di integrazione Adobe Sign. Il profilo di integrazione Adobe Sign viene assegnato all’account di sistema e viene utilizzato dall’integrazione quando si chiamano le API Vault. Questo profilo consente le autorizzazioni per:

* API di Vault
* Lettura, creazione, modifica ed eliminazione: Oggetti Firma, Firma, Eventi firma e Blocco processi

È necessario aggiornare Adobe Sign Admin Group (creato al passaggio 1) impostando il profilo di sicurezza incluso su Adobe Sign Integration Profile, come illustrato nell&#39;immagine seguente.

![Immagine dei dettagli dell’evento della firma](images/security-profiles.png)

### Passaggio 4. Crea utente {#create-user}

L’account di sistema Vault che utilizza l’integrazione con Adobe Acrobat Sign deve:

* Disporre di un profilo di integrazione Adobe Sign
* Avere un profilo di sicurezza
* Disporre di criteri di sicurezza specifici che disabilitano la scadenza della password
* Diventa membro del gruppo di amministrazione di Adobe Sign.

A tale scopo, effettua le seguenti operazioni:

1. Crea un account di sistema Vault per l&#39;integrazione con Adobe Acrobat Sign.

   ![Immagine dei dettagli dell’evento della firma](images/create-user.png)

2. Aggiungi l’utente al gruppo di amministrazione di Adobe Sign.

   ![Immagine dei dettagli dell’evento della firma](images/add-user.png)

### Passaggio 5. Configurare il gruppo di tipi di documento {#create-document-type-group}

Quando distribuisci il pacchetto Adobe Acrobat Sign, viene creato un record Gruppo tipi di documento denominato &quot;Adobe Sign documento&quot;.

![Immagine di gruppi di tipi di documento](images/document-type-groups.png)

È necessario aggiungere questo gruppo di tipi di documento per tutte le classificazioni di documenti idonee per la Adobe Acrobat Sign. Poiché la proprietà del gruppo di tipi di documento non viene ereditata dal tipo al sottotipo né dal sottotipo al livello di classificazione, deve essere impostata per ogni classificazione del documento idonea per Adobe Acrobat Sign.

![Immagine dei dettagli di modifica del documento](images/document-edit-details.png)

**Nota:** Se l’oggetto Impostazione ruolo utente non contiene il campo che fa riferimento all’oggetto Gruppo tipo di documento, è necessario aggiungere il campo. A tale scopo, passare a **[!UICONTROL Oggetto]** > **[!UICONTROL Impostazione ruolo utente]** > **[!UICONTROL Campi]** e completare i passaggi richiesti, come illustrato nell&#39;immagine seguente.

![Immagine della configurazione del ruolo utente](images/create-setup-field.png)

![Immagine del tipo di documento](images/document-type.png)

### Passaggio 6. Crea impostazione ruolo utente {#create-user-role-setup}

Una volta configurati correttamente i cicli di vita, il sistema deve garantire che l’utente amministratore di Adobe Sign sia aggiunto da DAC a tutti i documenti idonei per l’elaborazione di Adobe Acrobat Sign. A tale scopo, viene creato il record Impostazione ruolo utente appropriato che specifica:

* Gruppo di tipi di documento come documento Adobe Sign
* Ruolo dell’applicazione come ruolo di amministratore Adobe Sign
* Utente di integrazione

![Immagine della configurazione del ruolo utente](images/user-role-setup.png)

### Passaggio 7. Imposta campi documento {#create-fields}

La distribuzione del pacchetto crea il nuovo campo documento condiviso seguente necessario per stabilire l&#39;integrazione:

* Firma (signature__c)

![Immagine](images/document-fields.png)

Per configurare i campi documento:

1. Vai alla scheda Configuration e seleziona **[!UICONTROL Campi documento]** > **[!UICONTROL Campi condivisi]**.
1. Nel campo Sezione di visualizzazione, seleziona **[!UICONTROL Sezione Crea visualizzazione]** e assegnare **[!UICONTROL Adobe firma]** come etichetta Sezione.

   ![Immagine](images/create-display-section.png)

1. Per i campi del documento condiviso (signature__c), aggiorna la sezione dell’interfaccia utente con **[!UICONTROL Adobe firma]** come etichetta di sezione.
1. Aggiungi i due campi condivisi a tutti i tipi di documenti idonei per la firma Adobe Acrobat. A tale scopo, nella pagina Documento di base, seleziona **[!UICONTROL Aggiungi]** > **[!UICONTROL Campo condiviso esistente]** dall&#39;angolo superiore destro.

   ![Immagine](images/create-document-fields.png)

   ![Immagine](images/add-existing-fields.png)

   ![Immagine](images/use-shared-fields.png)

1. Entrambi i campi devono avere una protezione specifica che consente solo ai membri del gruppo di amministratori di Adobe Sign di aggiornare i propri valori.

   ![Immagine](images/security-overrides.png)

Disattiva le sovrapposizioni vettoriali (disable_vault_overlays__v) è un campo condiviso esistente. Facoltativamente, il campo può avere una protezione specifica che consente solo ai membri del gruppo di amministrazione di Adobe Sign di aggiornarne il valore.

### Passaggio 8. Dichiarare le interpretazioni dei documenti {#declare-renditions}

Il nuovo tipo di rendering chiamato *Adobe Sign rendering (adobe_sign_rendition__c)* viene utilizzato dall’integrazione Vault per caricare documenti PDF firmati in Adobe Acrobat Sign. È necessario dichiarare il rendering Adobe Sign per ogni tipo di documento idoneo per la firma Adobe Acrobat.

![Immagine dei tipi di rendering](images/rendition-type.png)

![Immagine](images/edit-details-clinical.png)

Il nuovo tipo di rendering chiamato *Rendition originale* (original_rendition__c) viene utilizzato dall’integrazione Vault come nome del rendering da utilizzare per memorizzare il rendering visualizzabile originale se il documento firmato viene importato come rendering visualizzabile.

È necessario dichiarare il rendering originale per ogni tipo di documento idoneo per la firma Adobe Acrobat.

![Immagine](images/original-rendition.png)

Facoltativamente, l’archivio può avere un nuovo tipo di rendering Adobe Rendition Audit Trail (adobe_audit_trail_rendition__c), che viene utilizzato dall’integrazione Vault per memorizzare il report Adobe dell’audit trail.

Segui i passaggi riportati di seguito per configurare il rendering dell’audit trail di Adobe:

1. Vai a **Tipo di rendering** > **Crea nuovo tipo di rendering**.
Create il nuovo tipo di rendering come Rendition della traccia di revisione (adobe_audit_trail_rendition__c).

   ![Immagine](images/audit-trail-rendition-setup-1.png)

1. Per visualizzare e scaricare il rendering Adobe della traccia di audit per il documento, dichiarare *Adobe rendering traccia di audit* per ogni tipo di documento idoneo per Adobe Acrobat Signature.

   ![Immagine](images/audit-trail-rendition-setup-2.png)

**Nota**: Puoi scegliere di allegare il report di audit all’interpretazione firmata attivando **[!UICONTROL Allega report di audit a rendering firmato]** e visualizzare anche il rendering abilitando ****[!UICONTROL Visualizzazione del rendering Acrobat Sign]**** nelle impostazioni dell’interfaccia utente dell’amministratore.

![Immagine](images/audit-trail-rendition-setup-3.png)

Quando un utente opta per un accordo di firma digitale con le impostazioni sopra riportate, viene visualizzato un messaggio (come illustrato di seguito) che indica che Adobe Acrobat Sign utilizza PDF Portfoli per combinare i report di PDF con firma digitale e audit trail.

Per visualizzare il contenuto del documento insieme alla firma digitale e all’audit trail, non selezionare &quot;Allega report di audit a rendering firmato&quot; con &quot;Visualizza rendering Acrobat Sign&quot; nell’interfaccia utente dell’amministratore per la firma digitale.

Puoi utilizzare l’opzione Adobe rendering traccia di revisione per scaricare o visualizzare l’Adobe traccia di revisione come un’interpretazione separata.

![Immagine](images/audit-trail-rendition-setup-4.png)

### Passaggio 9. Aggiorna azioni Web {#web-actions}

L&#39;integrazione di Adobe Acrobat Sign e Vault richiede la creazione e la configurazione di due azioni Web:

* **Creare Adobe Sign**: Crea o visualizza un accordo Adobe Acrobat Sign.

   Tipo: Document Target: Visualizza all’interno delle credenziali di archivio: Abilita le credenziali post-sessione tramite URL post-messaggio: <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

   ![Immagine di create Adobe Sign](images/create-adobe-sign.png)

* **Annulla Adobe Sign**: Annulla un accordo esistente in Adobe Acrobat Sign e ripristina lo stato iniziale di un documento.

   Tipo: Document Target: Visualizza all’interno delle credenziali di archivio: Abilita le credenziali post-sessione tramite URL post-messaggio: : <https://api.na1.adobesign.com/api/gateway/veevavaultintsvc/partner/agreement/cancel?docId=${Document.id}&majVer=${Document.major_version_number__v}&minVer=${Document.minor_version_number__v}&vaultid=${Vault.id}&useWaitPage=true>

   ![Immagine di Annulla Adobe Sign](images/cancel-adobe-sign.png)

### Passaggio 10. Aggiornamento del ciclo di vita dei documenti {#document-lifecycle}

Per ogni tipo di documento idoneo per la firma di Adobi, è necessario aggiornare il ciclo di vita del documento corrispondente aggiungendo nuovi stati e ruoli del ciclo di vita.

Il ciclo di vita degli accordi Adobe Acrobat Sign presenta i seguenti stati:

* BOZZA
* AUTHORING o DOCUMENTS_NOT_YET_PROCESSED
* OUT_FOR_SIGNATURE o OUT_FOR_approval
* FIRMATO O APPROVATO
* ANNULLATO
* SCADUTO

Per aggiornare il ciclo di vita del documento, effettua le seguenti operazioni:

1. Aggiungi il ruolo Ciclo di vita. Il ruolo dell’applicazione di amministrazione Adobe Sign deve essere aggiunto a tutti i cicli di vita utilizzati dai documenti idonei per la firma Adobe Acrobat, come illustrato di seguito.

   ![Immagine dei ruoli di amministratore del ciclo di vita](images/document-lifecycle-admin-role.png)

   Il ruolo di amministratore deve essere creato con le seguenti opzioni:

   * Abilitato Controllo accesso dinamico.
   * Regole di condivisione dei documenti che includono solo il gruppo di tipi di documento, come illustrato nell&#39;immagine seguente.

   ![Immagine della regola di condivisione di adobe sign](images/adobe-sign-sharing-rule.png)

2. Creare gli stati del ciclo di vita. A tale scopo, passare a **[!UICONTROL Impostazioni]** > **[!UICONTROL Configurazione]** > **[!UICONTROL Cicli di vita documento]** > **[!UICONTROL Cicli di vita generali]** > **[!UICONTROL Stati]** > **[!UICONTROL Crea]**. Quindi, creare i seguenti stati:

   * In Adobe Sign Draft

   ![Immagine della regola di condivisione di adobe sign](images/create-draft-state.png)

   * In Adobe Sign Authoring

   ![Immagine della regola di condivisione di adobe sign](images/create-authoring-state.png)

   * In Adobe firma

   ![Immagine della regola di condivisione di adobe sign](images/create-signing-state.png)

3. Aggiungi le azioni utente agli stati elencati di seguito.

   Quando un documento di archivio viene inviato a Adobe Acrobat Sign, il suo stato deve corrispondere allo stato in cui si trova l’accordo. A tale scopo, aggiungi i seguenti stati in ogni ciclo di vita utilizzato dai documenti idonei per la firma degli Adobi:

   * **Prima della firma dell’Adobe** (recensito): Si tratta di un nome segnaposto per lo stato da cui è possibile inviare il documento a Adobe Acrobat Sign. In base al tipo di documento, può essere Bozza o Revisionato. L&#39;etichetta dello stato del documento può essere personalizzata in base alle esigenze del cliente. Prima di Adobe lo stato della firma deve definire due azioni utente:

      * Azione che modifica lo stato del documento in *In Adobe Sign Draft* state. Il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento per qualsiasi ciclo di vita.
      * Azione che chiama l&#39;azione Web &quot;Adobe Sign&quot;. Questo stato deve avere una protezione che consenta al ruolo di amministratore di Adobe Sign di: visualizza il documento, visualizza il contenuto, modifica i campi, modifica le relazioni, scarica l’origine, gestisci le interpretazioni visualizzabili e modifica lo stato.

      ![Immagine dello stato del ciclo di vita 1](images/lifecycle-state1.png)

      * Modifica *Revisionato* sicurezza atomica dello stato impostando *In Adobe Sign Draft* per impostazione predefinita, l&#39;opzione Nascosto e l&#39;opzione Esegui solo per *Ruolo di amministratore Adobe Sign*.
      **Nota:** Se *Ruolo di amministratore Adobe Sign* non fa parte di *Sicurezza atomica:azioni degli utenti*, Aggiungi **[!UICONTROL Ruolo di amministratore Adobe Sign]** selezionando **[!UICONTROL Modifica]**> **[!UICONTROL Sostituzione ruolo]**. Quindi, aggiungi **Ruolo di amministratore Adobe Sign** per *Revisionato* Stato.

      ![Immagine](images/lifecycle-state-reviewed.png)
      ![Immagine](images/lifecycle-state-reviewed-1.png)
      ![Immagine](images/lifecycle-state-reviewed-2.png)

   * **In Adobe Sign Draft**: Si tratta di un nome segnaposto per lo stato che indica che il documento è già caricato in Adobe Acrobat Sign e che il suo accordo è in stato BOZZA. È uno stato obbligatorio. Questo stato deve definire cinque azioni utente:

      * Azione che modifica lo stato del documento in *In Adobe Sign Authoring* state. Il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento per qualsiasi ciclo di vita.
      * Azione che modifica lo stato del documento in *In Adobe stato di firma*. Il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento per qualsiasi ciclo di vita.
      * Azione che modifica lo stato del documento in *Adobe Sign annullato* state. Il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento per qualsiasi ciclo di vita.
      * Azione che chiama Azione Web *Adobe Sign*.
      * Azione che chiama Azione Web *Annulla Adobe Sign*. Questo stato deve avere una sicurezza che consenta al ruolo di amministratore di Adobe Sign di: visualizza il documento, visualizza il contenuto, modifica i campi, modifica le relazioni, scarica l’origine, gestisci le interpretazioni visualizzabili e modifica lo stato.

      ![Immagine dello stato del ciclo di vita 2](images/lifecycle-state2.png)

      * Modifica *In Adobe Sign Draft* sicurezza atomica di stato: azioni *Adobe Sign annullato*, *In Adobe Sign Authoring*, *In Adobe firma* deve essere nascosta per tutti tranne che per il ruolo di amministratore di Adobe Sign
      **Nota:** Se *Ruolo di amministratore Adobe Sign* non fa parte di *Sicurezza atomica: Azioni utente*, add **[!UICONTROL Ruolo di amministratore Adobe Sign]** selezionando **[!UICONTROL Modifica]** > **[!UICONTROL Sostituzione ruolo]**. Quindi, aggiungi **[!UICONTROL Ruolo di amministratore Adobe Sign]** ruolo *In Adobe Sign Draft* Stato.

      ![Immagine](images/atomic-security.png)

   * **In Adobe Sign Authoring**: Si tratta di un nome segnaposto per lo stato che indica che il documento è già caricato in Adobe Acrobat Sign e che il suo accordo è in stato AUTHORING o DOCUMENTS_NOT_YET_PROCESSED. È uno stato obbligatorio. Questo stato deve avere quattro azioni utente definite:

      * Azione che modifica lo stato del documento in Adobe Sign annullato. Il nome di questa azione utente deve essere uguale per tutti i tipi di documento, indipendentemente dal ciclo di vita.
      * Azione che modifica lo stato del documento in Adobe stato di firma. Il nome di questa azione utente deve essere uguale per tutti i tipi di documento, indipendentemente dal ciclo di vita.
      * Azione che chiama l&#39;azione Web &quot;Adobe Sign&quot;
      * Azione che chiama l’azione Web &quot;Annulla Adobe Sign&quot;. Questo stato deve avere una protezione che consenta al ruolo di amministratore di Adobe Sign di: visualizza il documento, visualizza il contenuto, modifica i campi, modifica le relazioni, scarica l’origine, gestisci le interpretazioni visualizzabili e modifica lo stato.

      ![Immagine dello stato del ciclo di vita 3](images/lifecycle-state3.png)

      * Modifica *In Adobe Sign Authoring* sicurezza atomica di stato: azioni *Adobe Sign annullato* e *In Adobe firma* deve essere nascosta per tutti tranne che per il ruolo di amministratore di Adobe Sign
      **Nota:** Se *Ruolo di amministratore Adobe Sign* non fa parte di *Sicurezza atomica: Azioni utente*, add **[!UICONTROL Ruolo di amministratore Adobe Sign]** selezionando **[!UICONTROL Modifica]** > **[!UICONTROL Sostituzione ruolo]**. Quindi, aggiungi **[!UICONTROL Ruolo di amministratore Adobe Sign]** ruolo *In Adobe Sign Authoring* Stato.

      ![Immagine](images/adobe-sing-authoring.png)

   * **In Adobe firma**: Si tratta di un nome segnaposto per lo stato che indica che il documento viene caricato in Adobe Acrobat Sign e che il relativo accordo è già stato inviato ai partecipanti (stato OUT_FOR_SIGNATURE o OUT_FOR_approval). È uno stato obbligatorio. Questo stato deve avere cinque azioni utente definite:

      * Azione che modifica lo stato del documento in Adobe Sign annullato. Lo stato di destinazione di questa azione può essere qualsiasi esigenza del cliente e può essere diverso per diversi tipi. Il nome di questa azione utente deve essere uguale per tutti i tipi di documento, indipendentemente dal ciclo di vita.
      * Azione che modifica lo stato del documento in Adobe Sign stato rifiutato. Lo stato di destinazione di questa azione può essere qualsiasi esigenza del cliente e può essere diverso per diversi tipi. Il nome di questa azione utente deve essere uguale per tutti i tipi di documento, indipendentemente dal ciclo di vita.
      * Azione che modifica lo stato del documento in Adobe dello stato Firmato. Lo stato di destinazione di questa azione può essere qualsiasi esigenza del cliente e può essere diverso per diversi tipi. Tuttavia, il nome di questa azione utente deve essere lo stesso per tutti i tipi di documento, indipendentemente dal ciclo di vita.
      * Azione che chiama Azione Web *Adobe Sign*.
      * Azione che chiama Azione Web *Annulla Adobe Sign*. Questo stato deve avere una protezione che consenta al ruolo di amministratore di Adobe Sign di: visualizza il documento, visualizza il contenuto, modifica i campi, modifica le relazioni, scarica l’origine, gestisci le interpretazioni visualizzabili e modifica lo stato.

      ![Immagine dello stato del ciclo di vita 4](images/lifecycle-state4.png)

      * Modifica *In Adobe firma* sicurezza atomica di stato: azioni *Adobe Sign annullato*, *Adobe Sign rifiutata* e *Adobe firmato* deve essere nascosta per tutti tranne che per il ruolo di amministratore di Adobe Sign
      **Nota:** Se *Ruolo di amministratore Adobe Sign* non fa parte di *Sicurezza atomica: Azioni utente*, add **[!UICONTROL Ruolo di amministratore Adobe Sign]** selezionando **[!UICONTROL Modifica]** > **[!UICONTROL Sostituzione ruolo]**. Quindi, aggiungi **[!UICONTROL Ruolo di amministratore Adobe Sign]** ruolo *In Adobe firma* Stato.

      ![Immagine](images/in-adobe-signing-2.png)

      * **Adobe firmato (approvato)**: Si tratta di un nome segnaposto per lo stato che indica che il documento viene caricato in Adobe Acrobat Sign e che il suo accordo è stato completato (stato FIRMATO o APPROVATO). È uno stato obbligatorio e può essere uno stato del ciclo di vita esistente, come Approvato.
Questo stato non richiede azioni da parte dell&#39;utente. Deve disporre di una protezione che consenta al ruolo di amministratore di Adobe Sign di: visualizza documenti, visualizza contenuti e modifica campi.

   Il diagramma seguente illustra le mappature tra gli stati dell’accordo Adobe Acrobat Sign e del documento Vault, in cui lo stato Prima della firma dell’Adobe è Bozza.

   ![Immagine](images/sign-vault-mappings.png)

### Passaggio 11. Aggiungere lo stage Adobe Sign ai gruppi di Lifecycle Stage Generali

![Immagine](images/add-adobe-sign-stage.png)

### Passaggio 12. Impostare le autorizzazioni per il ruolo utente nello stato del ciclo di vita

È necessario impostare autorizzazioni appropriate per ogni ruolo utente nello stato del ciclo di vita, come illustrato nell&#39;immagine seguente.

![Immagine](images/set-user-role-permissions.png)

### Passaggio 13. Configurare la sicurezza atomica in base allo stato del documento e al ruolo utente

![Immagine](images/set-atomic-security.png)

### Passaggio 14. Creazione di messaggi di documento per Adobe Sign Annulla

![Immagine](images/create-cancel-message.png)

## Connetti [!DNL Veeva Vault] per Adobe Acrobat Sign con il middleware {#connect-middleware}

Dopo aver completato la configurazione per [!DNL Veeva Vault] e l’account amministratore di Adobe Acrobat Sign, l’amministratore deve creare una connessione tra i due account utilizzando il middleware. Il [!DNL Veeva Vault] e la connessione all&#39;account Adobe Acrobat Sign viene avviata da Adobe Acrobat Sign Identity e quindi viene utilizzata per memorizzare[!DNL Veeva Vault] identità.
Per garantire la sicurezza e la stabilità del sistema, l&#39;amministratore deve utilizzare una [!DNL Veeva Vault] account di sistema/servizio/utilità, ad esempio `adobe.for.veeva@xyz.com`, anziché un account utente personale, ad esempio `bob.smith@xyz.com`.

L’amministratore dell’account Adobe Acrobat Sign deve seguire i passaggi riportati di seguito per connettersi [!DNL Veeva Vault] per Adobe Acrobat Sign con middleware:

1. Vai alla [Adobe Acrobat Sign per [!DNL Veeva Vault] Home page](https://static.adobesigncdn.com/veevavaultintsvc/index.html).
1. Seleziona **[!UICONTROL Login]** dall&#39;angolo superiore destro.

   ![Immagine di accesso middleware](images/middleware_login.png)

1. Per autorizzare il livello di accesso all&#39;applicazione, seleziona Acrobat Sign ambito OAuth come **[!UICONTROL RESOCONTO]** o **[!UICONTROL GRUPPO]**. Quindi, seleziona **[!UICONTROL Autorizza]**.

   ![Immagine](images/middleware_oauth.png)

1. Nella pagina di accesso di Adobe Acrobat Sign visualizzata, immetti l’indirizzo e-mail e la password dell’amministratore dell’account, quindi seleziona **[!UICONTROL Accedi]**.

   ![Immagine](images/middleware-signin.png)

   Dopo aver effettuato l’accesso, la pagina visualizza l’ID e-mail associato e la scheda Impostazioni, come illustrato di seguito.

   ![Immagine](images/middleware_settings.png)

1. Selezionate la proprietà **[!UICONTROL Impostazioni]** tab.

   La pagina Impostazioni visualizza le connessioni disponibili e mostra *Nessuna connessione disponibile* in caso di prima configurazione della connessione, come illustrato di seguito.

   ![Immagine](images/middleware_newconnection.png)

1. Seleziona **[!UICONTROL Aggiungi connessione]** per aggiungere una nuova connessione.

1. Nella finestra di dialogo Aggiungi connessione che si apre, fornire i dettagli necessari, tra cui [!DNL Veeva Vault] credenziali.

   Le credenziali Adobe Acrobat Sign vengono popolate automaticamente dall’accesso Adobe Sign iniziale.

   ![Immagine](images/middleware_addconnection.png)

1. Seleziona **[!UICONTROL Convalidare]** per convalidare i dettagli dell’account.

   Al termine della convalida, viene visualizzata una notifica &quot;L’utente è stato convalidato correttamente&quot;, come illustrato di seguito.

   ![Immagine](images/middleware_validated.png)

1. Per limitare l&#39;utilizzo a un determinato gruppo di Adobe Acrobat Sign, espandere la proprietà **[!UICONTROL Gruppo]** elenco a discesa e seleziona uno dei gruppi disponibili.

   ![Immagine](images/middleware_group.png)

1. Per allegare il report di audit all’interpretazione firmata, seleziona la casella di controllo **[!UICONTROL Allega report di audit a rendering firmato]**.

   ![Immagine](images/add-audit-report.png)

1. Per consentire il provisioning automatico degli utenti in Adobe Acrobat Sign, seleziona la casella di controllo **[!UICONTROL Fornitura automatica per gli utenti di Sign]**.

   **Nota:** Il provisioning automatico dei nuovi utenti di Adobe Acrobat Sign funziona solo se è stato abilitato a livello di account Adobe Acrobat Sign in Adobe Acrobat Sign, oltre all’attivazione **[!UICONTROL Fornitura automatica per gli utenti di Sign]** per la[!DNL Veeva Vault] Integrazione con Adobe Acrobat Sign come illustrato di seguito dall’amministratore dell’account Adobe Acrobat Sign.

   ![Immagine](images/allow-auto-provisioning.png)

1. Per configurare la visualizzazione di Adobe Sign rendering in Veeva anziché nella versione originale, selezionate la casella di controllo **[!UICONTROL Visualizzazione del rendering Acrobat Sign]**.

   ![Immagine](images/edit-connection-dispplay-adobe-sign-rendition.png)

1. Seleziona **[!UICONTROL Salva]** per salvare la nuova connessione.

   La nuova connessione viene visualizzata nella scheda Impostazioni e mostra l’integrazione riuscita tra [!DNL Veeva Vault] e Adobe Acrobat Sign.

   ![Immagine](images/middleware_setup.png)

