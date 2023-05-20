---
title: Installazione della versione di prova di Workday
description: Guida all’installazione di Workday per un account di prova in Adobe Sign
uuid: 0c51f329-b7c1-44a2-88a3-670be7673747
products: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 63ed2d5b-9d82-4f87-97e1-2dde23501e89
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: beafe6c0-262f-4f5b-9315-a023a4eef4a2
source-git-commit: 4d73ff36408283805386bd3266b683bc187d6031
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# [!DNL Workday] Installazione di prova{#workday-trial-installation}

## Panoramica {#overview}

Questo documento è progettato per facilitare [!DNL Workday] i clienti imparano come attivare un account di prova con Adobe Sign e quindi integrarlo in [!DNL Workday] inquilino. Per utilizzare Adobe Sign all&#39;interno di [!DNL Workday], devi sapere come creare e modificare [!DNL Workday] elementi quali:

* Quadro dei processi aziendali
* Configurazione e configurazione del tenant
* Segnalazione e [!DNL Workday] Integrazione in studio

**Nota**: Se disponi di un account Adobe Sign esistente, non è necessario avviare una versione di prova. Puoi contattare il tuo Client Success Manager per richiedere [!DNL Workday] integrazione.

I passaggi di alto livello per completare l&#39;integrazione sono:

* Attivazione dell’account di prova con Adobe Sign
* Generare una chiave di integrazione in Adobe Sign
* Installa la chiave di integrazione nella [!DNL Workday] Tenant

## Attivazione dell’account di prova di Adobe Sign {#activate-sign-trial-account}

