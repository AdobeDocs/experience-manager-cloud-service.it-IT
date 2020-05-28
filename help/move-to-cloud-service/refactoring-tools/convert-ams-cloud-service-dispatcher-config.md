---
title: Conversione di un AMS in Adobe Experience Manager come configurazione del dispatcher di servizi cloud
description: Conversione di un AMS in Adobe Experience Manager come configurazione del dispatcher di servizi cloud
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---


# Conversione di un AMS in Adobe Experience Manager (AEM) come configurazione del dispatcher di servizi cloud

## Introduzione {#introduction}

Questa sezione fornisce istruzioni dettagliate su come convertire una configurazione AMS.

>[!NOTE]
>Si parte dal presupposto che disponiate di un archivio con una struttura simile a quella descritta in [Gestione delle configurazioni](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)del dispatcher.

## Passaggi per la conversione di un AMS in AEM come configurazione del dispatcher di servizi cloud

1. **Estrarre l&#39;archivio e rimuovere un eventuale prefisso**

   Estrarre l&#39;archivio in una cartella e assicurarsi che le sottocartelle immediate inizino con conf, conf.d, conf.dispatcher.d e conf.module.d. In caso contrario, spostateli nella gerarchia.

1. **Eliminare le sottocartelle e i file non utilizzati**

   Rimuovete le sottocartelle conf e conf.module.d, nonché i file che corrispondono a conf.d/*.conf.

1. **Eliminazione di tutti gli host virtuali non pubblicati**

1. **Rimuovere un file host virtuale**

   In conf.d/enabled_vhosts con il nome autore, non integro, integrità, lc o scaricamento. È possibile rimuovere anche tutti i file host virtuali in conf.d/available_hosts non collegati.

1. Rimuovere o commentare sezioni di host virtuali che non fanno riferimento alla porta 80

   Se i file host virtuali contengono ancora sezioni che fanno riferimento esclusivamente a porte diverse dalla porta 80, ad esempio

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
rimuovete o commentateli. Le istruzioni in queste sezioni non verranno elaborate, ma se le si mantiene in giro, si potrebbe comunque finire per modificarle senza alcun effetto, il che crea confusione.

1. **Verifica riscrittura**

   * Immettere la directory conf.d/rewrite.

   * Rimuovete qualsiasi file denominato base_rewrite.rules e xinoltrato_forcessl_rewrite.rules e ricordate di rimuovere le istruzioni Include nei file host virtuali che vi fanno riferimento.

   * Se conf.d/rewrite ora contiene un singolo file, deve essere rinominato in rewrite.rules e non dimenticare di adattare le istruzioni Include che fanno riferimento a tale file anche nei file host virtuali.

   * Se tuttavia la cartella contiene più file specifici dell&#39;host virtuale, il relativo contenuto deve essere copiato nell&#39;istruzione Include che li fa riferimento nei file host virtuali.

1. **Verifica variabili**

   1. Immettere la directory conf.d/variables.

   1. Rimuovete qualsiasi file denominato ams_default.vars e ricordate di rimuovere le istruzioni Include nei file host virtuali che vi fanno riferimento.

   1. Se le variabili conf.d/variables ora contengono un singolo file, è necessario rinominarlo custom.vars e non dimenticare di adattare le istruzioni Include che fanno riferimento a tale file anche nei file host virtuali.

   1. Se tuttavia la cartella contiene più file specifici dell&#39;host virtuale, il relativo contenuto deve essere copiato nell&#39;istruzione Include che li fa riferimento nei file host virtuali.

1. **Rimuovi whitelist**

   Rimuovete la cartella conf.d/whitelist e rimuovete le istruzioni Include nei file host virtuali che fanno riferimento ad alcuni file nella sottocartella.

1. **Sostituisce qualsiasi variabile non più disponibile**

   In tutti i file host virtuali:

   Rinominare PUBLISH_DOCROOT in sezioni DOCROOTRemove facendo riferimento a variabili denominate DISP_ID, PUBLISH_FORCE_SSL o PUBLISH_WHITELIST_ENABLED

1. **Controllare lo stato eseguendo la convalida**

   Eseguire il dispatcher validator nella directory, con il sottocomando httpd:

   `$ validator httpd`
Se si verificano degli errori relativi ai file di inclusione mancanti, verificate di aver rinominato correttamente tali file.

   Se vengono visualizzate delle direttive Apache che non sono inserite nella white list, rimuoverle.

1. **Eliminazione di tutte le farm non pubblicate**

   Rimuovete qualsiasi file della farm in conf.dispatcher.d/enabled_farm il cui nome contiene l&#39;autore, l&#39;integrità, l&#39;lc o lo scaricamento è dannoso. È inoltre possibile rimuovere tutti i file della farm in conf.dispatcher.d/available_farm non collegati.

1. **Rinominare i file della farm**

   Tutte le farm in conf.dispatcher.d/enabled_farm devono essere rinominate in modo da corrispondere al pattern *.farm, pertanto, ad esempio, un file farm denominato customerX_farm.any deve essere rinominato customerX.farm.

1. **Controlla cache**

   Immettere la directory conf.dispatcher.d/cache.

   Rimuovete eventuali file con prefisso ams_.

   Se conf.dispatcher.d/cache è ora vuoto, copiate il file conf.dispatcher.d/cache/rules.any dalla configurazione standard del dispatcher in questa cartella. La configurazione standard del dispatcher si trova nella cartella src di questo SDK. Non dimenticare di adattare le istruzioni $include che fanno riferimento ai file di regole ams_*_cache.any anche nei file della farm.

   Se invece conf.dispatcher.d/cache ora contiene un singolo file con suffisso _cache.any, deve essere rinominato in rules.any e non dimenticare di adattare le istruzioni $include che fanno riferimento a tale file anche nei file della farm.

   Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nell&#39;istruzione $include che fa riferimento a tali file nei file della farm.

   Rimuovete qualsiasi file con il suffisso _invalidate_Allowiany.

   Copiare il file conf.dispatcher.d/cache/default_invalidate_any dalla configurazione del dispatcher predefinito a tale posizione.

   In ciascun file della farm, rimuovete eventuale contenuto nella sezione cache/allowClient e sostituitelo con:

   $include &quot;../cache/default_invalidate.any&quot;

1. **Verifica intestazioni client**

   Immettere la directory conf.dispatcher.d/clientheaders.

   Rimuovete eventuali file con prefisso ams_.

   Se conf.dispatcher.d/clientheaders contiene ora un singolo file con suffisso _clientheaders.any, deve essere rinominato in clientheaders.any e non dimenticare di adattare le istruzioni $include relative a tale file anche nei file della farm.

   Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nell&#39;istruzione $include che fa riferimento a tali file nei file della farm.

   Copiate il file conf.dispatcher/clientheaders/default_clientheaders.any dalla configurazione predefinita del dispatcher in quella posizione.

   In ciascun file farm, sostituite le istruzioni include di tipo client che abbiano il seguente aspetto:

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   con l&#39;istruzione:

   `$include "../clientheaders/default_clientheaders.any"`

1. **Filtro controllo**

   * Immettere la directory conf.dispatcher.d/Filters.

   * Rimuovete eventuali file con prefisso ams_.

   * Se conf.dispatcher.d/filter ora contiene un singolo file, deve essere rinominato come filter.any e non dimenticare di adattare le istruzioni $include che fanno riferimento a tale file anche nei file della farm.

   * Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nell&#39;istruzione $include che fa riferimento a tali file nei file della farm.

   * Copiate il file conf.dispatcher/filters/default_filters.any dalla configurazione predefinita del dispatcher in quella posizione.

   * In ciascun file farm, sostituire eventuali istruzioni di filtro con le seguenti:

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`con l&#39;istruzione:

      `$include "../filters/default_filters.any"`

1. **Controllare i rendering**

   * Immettere la directory conf.dispatcher.d/renders.

   * Rimuovete tutti i file presenti nella cartella.

   * Copiare il file conf.dispatcher.d/renders/default_renders.any dalla configurazione dispatcher predefinita in quella posizione.

   * In ciascun file della farm, rimuovete eventuale contenuto nella sezione dei rendering e sostituitelo con:

      `$include "../renders/default_renders.any"`

1. **Controllare i virtualhost**

   * Rinominare la directory `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` e immetterla.

   * Rimuovete eventuali file con prefisso `ams_`.

   * Se conf.dispatcher.d/virtualhosts ora contiene un singolo file, dovrebbe essere rinominato come virtualhosts.any e non dimenticare di adattare le istruzioni $include che fanno riferimento a quel file anche nei file della farm.

   * Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nell&#39;istruzione $include che fa riferimento a tali file nei file della farm.

   * Copiate il file conf.dispatcher/virtualhosts/default_virtualhosts.any dalla configurazione predefinita del dispatcher in quella posizione.

   * In ciascun file farm, sostituire eventuali istruzioni di filtro con le seguenti:

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
con l&#39;istruzione:

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **Controllare lo stato eseguendo la convalida**

   * Eseguire il dispatcher validator nella directory, con il sottocomando dispatcher:

      `$ validator dispatcher`

   * Se si verificano degli errori relativi ai file di inclusione mancanti, verificate di aver rinominato correttamente tali file.

   * Se vengono visualizzati errori relativi a una variabile non definita, rinominarla `PUBLISH_DOCROOT`in `DOCROOT`.

   * Per ogni altro errore, vedere la sezione Risoluzione dei problemi della documentazione relativa allo strumento di convalida.

## Verifica della configurazione con una distribuzione locale {#testing-config-local-deployment}

>[!IMPORTANT]
> Il test della configurazione con una distribuzione locale richiede l&#39;installazione di Docker.

Utilizzando lo script `docker_run.sh` nell’SDK del dispatcher, puoi verificare che la configurazione non contenga altri errori che verrebbero visualizzati solo nella distribuzione:

1. Generazione di informazioni sulla distribuzione con il validatore

   `validator full -d out`
In questo modo viene convalidata la configurazione completa e vengono generate le informazioni di distribuzione in

1. Avviare il dispatcher in un&#39;immagine docker con tali informazioni di distribuzione

   Con il server di pubblicazione AEM in esecuzione sul computer MacOS, in ascolto sulla porta 4503, potete avviare il dispatcher davanti al server come segue:

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   Verrà avviato il contenitore ed esporre Apache sulla porta locale 8080.

## Utilizzo della nuova configurazione dispatcher {#using-dispatcher-config}

Se la funzione di convalida non segnala più alcun problema e il contenitore docker si avvia senza errori o avvisi, è possibile spostare la configurazione in una sottodirectory d`ispatcher/src` del repository git.