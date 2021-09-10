---
title: Integrazioni di Adobe Sign Versioni e ciclo di vita dei prodotti
description: Informazioni sulle versioni di Adobe Sign Integrations e sul ciclo di vita del supporto
audience: External
products: Adobe Sign
type: Documentation
solution: Adobe Sign
role: User, Developer
topic: Integrations
exl-id: c1f22848-7951-4066-84d4-f8cf6c2f3a6f
source-git-commit: 30cb79b6856c7b623dc5118b4aa40193bf749220
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 40%

---

# Versioni e ciclo di vita dei prodotti {#version}

La convenzione di controllo delle versioni di Adobe Sign e il ciclo di vita del supporto per i servizi integrati si allinea con altri prodotti Adobe che potrebbero essere noti.

## Numeri di versione

La versione del pacchetto utilizza un sistema di numerazione in tre parti per identificare il numero di build sequenziale della versione rilasciata e l’importanza relativa dell’aggiornamento in termini di contenuto nuovo o modificato.

Il numero di versione segue questo schema: N.m.p.

Dove, N = versione principale; m = versione secondaria; p = versione con patch.

Ad esempio, un pacchetto di integrazione versione 23.2.1 indica uno stato di rilascio di:

* Versione principale: 23
* Versione secondaria: 2.
* Versione patch: 1.

Man mano che gli ingegneri sviluppano nuove &quot;build&quot; del pacchetto, aumentano il numero di versione in base alla natura degli aggiornamenti del codice.

* Le principali modifiche alla versione comportano un&#39;aggiunta significativa di funzioni o una modifica importante dei sistemi principali.
* Gli aggiornamenti delle versioni secondarie includono aggiornamenti delle funzionalità più piccoli e patch di sicurezza. Adobe Sign può richiedere un aggiornamento all&#39;ultima versione con patch in caso di aggiornamenti sulla sicurezza o per indirizzare un elemento segnalato.
* Le patch rappresentano quasi esclusivamente correzioni di bug e regolazioni dell’interfaccia utente.

>[!NOTE]
>
>Tutte le versioni non vengono rilasciate al pubblico mentre il prodotto si inserisce nello sviluppo. Quindi, potrebbero esserci dei salti significativi nella versione delle patch tra rilasci.

Gli amministratori devono mantenere aggiornata la propria versione per garantire che l&#39;account abbia pieno accesso a tutte le funzionalità e che tutti i problemi di sicurezza noti vengano risolti. Adobe Sign può richiedere un aggiornamento alla versione più recente con patch in caso di problemi di sicurezza o per risolvere un problema di sistema critico.

## Ciclo di vita del supporto della versione

Il ciclo di vita del supporto della versione di un prodotto di integrazione di Adobe Sign è definito in base alla versione principale del pacchetto e indica il periodo di tempo in cui Adobe Sign supporta attivamente la singola versione dell&#39;integrazione.

Adobe Sign supporta la versione corrente di un pacchetto e le due versioni principali precedenti (incluse tutte le versioni secondarie e di patch correlate). Le versioni principali sono espresse come segue:

* Versione corrente (N): versione principale più recente del pacchetto
* Versione precedente (N-1): versione principale immediatamente precedente rispetto a quella più recente
* Ultima versione supportata (N-2): due versioni principali precedenti rispetto alla versione corrente

Ad esempio, se la versione disponibile corrente del pacchetto è 23.2.1, effettuare le operazioni riportate di seguito.

* La versione principale corrente (N) è 23.
* La versione principale precedente (N-1) di questo pacchetto è 22.
* L’ultima versione principale supportata (N-2) di questo pacchetto è 21.
* Qualsiasi versione precedente alla versione 21.0.0 non è supportata.

![Tabella delle versioni](images/version_chart.png)

## Ciclo di vita del servizio Versione

Il ciclo di vita del servizio delle versioni definisce l’ambito completo nel quale il servizio risulta utilizzabile. La tempistica corrisponde a quella del ciclo di vita per il supporto delle versioni, con l’aggiunta di un periodo di tolleranza di 90 giorni durante il quale i clienti possono completare l’aggiornamento.

* Durante il periodo di tolleranza di una versione non supportata, il supporto contempla solo l’aggiornamento a una versione più recente, e non include la manutenzione di una versione non più supportata.
* Dopo il periodo di tolleranza, la versione non è più in servizio

* Adobe Sign non accetta richieste da versioni non in servizio
* Una volta aggiornata l’integrazione alla versione corrente, le comunicazioni tra Adobe Sign e l’integrazione riprenderanno normalmente

![Periodo di chiusura](images/shutdown_period.png)

Per qualsiasi domanda, contatta il tuo rivenditore o l’assistenza clienti.
