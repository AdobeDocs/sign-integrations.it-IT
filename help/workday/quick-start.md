---
title: Guida introduttiva per Workday
description: Guida rapida per i clienti che desiderano utilizzare Adobe Sign nei loro ambienti Workday.
uuid: 10bf8ee8-9075-44d1-a836-e454950e2d9a
products: Adobe Sign
content-type: reference
discoiquuid: 13135c88-4c39-4707-b7ba-63ff94769258
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 8b6fa8b4-e240-4ebe-ae2a-8807d75a6c69
source-git-commit: d462ccf41fa5483cfa02f5eaf154c23f26157a1e
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 32%

---

# [!DNL Workday] Guida introduttiva{#workday-quick-start-guide}

[**Contatta il supporto di Adobe Sign**](https://adobe.com/go/adobesign-support-center_it)

## Panoramica {#overview}

Questo documento è stato progettato per aiutare [!DNL Workday] gli amministratori a capire come personalizzare i processi aziendali [!DNL Workday] per includere Adobe Sign per l&#39;ottenimento di firme elettroniche. Per utilizzare Adobe Sign all&#39;interno di [!DNL Workday], è necessario sapere come creare e modificare [!DNL Workday] elementi quali:

* Framework di processi aziendali
* Configurazione e configurazione tenant
* Reporting and [!DNL Workday] Integrazione in studio

## Accesso ad Adobe Sign in [!DNL Workday] {#access-adobe-sign}

La funzionalità di firma elettronica di Adobe Sign viene visualizzata come azione [!UICONTROL Review Document Step] all&#39;interno di Business Process Framework (BPF) e come attività Distribuisci documenti.

## [!UICONTROL Passaggio Review Document (Rivedi documento)] {#review-document-step}

Adobe Sign for [!DNL Workday] è esposto tramite il [!UICONTROL Review Document Step] che è possibile aggiungere a uno qualsiasi dei più di 400 processi aziendali all&#39;interno di [!DNL Workday], inclusi Offerta, Distribuisci documenti e attività, Propone compensazione e altro ancora.

È possibile fare riferimento agli [[!DNL Workday] articoli della community su [!UICONTROL Review Document Step]](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg).

Esiste una relazione 1:1 tra [!UICONTROL [!UICONTROL Review Document Step]s] e le transazioni fatturabili con Adobe Sign. È possibile combinare più documenti all&#39;interno di un singolo [!UICONTROL Review Document Step] e vengono presentati come un unico pacchetto per la firma.

**Nota**: È possibile fare riferimento a un solo  ** documento dinamico all&#39;interno di un passo [!UICONTROL  specifico ]Revisione documento.

Per definire una funzione [!UICONTROL Rivedi fase documento]:

1. Inserire un [!UICONTROL Verifica fase documento].
1. Specificare i gruppi (ruoli) che possono agire in base alla [!UICONTROL Verifica fase documento].

![Passaggi dei processi aziendali](images/insert-review-doc-steptornm-575.png)

Per configurare [!UICONTROL Revisione passo documento]:

1. Specificare il *[!UICONTROL tipo di integrazione eSignature]* come *[!UICONTROL eSign da Adobe]*.

1. Aggiungi righe alla griglia delle firme.

   * La griglia delle firme specifica l’ordine seriale secondo cui il documento viene indirizzato per la firma. Ogni riga può contenere uno o più ruoli e ogni riga rappresenta un passaggio del processo di firma..
   * A ogni membro del ruolo all&#39;interno di un determinato passaggio viene notificato che un evento di firma è in sospeso.
   * Una volta che una singola persona viene segnalata dal ruolo, il passo riga viene completato e il documento viene spostato nel passo riga successivo.
   * Quando tutte le righe sono state firmate, [!UICONTROL Review Document Step] è stato completato.

1. Specifica il documento da firmare. Se si tratta di un processo aziendale di tipo “Offer” (Offerta), è possibile utilizzare il documento da un passaggio Generate Document (Genera documento). In caso contrario, seleziona un documento o report esistente.

1. Ripeti il passaggio 3 per tutti i documenti interessati..

   ![Finestra Configure Review Document Step (Configura passaggio Rivedi documento)](images/configure-rd-stepsmaller-575.png)

1. È possibile aggiungere un &quot;utente di reindirizzamento&quot; per l&#39;acquisizione delle azioni &quot;declino alla firma&quot;. Quando gli utenti rifiutano, [!DNL Workday] riinvia i documenti a un gruppo di sicurezza configurato per la revisione.

Dal menu delle azioni correlate di un [!UICONTROL Review Document Step], selezionare **[!UICONTROL Business Process]** > **[!UICONTROL Gestisci reindirizzamento]**. Quindi, selezionare una delle seguenti opzioni:

* **[!UICONTROL Invia indietro]**: Per consentire ai membri del gruppo di sicurezza di inviare un passo indietro a un passaggio precedente nel processo aziendale. Il processo aziendale riparte quindi da tale passaggio.
* **[!UICONTROL Passa al passaggio]** successivo: Per consentire ai membri del gruppo di sicurezza di inoltrare un passaggio al passo successivo del processo aziendale.
* **[!UICONTROL Gruppi]** di protezione: Per reindirizzare i passaggi nel flusso del processo aziendale. I gruppi di sicurezza visualizzati al prompt vengono selezionati nei criteri di sicurezza del processo aziendale nella sezione Redirect.

## Note passo processo aziendale {#business-process-step-notes}

Il Business Process Framework è potente; tuttavia, devi garantire che:

* Ogni processo aziendale deve avere una fase di completamento, idealmente alla fine del processo aziendale.

* Viene impostata una fase di completamento del menu delle azioni correlate dell&#39;icona di ricerca. Ciò è possibile solo quando si &quot;guarda&quot; la BP e non quando si &quot;modifica&quot;.

* Ogni fase del processo aziendale viene eseguita in modo sequenziale.

   È possibile modificare l&#39;ordine di un passo modificando il valore dell&#39;ordine. Ad esempio, per inserire un passaggio tra le voci &quot;c&quot; e &quot;d&quot;, specificare un nuovo elemento come &quot;ca&quot;.

### Esempio: offrire {#example-offer}

L&#39;Offerta BP è un processo secondario della Job Application Dynamic BP che deve essere configurato per eseguire l&#39;Offerta BP. Viene attivato quando lo stato della candidatura passa da “Offer” (Offri) a “Make offer” (Fai un’offerta).

Nell&#39;esempio seguente, un [!UICONTROL Review Document Step] utilizza un passaggio del documento dinamico sia per l&#39;America del Nord che per il Giappone.

![[!DNL Workday]Esempio di un processo aziendale di ](images/bp-for-offersmaller-575.png)

Questo processo aziendale prevede i seguenti passaggi:

* Chiede al promotore della BP di proporre una compensazione per il candidato (fase b).
* Utilizza una condizione di passaggio per verificare se il paese attuale NON è il Giappone.

   Se true, viene eseguito il passaggio &quot;ba&quot; che utilizza un documento in lingua inglese.

   Se false, viene eseguito il passaggio &quot;bb&quot; che utilizza un documento in lingua giapponese.

* Definisce il processo di firma in [!UICONTROL Review Document Step] &quot;bc&quot;.
* Definisce il punto di decisione di fare un&#39;offerta nella fase di completamento richiesta &quot;d&quot;.

Il documento dinamico generato nel passaggio “ba” è denominato [!UICONTROL Offer Letter] (Lettera di offerta) e contiene un singolo blocco di testo denominato [!UICONTROL Rapid Offer] (Offerta rapida). È possibile aggiungere più blocchi di testo, ad esempio intestazione, formula di apertura, compensazione, materiale, chiusura, termini e altro, a seconda delle necessità.

![[!DNL Workday] visualizza pagina documento](images/offer-letter-575.png)

La lettera di offerta dinamica riportata di seguito viene creata nell&#39;editor di testo RTF [!DNL Workday]. Gli elementi evidenziati in *grigio* sono [!DNL Workday] oggetti forniti che fanno riferimento a dati contestuali.

Gli elementi tra {{parentesi}} sono [tag di testo di Adobe](https://adobe.com/go/adobesign_text_tag_guide_it).

![Esempio di modulo dinamico](images/script.png)

All&#39;interno di [!UICONTROL Review Document Step], al documento dinamico viene fatto riferimento dal passaggio precedente e viene definito il processo di firma sequenziale tramite due gruppi di firma.

Il comportamento illustrato di seguito instraderà il documento generato in modo dinamico prima al Gestore assunzioni, quindi al Candidato.

![[!DNL Workday] gruppi di firma definiti](images/configure-rd-stepsmaller-575.png)

### Esempio: Distribuisci documenti {#example-distribute-documents}

Introdotta in [!DNL Workday] 30, l&#39;attività Distribuisci di massa documenti o Attività può essere utilizzata per inviare un singolo documento a un gruppo di grandi dimensioni (&lt;20K) di singoli firmatari. È soggetta alla limitazione di una singola firma per documento. La creazione di una distribuzione viene eseguita accedendo all&#39;azione &quot;[!UICONTROL Crea documenti di distribuzione o Attività]&quot; dalla barra di ricerca.

Esempio: invio di un modulo di scelta di partecipazione azionaria a tutti i manager di Global Modern Services. Se lo si desidera, è possibile filtrare ulteriormente i singoli manager.

È inoltre possibile accedere al report **Visualizza documenti di distribuzione o Attività** per tenere traccia dello stato di avanzamento della distribuzione.

![](images/create-distributedocumentsortasks.png)

### Esempio: generazione di report {#example-reporting}

[!DNL Workday] ha una potente infrastruttura per la generazione di report. Per visualizzare i dettagli sul processo di Adobe Sign, analizza gli elementi relativi alla voce *Review Document Event* (Evento Rivedi documento).

Di seguito viene riportato un semplice report personalizzato che può essere eseguito in tutti i processi aziendali per cercare transazioni Adobe Sign e il relativo stato.

![[!DNL Workday]Esempio di un report personalizzato di ](images/review-document-eventsmaller-575.png)

Il report seguente è stato generato con riferimento ai processi aziendali Offer (Offerta), Onboarding (On-boarding) e Propose Compensation (Proponi compenso) all’interno di un titolare di implementazione.

È possibile visualizzare:

* i documenti inviati per la firma;
* il passaggio del processo aziendale associato;
* la persona successiva in attesa di firma.

![[!DNL Workday]Esempio di un report di mediante tre oggetti](images/workday-reportsmaller-575.png)

## Documenti firmati {#signed-documents}

Il ciclo di firma [!DNL Workday] sopprime tutte le notifiche via e-mail di Adobe Sign. Gli utenti sono informati delle azioni in sospeso nella posta in arrivo [!DNL Workday].

Una volta firmato un documento da tutti i gruppi di firme, una copia del documento firmato viene distribuita a tutti i membri del gruppo di firme via e-mail.

Per sopprimere questo comportamento, è possibile contattare Adobe Sign Success Manager o il [Adobe Sign Support Team](https://adobe.com/go/adobesign-support-center).

All&#39;interno di [!DNL Workday] è possibile accedere ai documenti firmati nel record di elaborazione completo. Puoi trovare:

* Documenti lavoratore sul profilo lavoratore, e
* Documenti candidati (lettere di offerta) sul profilo Candidato.

L&#39;immagine seguente mostra una lettera di offerta firmata per il candidato Chris Foxx.

![Lettera  [!DNL Workday] offerta di esempio](images/offer.png)

## Supporto {#support}

### [!DNL Workday] sostegno {#workday-support}

[!DNL Workday] è il responsabile del processo di integrazione e deve essere considerato come il principale riferimento di contatto per domande relative a integrazione, richieste di funzionalità o problemi nelle operazioni quotidiane dell’integrazione.

La comunità [!DNL Workday] dispone di numerosi articoli validi su come risolvere i problemi relativi all&#39;integrazione e generare documenti:

* [Risoluzione di problemi relativi alle integrazioni di firma elettronica](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Passaggio di revisione dei documenti](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [Generazione di documenti dinamici](https://community.workday.com/node/176443)
* [Suggerimenti per la configurazione relativa alla generazione di documenti di offerta](https://community.workday.com/node/183242)

### Supporto di Adobe Sign {#adobe-sign-support}

In quanto partner per integrazione, è necessario contattare il supporto di Adobe Sign se l’integrazione non è in grado di ottenere firme o se si verificano problemi di notifica delle firme in sospeso.

I clienti Adobe Sign possono contattare il proprio Customer Success Manager (CSM) per ricevere assistenza. In alternativa, è possibile rivolgersi al supporto tecnico di Adobe telefonando al numero 1-866-318-4100 e digitando 4 in seguito all’elenco dei prodotti, quindi 2 (quando richiesto).

* [Aggiunta di tag di testo di Adobe ai documenti](https://adobe.com/go/adobesign_text_tag_guide)

<!--
[Download PDF](images/adobe-sign-for-workday-quick-start-guide-2016.pdf)
-->