Per richiedere una versione di prova di 30 giorni di Adobe Sign, è necessario compilare questo [modulo di iscrizione](https://land.echosign.com/esign-trial-workday-registration.html).

**Nota**: Si consiglia vivamente di utilizzare un indirizzo e-mail funzionale valido per creare la versione di prova e non un indirizzo e-mail temporaneo. È necessario accedere a questa e-mail per verificare l’account, quindi l’indirizzo deve essere valido.

![Modulo di richiesta della versione di prova](images/trial-land.png)

Entro un giorno lavorativo, un Adobe Sign on-boarding specializzato fornisce il proprio account (in Adobe Sign) per [!DNL Workday]. Al termine, riceverai un&#39;e-mail di conferma come illustrato di seguito.

![E-mail di benvenuto da Adobe Sign](images/welcome-email-2020.png)

Per inizializzare l’account e accedere all’Adobe Sign [!UICONTROL Home] , segui le istruzioni nell’e-mail .

![Dashboard di Adobe Sign](images/classic-home.png)

## Generare una chiave di integrazione {#generate-an-integration-key}

Per le nuove installazioni, è necessario generare una chiave di integrazione in Adobe Sign e quindi inserirla in [!DNL Workday]. Questa chiave autentica l&#39;Adobe Sign e [!DNL Workday] per fidarsi reciprocamente e condividere i contenuti.

Per generare una chiave di integrazione in Adobe Sign:

1. Accedi al tuo amministratore in Adobe Sign.
1. Passa a **[!UICONTROL **Account]** > **[!UICONTROL Preferenze personali]** > **[!UICONTROL Token di accesso**]**.
1. Fate clic sul **icona più cerchiato** sul lato destro della finestra.

   Apre la [!UICONTROL Crea chiave di integrazione] interfaccia.

   ![Immagine della navigazione alla pagina Token di accesso](images/navigate-to-group-accesstokens.png)

1. Fornire un nome intuitivo per la chiave, ad esempio [!DNL Workday].

   La chiave di integrazione deve avere i seguenti elementi attivati:

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_read
   * library_read

   ![Pannello Crea chiave di integrazione](images/create-integration-key-575.png)

1. Fai clic su **[!UICONTROL Salva]**.

   Il [!UICONTROL Token di accesso] viene visualizzata la pagina con i tasti progettati nel tuo account.

1. Fate clic sulla definizione della chiave creata per [!DNL Workday].

   Il [!UICONTROL Chiave di integrazione] viene visualizzato nella parte superiore della definizione.

1. Fate clic sul **[!UICONTROL Chiave di integrazione]** link.

   Espone la chiave di integrazione.

   ![Il collegamento Chiave di integrazione](images/integration-key.png)

1. Copia questa chiave e salva in un luogo sicuro per il passaggio successivo.
1. Fai clic su **[!UICONTROL OK]**.

   ![Il pannello Chiave di integrazione](images/copy-the-key-575.png)

## Configura il [!DNL Workday] inquilino {#configuring-the-workday-tenant}

### Installazione della chiave di integrazione {#install-the-integration-key}

Installazione della chiave di integrazione nel [!DNL Workday] tenant stabilisce la relazione affidabile con Adobe Sign. Una volta stabilita tale relazione, qualsiasi processo aziendale può avere un [!UICONTROL Passaggio Rivedi documento] aggiunto che abilita il processo di firma.

**Nota**: Adobe Sign è denominato &quot;Adobe Document Cloud&quot; in tutto il [!DNL Workday] ambiente.

Per installare la chiave di integrazione:

1. Accedi a [!DNL Workday] come amministratore dell’account.
1. Cerca e apri il **[!UICONTROL Modifica configurazione titolare - Processi aziendali]** pagina.

1. Fornire informazioni per i quattro campi seguenti:

   * **[!UICONTROL Adobe Document Cloud riconoscimento]**: Un testo fisso che riconosce l&#39;integrazione.

   * **[!UICONTROL Chiave API di Adobe Document Cloud]**: Dove è installata la chiave di integrazione

   * **[!UICONTROL Indirizzo e-mail mittente di Adobe Document Cloud]**: Indirizzo e-mail dell’amministratore a livello di gruppo in Adobe Sign

   * **[!UICONTROL Rimuovere i documenti in attesa di firma elettronica quando il documento è annullato]**: Una configurazione opzionale che rimuove i documenti dal ciclo di firma se un documento viene annullato in [!DNL Workday].

   ![Campi per la chiave di integrazione Adobe Sign](images/bp-filled-torn2-575.png)

1. Quindi, completa l’installazione:

   1. Incolla la chiave di integrazione nel [!UICONTROL Chiave di integrazione API di Adobe Sign] campo.
   1. Immetti l’indirizzo e-mail dell’amministratore dell’Adobe Sign nel [!UICONTROL Indirizzo e-mail mittente di Adobe Document Cloud] campo.
   1. Fai clic su **[!UICONTROL OK]**.

   ![I campi Chiave di integrazione e il campo e-mail del titolare della chiave](images/bp-filled-small.png)

Ora è possibile aggiungere la funzionalità Adobe Sign a qualsiasi processo aziendale aggiungendo un [!UICONTROL Passaggio Rivedi documento] e configurarlo per l&#39;uso **[!UICONTROL eSign per Adobe]** come tipo di firma elettronica.

### Configurare il passaggio Rivedi documento {#configure-the-review-document-step}

Il documento per il passaggio Rivedi documento può essere un documento statico; un documento generato da un passaggio Genera documento all&#39;interno dello stesso processo aziendale; oppure un report formattato creato con il metodo [!DNL Workday] Report Designer. Tutti questi casi possono essere aumentati con [Adobe di tag di testo](https://adobe.com/go/adobesign_text_tag_guide) per controllare l&#39;aspetto e la posizione dei componenti specifici di Adobe Signing. L&#39;origine del documento deve essere specificata all&#39;interno della definizione del processo aziendale. Non è possibile caricare un documento ad hoc durante l&#39;esecuzione del processo aziendale.

La possibilità di disporre di gruppi di firmatari serializzati è una caratteristica esclusiva di Adobe Sign con un passaggio Rivedi documento. I gruppi di firmatari consentono di specificare gruppi basati su ruoli che firmano in sequenza. Adobe Sign non supporta i gruppi di firma paralleli.

Per assistenza nella configurazione del passaggio Rivedi documento, fare riferimento alla [Guida rapida](https://adobe.com//go/adobesign_workday_quick_start){target="_blank"}.

## Supporto {#support}

### [!DNL Workday] supporto {#workday-support}

[!DNL Workday] è il proprietario dell&#39;integrazione e deve essere il primo punto di contatto per le domande sull&#39;ambito dell&#39;integrazione, le richieste di funzioni o i problemi che si verificano quotidianamente nell&#39;integrazione.

Il [!DNL Workday] la community contiene diversi articoli utili su come risolvere i problemi di integrazione e generare documenti:

* [Risoluzione dei problemi relativi alle integrazioni di eSignature](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Passaggio Rivedi documenti](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [Generazione di documenti dinamici](https://community.workday.com/node/176443)

* [Suggerimenti sulla configurazione per la generazione di documenti di offerta](https://community.workday.com/node/183242)

### Supporto Adobe Sign {#adobe-sign-support}

Adobe Sign è il partner di integrazione e deve essere contattato se l’integrazione non riesce a ottenere le firme o se la notifica delle firme in sospeso non riesce.

I clienti Adobe Sign devono contattare il proprio Customer Success Manager (CSM) per assistenza. In alternativa, è possibile contattare il supporto tecnico di Adobe telefonicamente: 1-866-318-4100; attendi l&#39;elenco dei prodotti e immetti: 4 e poi 2 (come richiesto).

* [Aggiunta di tag di testo di Adobe ai documenti](https://adobe.com/go/adobesign_text_tag_guide)

* [Esempi e configurazione della revisione del documento](https://www.adobe.com//go/adobesign_workday_quick_start){target="_blank"}

[**Contatta il supporto Adobe Sign**](https://www.adobe.com/go/adobesign-support-center)
