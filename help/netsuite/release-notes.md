---
title: Note sulla release di Adobe Sign per NetSuite
description: 'Learn about the new features and changes that are included in the current release of the Adobe Sign integration for NetSuite.  '
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
source-git-commit: 27610773d47a947dbfa1deb3f594667406a9aefb
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 5%

---


# Adobe Sign for NetSuite Release Notes

## Aggiorna al pacchetto v4.0.4

4.0.4 è completamente adattato per utilizzare domini specifici dell&#39;account per tutto il traffico appena generato.

L&#39;icona di Adobe Sign è stata aggiornata alla nuova immagine.

## Versioni precedenti

### Adobe Sign per NetSuite 4.0.4

4.0.4 è completamente adattato per utilizzare domini specifici dell&#39;account per tutto il traffico appena generato.

The Adobe Sign icon has been updated to the new graphic.

### Adobe Sign per NetSuite 4.0.2

Assegnato a **Adobe Sign** (da *Servizi di Adobe Document Cloud eSign*)\
È ora possibile vedere *Adobe Sign* dove è stato visto in precedenza *Adobe eSign Services* come prova della riassegnazione.

### Adobe Sign per NetSuite 4.0.1

A causa di un errore di regressione API introdotto quando NetSuite ha eseguito il relativo aggiornamento della piattaforma, è stato rilasciato un nuovo pacchetto (v4.0.1).

I clienti vengono incoraggiati ad aggiornare il nuovo pacchetto.

### Adobe Sign per NetSuite 4.0

**Aggiunta di provisioning automatico degli utenti tramite NetSuite**

È stata aggiunta una nuova preferenza personalizzata per v4.0. Se abilitato, gli utenti che inviano contratti in NetSuite vengono automaticamente dotati di un account utente dei servizi eSign di Adobe Document Cloud.

**Certificato con &#39;Built for NetSuite&#39;**

Questa versione ha ottenuto la certificazione &quot;Built for NetSuite&quot; e soddisfa tutte le procedure ottimali più recenti per la progettazione di NetSuite.

**Assegnato ai servizi Adobe Document Cloud eSign (da EchoSign)**

Potete vedere Adobe Document Cloud eSign Services (o Adobe eSign Services per breve tempo) dove in precedenza avete visto Adobe EchoSign come prova del ribilanciamento.

**Implemented enhanced security with OAuth**

Per migliorare la sicurezza dei dati, i servizi eSign utilizzano ora OAuth 2.0 per autenticare l&#39;account dei servizi Adobe Document Cloud eSign in NetSuite. Questo nuovo protocollo consente a NetSuite di parlare con i servizi eSign senza richiedere la password dei servizi eSign. Poiché le informazioni riservate non vengono condivise direttamente tra le applicazioni, la probabilità che il tuo account venga compromesso è più bassa. Questo miglioramento non incide sull&#39;implementazione, ma è necessario eseguire una configurazione unica per autorizzare il pacchetto NetSuite a comunicare con Adobe Document Cloud. Questa operazione viene eseguita durante il processo di installazione. For customers upgrading from a previous version of the package—v3.5.9 and prior—the API key previously used is replaced by an OAuth token generated during the authorization process.

**Migrazione dei servizi eSign dalle API SOAP alle API REST eseguita**

Per migliorare l&#39;efficienza, la flessibilità e la velocità di elaborazione, i servizi Adobe Document Cloud eSign e, di conseguenza, l&#39;integrazione v4.0 per NetSuite sono stati migrati da API basate su SOAP a API basate su REST.

### Adobe Sign per NetSuite 3.0

**Advanced Participant Roles - Approver**

* One or more recipients can be marked as approver(s) in an agreement
* Gli approvatori devono esaminare e approvare il documento
* Gli approvatori possono anche essere tenuti a compilare i dati nell&#39;accordo prima di approvare

**Anteprima dei campi del documento o trascinamento della selezione prima dell&#39;invio**

Visualizza in anteprima i campi del contratto o trascina i campi del modulo prima di inviare la firma

**Invia promemoria al firmatario corrente**

Invia promemoria immediato al firmatario corrente

**Criteri di autenticazione firma avanzata**

* **Autenticazione basata sulle conoscenze:** rispondere alle domande per verificare l&#39;identità del firmatario
   * Richiede ai firmatari di provare la propria identità rispondendo alle domande di centinaia di banche dati pubbliche e commerciali
   * Il nome nella firma è tratto dal nome autenticato dell’utente e non può essere modificato al momento della firma
   * Con tecnologia RSA
   * KBA usage is limited per account, per month. Contatta le vendite per ulteriori informazioni.

* **Identità Web:** Accedere con Facebook, LinkedIn, Google o altri servizi Web di terze parti prima di firmare.

   * Il firmatario può firmare solo dopo aver verificato la propria identità utilizzando un servizio Web di terze parti.
   * Il nome nella firma viene preso dal servizio Web pro!le dell&#39;utente e non può essere modificato al momento della firma
   * Audit trail acquisisce i dettagli della verifica dell&#39;identità

* **Password una volta**
   * Applicare metodi di autenticazione per i sottoscrittori interni o esterni o per tutti i sottoscrittori. I firmatari esterni devono utilizzare una password o l&#39;autenticazione basata su conoscenze mentre i firmatari interni non utilizzano

**Preferenze personalizzate aggiuntive**

* Aggiungi PDF firmato come collegamento all&#39;URL o come allegato ospitato in NetSuite
* Aggiungi traccia di controllo al record del contratto a un contratto$er firmato
* Utilizza il contatto transazione come firmatario per impostazione predefinita, anziché come messaggio di posta elettronica del cliente
* Concedi ai mittenti l&#39;opzione per contrassegnare i destinatari come approvatori

**File di transazione**

È possibile selezionare i file da allegare dalla transazione corrente con il nuovo elenco a discesa File di transazione.

**Certificazione Adobe PDF per tutti i documenti EchoSign**

* Tutti i file PDF inviati o scaricati da EchoSign sono certificati con un certificato digitale Adobe EchoSign
* Acrobat o Reader visualizza la certificazione che garantisce che il documento non sia stato alterato per un&#39;ulteriore attendibilità e tranquillità

**Raccolta dei documenti di supporto**

* I mittenti possono raccogliere ulteriori documenti giustificativi dai sottoscrittori durante la firma, ad esempio la patente di guida, il certificato commerciale e altro ancora.
* Collected documents become part of the official record of the signed agreement

**Campi di dati condizionali**

* Definire la logica condizionale per i campi dell&#39;accordo
* Le condizioni possono essere basate su valori per uno o più campi del contratto
* Conditions can be de!ned through the drag-and-drop forms authoring UI or through text-tags
* Al firmatario vengono presentati i campi appropriati durante la firma di un documento in base alle condizioni de!ned

**Ulteriori miglioramenti per i campi modulo EchoSign**

* Menu a discesa
* Mascheramento sul campo
* Pulsanti di scelta
* Crea tag di testo più brevi per mantenere la struttura del documento
