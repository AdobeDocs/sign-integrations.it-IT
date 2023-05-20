---
title: Note sulla versione di Adobe Sign per NetSuite
description: Scoprite le nuove funzioni e le modifiche incluse nella versione corrente dell'integrazione di Adobe Sign per NetSuite.
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 6317723e-447a-4506-a621-4d967bdd6561
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Note sulla versione di Adobe Sign per NetSuite

## Aggiornamento al pacchetto v4.0.4

4.0.4 è completamente adattato per utilizzare domini specifici dell’account per tutto il traffico generato di recente.

L’icona Adobe Sign è stata aggiornata alla nuova grafica.

## Versioni precedenti

### Adobe Sign per NetSuite 4.0.4

4.0.4 è completamente adattato per utilizzare domini specifici dell’account per tutto il traffico generato di recente.

L’icona Adobe Sign è stata aggiornata alla nuova grafica.

### Adobe Sign per NetSuite 4.0.2

Rebranded to **Adobe Sign** (da *Servizi eSign di Adobe Document Cloud*)\
Vedete *Adobe Sign* dove hai visto in precedenza *Adobe di servizi eSign* come prova del rebranding.

### Adobe Sign per NetSuite 4.0.1

A causa di un bug di regressione API introdotto quando NetSuite ha eseguito l&#39;aggiornamento della piattaforma, è stato rilasciato un nuovo pacchetto (v4.0.1).

Si consiglia ai clienti di eseguire l&#39;aggiornamento al pacchetto più recente.

### Adobe Sign per NetSuite 4.0

**Aggiunta del provisioning automatico degli utenti tramite NetSuite**

È stata aggiunta una nuova preferenza personalizzata per la versione 4.0. Quando questa opzione è attivata, gli utenti che inviano accordi in NetSuite dispongono automaticamente di un account utente dei servizi eSign di Adobe Document Cloud.

**Certificato con &#39;Built for NetSuite&#39;**

Questa versione ha ottenuto la certificazione &quot;Built for NetSuite&quot; e soddisfa tutte le più recenti best practice di progettazione di NetSuite.

**Rebranded to Adobe Document Cloud eSign services (da EchoSign)**

I servizi eSign di Adobe Document Cloud (o in breve Adobe i servizi eSign) sono ora visualizzati in precedenza come prova del rebranding di Adobe EchoSign.

**Sicurezza avanzata implementata con OAuth**

Per migliorare la sicurezza dei dati, i servizi eSign ora utilizzano OAuth 2.0 per autenticare l’account dei servizi eSign di Adobe Document Cloud in NetSuite. Questo nuovo protocollo consente a NetSuite di comunicare con i servizi eSign senza richiedere la password dei servizi eSign. Poiché le informazioni riservate non vengono condivise direttamente tra le app, è meno probabile che l’account venga compromesso. Questo miglioramento non influisce sull&#39;implementazione, ma è necessario eseguire una configurazione una tantum per autorizzare il pacchetto NetSuite a comunicare con Adobe Document Cloud. Questa operazione viene eseguita durante il processo di installazione. Per i clienti che eseguono l’aggiornamento da una versione precedente del pacchetto (v3.5.9 e versioni precedenti), la chiave API precedentemente utilizzata viene sostituita da un token OAuth generato durante il processo di autorizzazione.

**Migrazione dei servizi eSign dalle API SOAP alle API REST**

Per migliorare l&#39;efficienza, la flessibilità e la velocità di elaborazione, i servizi eSign di Adobe Document Cloud, e di conseguenza l&#39;integrazione v4.0 per NetSuite, sono passati dalle API basate su SOAP a quelle basate su REST.

### Adobe Sign per NetSuite 3.0

**Ruoli partecipanti avanzati - Approvatore**

* Uno o più destinatari possono essere contrassegnati come approvatori in un accordo
* Gli approvatori devono rivedere e approvare il documento
* Gli approvatori possono anche essere tenuti a compilare i dati dell’accordo prima di approvarlo

**Anteprima documento o trascinamento dei campi modulo prima dell’invio**

Anteprima dell’accordo o trascinamento dei campi modulo prima dell’invio per la firma

**Invia promemoria al firmatario corrente**

Invia un promemoria immediato al firmatario corrente

**Criteri avanzati per l’autenticazione dei firmatari**

* **Autenticazione basata su conoscenza:** Rispondere alle domande per verificare l’identità del firmatario
   * Richiede ai firmatari di dimostrare la propria identità rispondendo a domande prese da centinaia di database pubblici e commerciali
   * Il nome alla firma è tratto dal nome autenticato dell’utente e non può essere modificato al momento della firma.
   * Con tecnologia RSA
   * L’utilizzo di KBA è limitato per account, al mese. Per ulteriori informazioni, contatta il reparto Vendite.

* **Identità Web:** Accedi con Facebook, LinkedIn, Google o altri servizi Web di terze parti prima di firmare.

   * Il firmatario può firmare solo dopo aver verificato la propria identità tramite un servizio Web di terze parti.
   * Il nome alla firma viene preso dal servizio Web pro!le dell&#39;utente e non può essere modificato al momento della firma.
   * L’audit trail acquisisce i dettagli della verifica dell’identità

* **Password una tantum**
   * Applica metodi di autenticazione per i firmatari interni o esterni o per tutti i firmatari. I firmatari esterni devono utilizzare una password o l’autenticazione basata su conoscenza, mentre i firmatari interni non utilizzano l’autenticazione.

**Preferenze personalizzate aggiuntive**

* Aggiungere PDF firmato come collegamento all&#39;URL o come allegato ospitato in NetSuite
* Aggiungi audit trail al record dell’accordo a$er viene firmato un accordo
* Utilizza il contatto della transazione come firmatario per impostazione predefinita, anziché l’e-mail del cliente
* Concedi ai mittenti l’opzione di contrassegnare i destinatari come approvatori

**File delle transazioni**

Puoi selezionare i file da allegare dalla transazione corrente con il nuovo elenco a discesa &quot;File di transazione&quot;.

**Certificazione Adobe PDF Per Tutti I Documenti EchoSign**

* Tutti i file PDF inviati o scaricati da EchoSign sono certificati con un certificato digitale Adobe EchoSign
* Acrobat o Reader visualizza la certificazione che garantisce che il documento non sia stato manomesso per una maggiore fiducia e tranquillità

**Raccogli documenti di supporto**

* I mittenti possono raccogliere ulteriori documenti di supporto dai firmatari durante la firma, ad esempio una patente di guida, un certificato aziendale e altro ancora.
* I documenti raccolti diventano parte del registro ufficiale dell’accordo firmato

**Campi di dati condizionali**

* Definire la logica condizionale per i campi dell’accordo
* Le condizioni possono basarsi su valori per uno o più campi dell’accordo
* Le condizioni possono essere create!ned tramite l&#39;interfaccia utente di creazione dei moduli tramite trascinamento o tramite tag di testo
* Al firmatario vengono presentati i campi appropriati quando firma un documento in base alle condizioni de!ned.

**Ulteriori miglioramenti per i campi modulo EchoSign**

* Menu a discesa
* Mascheramento dei campi
* Pulsanti di scelta
* Creare tag di testo più brevi per mantenere la struttura del documento
