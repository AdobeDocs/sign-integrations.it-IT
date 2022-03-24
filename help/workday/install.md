---
title: Guida all'installazione di Workday
description: Guida all'installazione per abilitare l'integrazione di Adobe Sign in Workday
uuid: 56478222-fe66-4fa5-aac3-0ecdf2863197
product: Adobe Sign
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 29d55a25-6e2f-4c59-ae7c-c21bb82cecba
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance)
type: Documentation
solution: Acrobat Sign, Adobe Sign
role: User, Developer
topic: Integrations
exl-id: 8f12b524-2123-45d4-98d5-b2b23580a5ea
source-git-commit: b326a9afa2c16333d390cac3b30a2c7c741a4360
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 23%

---

# [!DNL Workday] Guida all’installazione{#workday-installation-guide}

[**Contatta il supporto di Adobe Sign**](https://adobe.com/go/adobesign-support-center_it)

## Panoramica {#overview}

Questo documento spiega come integrare Adobe Sign nel [!DNL Workday] inquilino. Per utilizzare Adobe Sign all&#39;interno di [!DNL Workday], devi sapere come creare e modificare [!DNL Workday] elementi quali:

* Quadro dei processi aziendali
* Configurazione e configurazione del tenant
* Segnalazione e [!DNL Workday] integrazione in studio

I passaggi di alto livello per completare l&#39;integrazione sono:

* Attivazione dell’account amministrativo in Adobe Sign (solo per i nuovi clienti)
* Configura un gruppo in Adobe Sign per contenere la proprietà [!DNL Workday] utente integrazione
* Stabilire la relazione OAuth tra [!DNL Workday] e Adobe Sign

## Attivazione dell’account Adobe Sign {#activating-your-adobe-sign-account}

I clienti esistenti con account consolidati possono passare al [Configurare Adobe Sign per [!DNL Workday]](#config) argomento.

Per i clienti che non hanno mai utilizzato Adobe Sign e che non dispongono di un accesso preesistente, un Adobe sulle disposizioni specialistiche per l’account (in Adobe Sign) per [!DNL Workday]. Al termine, riceverai un&#39;e-mail di conferma come illustrato di seguito.

![Immagine dell&#39;e-mail di benvenuto da Adobe Sign](images/welcome-email-2020.png)

Per inizializzare l’account e accedere al tuo Adobe Sign, devi seguire le istruzioni riportate nell’e-mail. [!UICONTROL Home] pagina.

![Pagina del dashboard di Adobe Sign](images/classic-home.png)

## Configurare Adobe Sign per [!DNL Workday] {#config}

Per configurare Adobe Sign per [!DNL Workday], è necessario generare due oggetti dedicati nel sistema Adobe Sign:

* **A [!DNL Workday] gruppo**: [!DNL Workday] richiede un &quot;gruppo&quot; dedicato nell’account Adobe Sign per abilitare la funzionalità di integrazione. Il gruppo Adobe Sign viene utilizzato per controllare solo la proprietà [!DNL Workday] utilizzo di Adobe Sign. Qualsiasi altro utilizzo potenziale, ad esempio Salesforce.com o Arriba, non viene influenzato. Le notifiche e-mail vengono eliminate in [!DNL Workday] in modo che la proprietà [!DNL Workday] gli utenti ricevono solo le notifiche all&#39;interno dei [!DNL Workday] posta in arrivo.

* **Un utente che autentica la chiave di integrazione**: A [!DNL Workday] il gruppo deve avere un solo amministratore a livello di gruppo, che è il titolare autorevole della chiave di integrazione. Si consiglia all’amministratore di utilizzare un indirizzo e-mail funzionale come `HR@MyDomain.com` anziché un messaggio e-mail personale per ridurre il rischio che l&#39;utente venga disattivato in futuro e quindi disabilitare l&#39;integrazione.

### Creare un utente e un gruppo in Adobe Sign {#create-a-user-and-group-in-adobe-sign}

Per creare un utente in Adobe Sign:

1. Accedere ad Adobe Sign come amministratore dell&#39;account..
1. Passa a **[!UICONTROL Account]** > **[!UICONTROL Utenti]**.
1. Fate clic sul ![immagine più icona](images/icon_plus.png) per creare un nuovo utente.

   ![Immagine del percorso di navigazione per creare un nuovo utente](images/navigate-to-group-unbranded.png)

1. Nella finestra di dialogo visualizzata, fornisci i dettagli del nuovo utente:

   * Fornisci un indirizzo e-mail funzionale a cui puoi accedere.
   * Immettere un valore appropriato per Nome e Cognome.
   * Seleziona **[!UICONTROL Creare un nuovo gruppo per questo utente]** dal gruppo di utenti.
   * Fornire la proprietà **[!UICONTROL Nuovo nome gruppo]** con un nome intuitivo come *[!DNL Workday]*.

   ![Riquadro Crea un utente](images/create-user.png)

1. Fai clic su **[!UICONTROL Salva]**.

   Ti riporta al [!UICONTROL Utenti] che elenca il nuovo utente con una **[!UICONTROL CREATO]** stato.

   ![Una vista del nuovo utente creato](images/post-user-creation.png)

Per verificare l’indirizzo e-mail dell’utente con lo stato &quot;Creato&quot;:

1. Accedi all’e-mail del nuovo utente.
2. Trova l’e-mail &quot;Benvenuti in Adobe Sign&quot;.
3. Fai clic nel punto indicato **[!UICONTROL Fai clic qui per impostare la password]**.
4. Imposta la password.

Una volta verificato l’indirizzo e-mail, lo stato dell’utente cambia da [!UICONTROL CREATO] a [!UICONTROL ATTIVO].

![Immagine del nuovo utente attivato](images/actived-users-575.png)

### Definire l’utente che esegue l’autenticazione {#define-the-authenticating-user}

Per promuovere il nuovo utente nel [!DNL Workday] gruppo:

1. Passa al [!UICONTROL Utenti] (se non è già presente).
2. Fai doppio clic sull&#39;utente nel [!DNL Workday] gruppo.

   Si apre un evento [!UICONTROL Modifica] pagina delle autorizzazioni utente.

3. Verifica la proprietà **[!UICONTROL Amministratore del gruppo]**.
4. Fai clic su **[!UICONTROL Salva]**.

![](images/user-permissions-edit1-575.png)

## Configura il [!DNL Workday] inquilino {#configure-workday}

Per completare la connessione tra [!DNL Workday] titolare e Adobe Sign, è necessario stabilire una relazione di affidabilità tra i servizi. Al termine, è possibile aggiungere un passaggio Review Document (Rivedi documento) che abilita il processo di firma tramite Adobe Sign.

>[!NOTE]
>
>Adobe Sign è marchiato come Adobe Document Cloud in tutto il [!DNL Workday] ambiente.

Per stabilire la relazione di affidabilità:

1. Accedi a [!DNL Workday] come amministratore dell’account.
1. Apri il **[!UICONTROL Modifica configurazione titolare - Processi aziendali]** pagina.
1. Individua la sezione [!UICONTROL eSignature Configuration] (Configurazione firma elettronica):

   ![](images/esignature_configurations.png)

1. Fai clic su **[!UICONTROL Autenticazione tramite Adobe]**.

   Viene avviata la sequenza di autenticazione OAuth2.0.

1. Quando richiesto, immetti le credenziali per l’amministratore del gruppo Adobe Sign creato in precedenza.
1. Approva l’accesso ad Adobe Sign.

>[!NOTE]
>
>Prima di procedere, assicurati di uscire completamente da qualsiasi altra istanza di Adobe Sign.

Una volta effettuata la connessione, la casella di controllo Adobe configuration enabled (Configurazione di Adobe attivata) è impostata e puoi iniziare a utilizzare Adobe Sign con [!DNL Workday].

### Configurare il passaggio Rivedi documento {#configure-review}

Il documento per il passaggio Rivedi documento può essere uno dei seguenti:

* Un documento statico
* Un documento generato da un passaggio Genera documento all’interno dello stesso processo aziendale
* Un rapporto formattato creato con il metodo [!DNL Workday] Report Designer

È possibile aggiungere questi documenti con [Adobe di tag di testo](https://adobe.com/go/adobesign_text_tag_guide_it) per controllare l&#39;aspetto e la posizione dei componenti specifici di Adobe Signing. È necessario specificare l&#39;origine del documento nella definizione del processo aziendale. Non è possibile caricare un documento ad hoc durante l&#39;esecuzione del processo aziendale.

La possibilità di disporre di gruppi di firmatari serializzati è una caratteristica esclusiva di Adobe Sign con un passaggio Rivedi documento. Ciò consente di specificare gruppi basati su ruoli per la firma in sequenza. Adobe Sign non supporta i gruppi di firma paralleli.

Per assistenza nella configurazione del passaggio Rivedi documento, fai riferimento alla [Guida rapida](https://adobe.com//go/adobesign_workday_quick_start){target=&quot;_blank&quot;}.

## Supporto {#support}

### [!DNL Workday] supporto {#workday-support}

[!DNL Workday] è il responsabile del processo di integrazione e deve essere considerato come il principale riferimento di contatto per domande relative a integrazione, richieste di funzionalità o problemi nelle operazioni quotidiane dell’integrazione.

Potete fare riferimento a quanto segue [!DNL Workday] articoli della community su come risolvere i problemi di integrazione e generare documenti:

* [Risoluzione dei problemi relativi alle integrazioni di eSignature](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Passaggio Rivedi documenti](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)
* [Generazione di documenti dinamici](https://community.workday.com/saml/login?destination=/articles/176443)
* [Suggerimenti per la generazione di documenti](https://community.workday.com/node/183242)

### Supporto Adobe Sign {#adobe-sign-support}

In quanto partner per integrazione, è necessario contattare il supporto di Adobe Sign se l’integrazione non è in grado di ottenere firme o se si verificano problemi di notifica delle firme in sospeso.

I clienti Adobe Sign possono contattare il proprio Customer Success Manager (CSM) per ricevere assistenza. In alternativa, è possibile rivolgersi al supporto tecnico di Adobe telefonando al numero 1-866-318-4100 e digitando 4 in seguito all’elenco dei prodotti, quindi 2 (quando richiesto).

* [Aggiunta di tag di testo di Adobe ai documenti](https://adobe.com/go/adobesign_text_tag_guide)
* [Esempi e configurazione del documento di revisione](https://www.adobe.com//go/adobesign_workday_quick_start)

## Domande frequenti {#faq}

### Perché lo stato non viene aggiornato all’interno di [!DNL Workday] anche quando il documento è completamente firmato? {#why-is-the-status-not-being-updated-within-workday-even-the-document-is-fully-signed}

Lo stato del documento in [!DNL Workday] potrebbe non riflettere se il candidato non fa clic sul[!UICONTROL Invia]&#39; dopo aver effettuato l&#39;accesso ad Adobe Sign.

Come da [!DNL Workday] task Controlla stato firma elettronica: Per avviare il processo, l&#39;utente può inviare l&#39;attività Casella in arrivo associata.

Come da [!DNL Workday] Sviluppo: La firma originale completa la procedura solo se l&#39;utente invia l&#39;attività della posta in arrivo dopo aver firmato il documento. Dopo la firma, l&#39;iframe viene chiuso e l&#39;utente viene reindirizzato alla stessa attività in cui può fare clic sul [!UICONTROL Invia] per completare il processo.
