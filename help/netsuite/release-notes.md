---
title: Note sulla release di Adobe Sign per NetSuite
description: 'Informazioni sulle nuove funzionalità e le modifiche incluse nella versione corrente dell''integrazione di Adobe Sign per NetSuite.  '
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
source-git-commit: 924813403d8e13f816347dd548a68a16d78d866e
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 5%

---


# Note sulla release di Adobe Sign per NetSuite

## Aggiorna al pacchetto v4.0.4

4.0.4 è completamente adattato per utilizzare domini specifici dell&#39;account per tutto il traffico appena generato.

L&#39;icona di Adobe Sign è stata aggiornata alla nuova immagine.

## Versioni precedenti

### Adobe Sign per NetSuite 4.0.4

4.0.4 è completamente adattato per utilizzare domini specifici dell&#39;account per tutto il traffico appena generato.

L&#39;icona di Adobe Sign è stata aggiornata alla nuova immagine.

### Adobe Sign per NetSuite 4.0.2

Assegnato a **Adobe Sign** (da *Servizi di Adobe Document Cloud eSign*)\
Vedrete *Adobe Sign* dove avete visto in precedenza *Adobe eSign Services* come prova della riassegnazione.

### Adobe Sign per NetSuite 4.0.1

A causa di un errore di regressione API introdotto quando NetSuite ha eseguito il relativo aggiornamento della piattaforma, è stato rilasciato un nuovo pacchetto (v4.0.1).

I clienti vengono incoraggiati ad aggiornare il nuovo pacchetto.

### Adobe Sign per NetSuite 4.0

**Aggiunta di provisioning automatico degli utenti tramite NetSuite**

È stata aggiunta una nuova preferenza personalizzata per v4.0. Se abilitato, gli utenti che inviano contratti in NetSuite vengono automaticamente dotati di un account utente dei servizi eSign di Adobe Document Cloud.

**Certificato con &#39;Built for NetSuite&#39;**

Questa versione ha ottenuto la certificazione &#39;Built for Netsuite&#39; e soddisfa tutte le procedure ottimali più recenti per la progettazione di NetSuite.

**Assegnato ai servizi Adobe Document Cloud eSign (da EchoSign)**

Vedrete Adobe Document Cloud eSign Services (o Adobe eSign Services per breve tempo) dove in precedenza avete visto Adobe EchoSign come prova della rideterminazione.

**Protezione avanzata implementata con OAuth**

Per migliorare la sicurezza dei dati, i servizi eSign utilizzano ora OAuth 2.0 per autenticare l&#39;account dei servizi Adobe Document Cloud eSign in NetSuite. Questo nuovo protocollo consente a NetSuite di parlare con i servizi eSign senza richiedere la password dei servizi eSign. Poiché le informazioni riservate non vengono condivise direttamente tra le applicazioni, la probabilità che il tuo account venga compromesso è più bassa. Questo miglioramento non avrà alcun impatto sull&#39;implementazione, ma sarà necessario eseguire una configurazione unica per autorizzare il pacchetto NetSuite a comunicare con Adobe Document Cloud. Questa operazione viene eseguita durante il processo di installazione. Per i clienti che eseguono l&#39;aggiornamento da una versione precedente del pacchetto—v3.5.9 e precedente—la chiave API utilizzata in precedenza verrà sostituita da un token OAuth generato durante il processo di autorizzazione.

**Migrazione dei servizi eSign dalle API SOAP alle API REST eseguita**

Per migliorare l&#39;efficienza, la flessibilità e la velocità di elaborazione, i servizi Adobe Document Cloud eSign e, di conseguenza, l&#39;integrazione v4.0 per NetSuite sono stati migrati da API basate su SOAP a API basate su REST.

### Adobe Sign per NetSuite 3.0

**Ruoli partecipanti avanzati - Approvatore**

* Uno o più destinatari possono essere contrassegnati come approvatori in un contratto
* Gli approvatori devono esaminare e approvare il documento
* Gli approvatori possono anche essere tenuti a compilare i dati nell&#39;accordo prima di approvare

**Anteprima dei campi del documento o trascinamento della selezione prima dell&#39;invio**

Visualizza in anteprima i campi del contratto o trascina i campi del modulo prima di inviare la firma

**Invia promemoria al firmatario corrente**

Invia promemoria immediato al firmatario corrente

**Criteri di autenticazione firma avanzata**

* **Autenticazione basata su conoscenze:** rispondere alle domande per verificare l&#39;identità del firmatario
   * Richiede ai firmatari di provare la propria identità rispondendo alle domande di centinaia di banche dati pubbliche e commerciali
   * Il nome nella firma è tratto dal nome autenticato dell’utente e non può essere modificato al momento della firma
   * Con tecnologia RSA
   * L&#39;utilizzo di KBA è limitato per account al mese. Contatta le vendite per ulteriori informazioni.

* **Identità Web:** Accedi con Facebook, LinkedIn, Google o altri servizi Web di terze parti prima di firmare.

   * Il firmatario può firmare solo dopo aver verificato la propria identità utilizzando un servizio Web di terze parti.
   * Il nome nella firma viene preso dal servizio Web pro!le dell&#39;utente e non può essere modificato al momento della firma
   * Audit trail acquisisce i dettagli della verifica dell&#39;identità

* **Password una volta**
   * Applicare metodi di autenticazione per i sottoscrittori interni o esterni o per tutti i sottoscrittori. I firmatari esterni devono utilizzare una password o l&#39;autenticazione basata su conoscenze mentre i firmatari interni non

**Preferenze personalizzate aggiuntive**

* Aggiungi PDF firmato come collegamento a !le URL o come allegato ospitato in NetSuite
* Aggiungi traccia di controllo al record del contratto a un contratto$er firmato
* Utilizza il contatto della transazione come !rst firmater per impostazione predefinita, anziché come messaggio di posta elettronica del cliente
* Concedi ai mittenti l&#39;opzione per contrassegnare i destinatari come approvatori

**File di transazione**

È possibile selezionare i file da allegare dalla transazione corrente con il nuovo elenco a discesa File di transazione.

**Certificazione Adobe PDF per tutti i documenti EchoSign**

* Tutti i file PDF inviati o scaricati da EchoSign saranno certificati con un certificato digitale Adobe EchoSign
* Acrobat o Reader visualizzano la certificazione che garantisce che il documento non sia stato alterato per un&#39;ulteriore affidabilità e tranquillità

**Raccolta dei documenti di supporto**

* I mittenti possono raccogliere ulteriori documenti giustificativi dai sottoscrittori durante la firma (ad esempio, patente, certificato commerciale)
* I documenti raccolti fanno parte del record ufficiale del contratto firmato

**Campi di dati condizionali**

* Definire la logica condizionale per i campi dell&#39;accordo
* Le condizioni possono essere basate su valori per uno o più campi del contratto
* Le condizioni possono essere disattivate!Nate tramite l&#39;interfaccia utente di creazione moduli di trascinamento della selezione o tramite tag di testo
* Al firmatario vengono presentati i campi appropriati durante la firma di un documento in base alle condizioni de!ned

**Ulteriori miglioramenti per i campi modulo EchoSign**

* Menu a discesa
* Mascheramento sul campo
* Pulsanti di scelta
* Crea tag di testo più brevi per mantenere la struttura del documento
