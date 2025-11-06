---
title: Introduzione ai programmi sandbox
description: Scopri cosa sono i programmi sandbox e come si differenziano dai programmi di produzione.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 32%

---


# Introduzione ai programmi sandbox {#sandbox-programs}

Scopri cosa sono i programmi sandbox e come si differenziano dai programmi di produzione.

## Introduzione {#introduction}

Un programma sandbox viene tipicamente creato per scopi di formazione, esecuzione di demo, attivazione o modelli di verifica (POC) e non è quindi destinato a contenere traffico in tempo reale.

Un programma sandbox è uno dei due tipi di programmi disponibili in AEM Cloud Service; l&#39;altro è un [programma di produzione](introduction-production-programs.md). Per ulteriori informazioni sui tipi di programmi, vedere [Informazioni su programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## Creazione automatica {#auto-creation}

I programmi sandbox dispongono della funzionalità di creazione automatica. Ogni volta che [crei un programma sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md), Cloud Manager automaticamente:

* Aggiunge al programma le soluzioni predefinite AEM Sites, Assets e Edge Delivery Services.

  ![Selezionare soluzioni e componenti aggiuntivi per una sandbox](assets/sandbox-solutions-add-ons.png)

* Imposta un archivio Git del progetto con un progetto di esempio basato sull&#39;[Archetipo progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview).
* Crea un ambiente di sviluppo.
* Crea una pipeline non di produzione da distribuire nell’ambiente di sviluppo.

Un programma sandbox dispone di un solo ambiente di sviluppo.

## Note e condizioni di utilizzo {#usage-notes-conditions}

Poiché non sono destinati al traffico live, i programmi sandbox presentano determinate limitazioni e condizioni di utilizzo, che li differenziano dai programmi di produzione.

| Limitazione/condizione | Descrizione |
| --- | --- |
| Nessun traffico live | I programmi sandbox non sono destinati a contenere traffico in tempo reale e non sono pertanto soggetti a [impegni AEM as a Cloud Service](https://www.adobe.com/it/legal/service-commitments.html). |
| Ridimensionamento automatico non disponibile | Gli ambienti creati in un programma sandbox non sono configurati per il ridimensionamento automatico. Pertanto, questi ambienti non sono adatti per il test delle prestazioni o del carico. |
| Nessun dominio o Elenco consentiti IP personalizzato | [I domini personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md) e [Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) non sono disponibili nei programmi sandbox. |
| Nessuna area geografica di pubblicazione aggiuntiva | [Altre aree geografiche di pubblicazione](/help/operations/additional-publish-regions.md) non sono disponibili nei programmi sandbox. |
| No 99,99% SLA | [99,99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) non è applicabile ai programmi sandbox. |
| Nessuna rete avanzata | [Funzionalità di rete avanzate](/help/security/configuring-advanced-networking.md) (ad esempio, il provisioning self-service di VPN, porte non standard, indirizzi IP in uscita dedicati e così via) non sono disponibili nei programmi sandbox. |
| Nessun aggiornamento automatico di AEM | Gli aggiornamenti di AEM non vengono eseguiti automaticamente per i programmi sandbox, ma possono essere applicati manualmente agli ambienti nel programma sandbox.<br>· È possibile eseguire un aggiornamento manuale solo quando nell&#39;ambiente di destinazione è presente una pipeline configurata correttamente.<br>· Un aggiornamento manuale a un ambiente di produzione o di gestione temporanea aggiorna automaticamente l&#39;altro. Il set di ambienti Produzione + Staging deve avere la stessa versione di AEM.<br>Per ulteriori dettagli, consulta [Aggiornamenti della versione di AEM](/help/implementing/deploying/aem-version-updates.md).<br>Consulta [Aggiornamento dell&#39;ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) per scoprire come aggiornare un ambiente. |
| Nessun supporto tecnico | Poiché un programma sandbox viene generalmente creato a scopi di formazione, esecuzione di demo, abilitazione o POC (proof of concepts, verifica dei concetti), il supporto tecnico non è disponibile per i problemi riscontrati in un programma sandbox.<br>In caso di problemi durante la creazione e la gestione dei programmi sandbox, tali problemi rientrano nell&#39;ambito del supporto tecnico. |
| Sospensione ed eliminazione | Gli ambienti in un programma sandbox vengono automaticamente sospesi dopo otto ore di inattività. Gli ambienti sandbox vengono eliminati dopo sei mesi continuativi di ibernazione.<br>Consulta [Sospensione e riattivazione degli ambienti sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) per ulteriori dettagli su come riattivare gli ambienti e l&#39;eliminazione automatica delle sandbox. |
