---
title: Ore non interattive e aggiornamento dei periodi liberi
description: Scopri come ridurre al minimo l’impatto operativo degli aggiornamenti automatici di AEM as a Cloud Service utilizzando le ore non interattive e i periodi senza aggiornamento.
feature: Deploying
role: Admin
badge: label="Disponibilità limitata" type="Positive"
source-git-commit: 44696aef63b7a9882b001a33ea24a815183996a8
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Ore non interattive e aggiornamento dei periodi liberi {#quiet-hours-update-free-periods}

>[!NOTE]
>Questa funzionalità sarà disponibile come **Disponibilità limitata** a partire dal 29 settembre. Invia un&#39;e-mail a [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) per attivare la funzionalità nei programmi.

Gli [aggiornamenti di manutenzione automatica](/help/implementing/deploying/aem-version-updates.md) di AEM as a Cloud Service garantiscono la protezione delle istanze e l&#39;aggiornamento alle ultime versioni di manutenzione. Detto questo, in alcuni casi (come eventi di pubblicazione) potrebbe essere necessario &quot;proteggere&quot; tali ore di lavoro critiche da potenziali interruzioni. AEM as a Cloud Service offre quindi la possibilità di impostare un intervallo di tempo in cui non si verificano aggiornamenti automatici per i programmi in corso.

È possibile configurare questi intervalli di tempo utilizzando due opzioni di pianificazione:

* **Ore non interattive** - È possibile definire un intervallo di tempo giornaliero (fino a 8 ore) in cui non verranno eseguiti aggiornamenti.
* **Aggiorna periodi liberi** - È possibile definire un periodo di tempo di 7 giorni in cui gli aggiornamenti non verranno eseguiti. È possibile avere fino a tre periodi liberi di aggiornamento in un intervallo di 12 mesi.

Le funzioni di aggiornamento dei periodi liberi e delle ore non interattive sono configurate in base al singolo programma.

Inoltre, per informazioni sui periodi di manutenzione automatica pianificati per AEM as a Cloud Service, consulta la pagina [Roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

## Ore non interattive {#quiet-hours}

Utilizzando la funzione ore non interattive è possibile definire una finestra temporale durante il giorno senza alcun aggiornamento automatico. Tutti gli aggiornamenti di manutenzione verranno eseguiti all’esterno dell’intervallo di tempo configurato. Se, ad esempio, un aggiornamento è pianificato durante le ore non interattive specificate, verrà avviato automaticamente al termine dell&#39;intervallo. L’intervallo di tempo configurato non può superare le 8 ore, pertanto gli aggiornamenti possono comunque essere eseguiti ogni giorno.

Puoi definire queste ore non interattive **per programma**, utilizzando il tuo fuso orario locale.

### Come configurare l’intervallo di ore non interattive {#configure-quiet-hours}

L’intervallo di ore non interattive può essere configurato utilizzando l’interfaccia di AEM Cloud Manager come segue:

Vai a **Attività>Aggiornamenti automatici>Opzioni di aggiornamento**.

![Configurazione](assets/main-config.png)

1. Assicurarsi che l&#39;opzione **Impedisci aggiornamenti automatici durante ore specifiche** sia attivata.
2. Fai clic su **Modifica**.
3. Impostare l&#39;intervallo di ore non interattive nella finestra di configurazione.

![Configurazione ore di pausa](assets/quiet-hours.png)

Una volta impostati, gli orari di inizio e di fine specificati verranno applicati a ogni giorno di calendario successivo. Se necessario, puoi disabilitare o riconfigurare il valore relativo alle ore non interattive.

## Aggiorna periodi liberi {#update-free-periods}

Utilizzando la funzione di aggiornamento periodi liberi è possibile definire un intervallo di tempo di 7 giorni in cui gli aggiornamenti non verranno eseguiti. Una volta configurati, tutti gli aggiornamenti di manutenzione verranno eseguiti automaticamente al di fuori dell’intervallo di tempo definito. In un intervallo di 12 mesi è possibile disporre di un massimo di tre periodi liberi di aggiornamento. Inoltre, i periodi gratuiti di aggiornamento possono essere designati con un anticipo fino a un anno.

Tieni presente che, per facilitare gli aggiornamenti automatici, è obbligatorio un intervallo di tempo di almeno una settimana tra i periodi. Di conseguenza, questo intervallo di tempo di una settimana viene applicato automaticamente e verrà aggiunto al calendario tra i periodi liberi di aggiornamento configurati. Di conseguenza, alcuni giorni di calendario non sono disponibili per la selezione.

Puoi definire i periodi liberi di aggiornamento **per programma**.

### Come configurare i periodi liberi di aggiornamento {#configure-update-free-periods}

La funzione di aggiornamento dei periodi liberi può essere configurata utilizzando l’interfaccia di AEM Cloud Manager nel modo seguente:

Vai a **Attività>Aggiornamenti automatici>Opzioni di aggiornamento**.

![Configurazione](assets/main-config.png)

1. Passare alla sezione Aggiornamento periodi liberi.
2. Fai clic su **Aggiungi aggiornamento periodo gratuito**.
3. Seleziona un periodo gratuito di aggiornamento di una settimana dal calendario.

![Aggiorna configurazione periodi liberi](assets/update-free-periods.png)

Un&#39;icona **Attivo** verrà visualizzata accanto al periodo di disponibilità dell&#39;aggiornamento attualmente attivo e un&#39;icona **Completo** accanto ai periodi di disponibilità dell&#39;aggiornamento completati.
