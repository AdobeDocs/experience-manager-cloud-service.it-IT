---
title: Utilizzo della pubblicazione selettiva in Dynamic Media
description: Scopri come utilizzare Selective Publish in Dynamic Medie.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Publishing,Dynamic Media
role: User
exl-id: a5a2df68-be13-45a6-ad80-09fbd2fea8f2
source-git-commit: 26afff3a39a2a80c1f730287b99f3fb33bff0673
workflow-type: tm+mt
source-wordcount: '2946'
ht-degree: 3%

---

# Configurare Selective Publish a livello di cartella in Dynamic Medie {#selective-publish-configure-folder}

Puoi scegliere di pubblicare o annullare la pubblicazione delle risorse su o da Adobe Experience Manager o Dynamic Medie. Puoi eseguire questa operazione a livello di cartella utilizzando **[!UICONTROL Gestisci pubblicazione]** o **[!UICONTROL Publish rapido]**. Questo metodo di pubblicazione è utile perché non si basa esclusivamente sulla **[!UICONTROL configurazione di Dynamic Medie]**, le cui impostazioni sono globali per tutte le cartelle nell&#39;istanza di Dynamic Medie.

Ad esempio, con la pubblicazione selettiva è possibile lavorare su risorse per prodotti non ancora live. In questo caso, un team di marketing può accedere alle immagini con ritaglio avanzato e alle rappresentazioni dinamiche sincronizzate con Dynamic Medie. Possono creare materiali promozionali senza dover pubblicare tali risorse su Dynamic Medie per la distribuzione globale.

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Se si copiano* risorse da e verso le cartelle, lo stato di pubblicazione di tali risorse viene cancellato. Tuttavia, quando *sposti* risorse in e da cartelle la cui proprietà cartella è impostata su **[!UICONTROL Publish selettivo]**, lo stato di pubblicazione di tali risorse viene mantenuto.

Se successivamente decidi di modificare le impostazioni di **[!UICONTROL Publish]** selettivo in una cartella, tali modifiche interesseranno solo le nuove risorse caricate in tale cartella da quel momento in poi. Lo stato di pubblicazione delle risorse esistenti nella cartella rimane invariato finché non vengono modificate manualmente da **[!UICONTROL Quick Publish]** o dalla finestra di dialogo **[!UICONTROL Gestisci pubblicazione]**.

L&#39;opzione di livello cartella **[!UICONTROL Modalità Publish Dynamic Medie]** utilizza sempre per impostazione predefinita il valore presente nell&#39;impostazione **[!UICONTROL Assets]** di Publish nella **[!UICONTROL Configurazione Dynamic Medie]**. Nei passaggi seguenti di questo argomento viene tuttavia illustrato come modificare manualmente questo valore predefinito a livello di cartella (come descritto nei passaggi seguenti) per ignorare il valore di **[!UICONTROL Configurazione Dynamic Medie]**.

Indipendentemente dal fatto che ci si basi su:

* Il valore **[!UICONTROL Publish Assets]** impostato in **[!UICONTROL Configurazione Dynamic Medie]**
* Oppure, il valore **[!UICONTROL modalità Publish di Dynamic Medie]** impostato nelle proprietà a livello di cartella

Puoi comunque scegliere **[!UICONTROL Immediatamente]**, **[!UICONTROL All&#39;attivazione]** o **[!UICONTROL Publish selettivo]**. Ad esempio, puoi impostare il valore **[!UICONTROL Publish Assets]** nella **[!UICONTROL Configurazione Dynamic Medie]** su **[!UICONTROL All&#39;attivazione]**. È inoltre possibile impostare il valore della modalità **[!UICONTROL Dynamic Medie Publish]** a livello di cartella su **[!UICONTROL Selective Publish]**, viceversa e così via.

Dopo aver configurato la pubblicazione selettiva in una cartella, puoi effettuare una delle seguenti operazioni:

* [Pubblica selettivamente le risorse in Dynamic Medie o Experience Manager utilizzando Gestisci pubblicazione](#selective-publish-manage-publication).
* [Annullamento selettivo della pubblicazione di risorse da Dynamic Medie o Experience Manager tramite Gestisci pubblicazione](#selective-unpublish-manage-publication).
* [Risorse Publish in Dynamic Medie o Experience Manager tramite Quick Publish](#quick-publish-aem-dm).
* [Pubblicare o annullare la pubblicazione selettiva delle risorse in base ai risultati della ricerca](#selective-publish-unpublish-search-results).

**Per configurare Publish selettivo a livello di cartella in Dynamic Medie:**

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi vai a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Effettua una delle operazioni seguenti:
   * Modifica le proprietà di una cartella esistente. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, accedi a una cartella di cui desideri modificare le proprietà. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]**.
   * Modifica le proprietà di una nuova cartella. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, nell&#39;angolo superiore destro della pagina, vai a **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**. Nella finestra di dialogo **[!UICONTROL Crea cartella]**, immetti un titolo (obbligatorio) per la cartella, quindi seleziona **[!UICONTROL Crea]**. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]**.

1. Nell&#39;elenco a discesa **[!UICONTROL Modalità di sincronizzazione]** selezionare una delle opzioni seguenti:

   | Modalità di sincronizzazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ereditato]** | Nessun valore di sincronizzazione esplicito nella cartella. La cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o dalla modalità predefinita impostata nella **[!UICONTROL configurazione Dynamic Medie]**. Lo stato dettagliato di **[!UICONTROL Ereditato]** viene visualizzato tramite una descrizione comando. |
   | **[!UICONTROL Sincronizza tutto il contenuto di questa sottostruttura di cartelle con Dynamic Medie]** | Affinché la pubblicazione in Dynamic Medie venga eseguita correttamente, le risorse devono essere sincronizzate in Dynamic Medie. Selezionando questa opzione vengono incluse tutte le risorse di questa sottostruttura per la sincronizzazione con Dynamic Medie. Le impostazioni specifiche della cartella sostituiscono l&#39;impostazione predefinita nella **[!UICONTROL configurazione Dynamic Medie]**. |
   | **[!UICONTROL Escludi tutto il contenuto di questa sottostruttura di cartelle dalla sincronizzazione di Dynamic Medie]** | Escludi tutte le risorse in questa sottostruttura dalla sincronizzazione con Dynamic Medie. |

   ![Pubblicazione selettiva a livello di cartella](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Selezionare un&#39;opzione nell&#39;elenco a discesa **[!UICONTROL Modalità Publish Dynamic Medie]**. L&#39;opzione **[!UICONTROL Modalità Publish Dynamic Medie]** utilizza sempre per impostazione predefinita il valore impostato nella **[!UICONTROL Configurazione Dynamic Medie]**. È tuttavia possibile sostituire manualmente il valore predefinito **[!UICONTROL Configurazione Dynamic Medie]** utilizzando una delle opzioni seguenti.

   >[!IMPORTANT]
   >
   >Indipendentemente dall&#39;opzione della modalità Dynamic Medie Publish selezionata, gli eventuali aggiornamenti apportati successivamente a una risorsa *già* pubblicata verranno pubblicati immediatamente senza ulteriori azioni da parte dell&#39;utente.

   | Opzione modalità Dynamic Medie Publish | Descrizione |
   | --- | --- |
   | **[!UICONTROL Immediatamente]** | Quando le risorse vengono caricate in questa cartella, il sistema acquisisce le risorse in Experience Manager e fornisce immediatamente l’URL/Incorpora. Questa opzione è associata solo alla pubblicazione Experience Manager e non è necessario alcun intervento da parte dell’utente per pubblicare le risorse.<br>Questa opzione è *non* disponibile se hai selezionato **[!UICONTROL Escludi tutti gli elementi di questa sottostruttura di cartelle dalla sincronizzazione di Dynamic Medie]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |
   | **[!UICONTROL All&#39;attivazione]** | Quando le risorse vengono caricate in questa cartella, devi pubblicarle esplicitamente prima di fornire un URL o un collegamento di incorporamento. Questa opzione è associata solo alla pubblicazione Experience Manager.<br>Questa opzione è *non* disponibile se hai selezionato **[!UICONTROL Escludi tutti gli elementi di questa sottostruttura di cartelle dalla sincronizzazione di Dynamic Medie]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |
   | **[!UICONTROL Publish selettivo]** | Assets vengono pubblicati nell’Experience Manager o in Dynamic Medie a tua scelta per la distribuzione nel dominio pubblico. Entrambi i metodi di pubblicazione si escludono a vicenda. In altre parole, puoi pubblicare le risorse in DMS7 per utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche. In alternativa, puoi pubblicare le risorse esclusivamente in Experience Manager per una visualizzazione protetta in anteprima; le stesse risorse sono *non* pubblicate in DMS7 per la distribuzione nel dominio pubblico. Questa opzione non è disponibile se hai selezionato **[!UICONTROL Escludi tutti gli elementi di questa sottostruttura di cartelle dalla sincronizzazione di Dynamic Medie]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |

1. Nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Salva e chiudi]**, quindi seleziona **[!UICONTROL OK]** per tornare a Experience Manager Assets.

## Pubblicare selettivamente le risorse in Dynamic Medie Experience Manager o in un as a Cloud Service tramite Gestisci pubblicazione{#selective-publish-manage-publication}

Prima di poter utilizzare **[!UICONTROL Gestisci pubblicazione]** per pubblicare selettivamente le risorse in Dynamic Medie o in Experience Manager, assicurati di aver eseguito una delle seguenti operazioni:

* Impostare l&#39;opzione **[!UICONTROL Publish Assets]** in **[!UICONTROL Configurazione Dynamic Medie]** su **[!UICONTROL Publish selettivo]**.
* Oppure, è stata configurata la pubblicazione selettiva a livello di cartella.

Vedere [Creare una configurazione di Dynamic Medie](#configuring-dynamic-media-cloud-services) o [Configurare Publish selettivo a livello di cartella in Dynamic Medie](#selective-publish-configure-folder)

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Se si copiano* risorse da e verso le cartelle, lo stato di pubblicazione di tali risorse viene cancellato. Tuttavia, quando *sposti* risorse in e da cartelle la cui proprietà cartella è impostata su **[!UICONTROL Publish selettivo]**, lo stato di pubblicazione di tali risorse viene mantenuto.

**Per pubblicare selettivamente le risorse in Dynamic Medie o in Experience Manager as a Cloud Service con Gestisci pubblicazione:**

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi vai a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, eseguire una delle operazioni seguenti:
   * Passa a una cartella di cui desideri pubblicare le risorse. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, selezionare **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

     >[!NOTE]
     >
     >Se **[!UICONTROL Gestisci pubblicazione]** non è visualizzato nella barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu elenco.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]**, in **[!UICONTROL Azione]**, selezionare il tipo di attivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Publish]** (a Experience Manager) | Per pubblicare le risorse su Experience Manager per l’anteprima protetta, seleziona questa opzione. |
   | **[!UICONTROL Publish a Dynamic Medie]** | Per pubblicare le risorse in Dynamic Medie per la distribuzione nel dominio pubblico o in modo da poter utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche, seleziona questa opzione.<br>Questa opzione è disponibile solo se **[!UICONTROL la modalità Publish di Dynamic Medie]** è impostata su **[!UICONTROL Publish selettivo]** nelle proprietà della cartella. |

1. In **[!UICONTROL Pianificazione]**, impostare la tempistica della pubblicazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona questa opzione per pubblicare immediatamente le risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona questa opzione per pubblicare le risorse in una data e un’ora specifiche. |

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione]**, seleziona **[!UICONTROL Successivo]**.
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:
   * Se necessario, seleziona una o più risorse da rimuovere dalla pubblicazione.
   * Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, selezionare **[!UICONTROL Publish]** o **[!UICONTROL Publish in Dynamic Medie]**.
1. Selezionare **[!UICONTROL OK]**.

### Annullare la pubblicazione selettiva di risorse da Dynamic Medie o Experience Manager tramite Gestisci pubblicazione {#selective-unpublish-manage-publication}

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi vai a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, eseguire una delle operazioni seguenti:
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, selezionare **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

     >[!NOTE]
     >
     >Se **[!UICONTROL Gestisci pubblicazione]** non è visualizzato nella barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu elenco.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]**, in **[!UICONTROL Azione]**, selezionare il tipo di disattivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla pubblicazione]** (da Experience Manager) | Per annullare la pubblicazione delle risorse da Experience Manager, seleziona questa opzione. |
   | **[!UICONTROL Annulla pubblicazione da Dynamic Medie]** | Per annullare la pubblicazione delle risorse da Dynamic Medie, seleziona questa opzione.<br>Questa opzione è disponibile solo se **[!UICONTROL la modalità Publish di Dynamic Medie]** è impostata su **[!UICONTROL Publish selettivo]** nelle proprietà della cartella. |

1. In **[!UICONTROL Pianificazione]**, impostare la tempistica della disattivazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona questa opzione per annullare subito la pubblicazione delle risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona questa opzione per annullare la pubblicazione delle risorse in una data e un’ora specifiche. |

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione]**, seleziona **[!UICONTROL Successivo]**.
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:
   * Seleziona una o più risorse da rimuovere per annullare la pubblicazione.
   * Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, selezionare **[!UICONTROL Annulla pubblicazione]** o **[!UICONTROL Annulla pubblicazione da Dynamic Medie]**.
1. Selezionare **[!UICONTROL OK]**.

## Risorse Publish per Dynamic Medie o Experience Manager tramite Quick Publish {#quick-publish-aem-dm}

È possibile utilizzare **[!UICONTROL Quick Publish]** per casi di attivazione di risorse semplici. **[!UICONTROL Publish rapido]** pubblica immediatamente le risorse selezionate senza ulteriore interazione da parte dell&#39;utente. Vengono pubblicati automaticamente anche tutti i riferimenti non pubblicati.

>[!NOTE]
>
>Per utilizzare **[!UICONTROL Quick Publish]** per pubblicare risorse in Dynamic Medie o Experience Manager, assicurati che **[!UICONTROL Selective Publish]** sia abilitato nella **[!UICONTROL Configurazione Dynamic Medie]** o nelle proprietà della cartella selezionata.

**Per pubblicare risorse in Dynamic Medie o Experience Manager utilizzando Quick Publish:**

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi sul lato destro della pagina passa a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, eseguire una delle operazioni seguenti:
   * Passa a una cartella di cui desideri pubblicare le risorse. Selezionare la cartella, quindi sulla barra degli strumenti selezionare **[!UICONTROL Publish rapido]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, selezionare **[!UICONTROL Publish rapido]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

     >[!NOTE]
     >
     >Se **[!UICONTROL Publish rapido]** non è visualizzato nella barra degli strumenti, selezionare il pulsante con i puntini di sospensione, quindi selezionare **[!UICONTROL Publish rapido]** dal menu elenco.

     ![Publish rapido a livello di cartella a Dynamic Medie](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Selezionare una delle opzioni seguenti dall&#39;elenco del menu **[!UICONTROL Publish rapido]**.

   | Publish rapido, opzione | Effetto |
   | --- | --- | 
   | Publish all&#39;Experience Manager | Pubblica immediatamente su Experience Manager le risorse selezionate. |
   | Pubblica su Brand Portal | Pubblica immediatamente le risorse selezionate in **[!UICONTROL Brand Portal]**.<br>Questa opzione è disponibile solo se nell&#39;istanza di Experience Manager Assets è già configurato **[!UICONTROL Brand Portal]**. |
   | Pubblica in Dynamic Media | Pubblica immediatamente le risorse selezionate in Dynamic Medie.<br>Una risorsa deve già essere sincronizzata con Dynamic Medie. Se necessario, verificare che la modalità di sincronizzazione **[!UICONTROL Modalità di sincronizzazione]** nelle proprietà di una cartella sia già impostata su **[!UICONTROL Sincronizza tutto il contenuto di questa sottostruttura di cartelle con Dynamic Medie]**. |

1. Seleziona **[!UICONTROL OK]**, quindi seleziona **[!UICONTROL Chiudi]**.

## Pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca {#selective-publish-unpublish-search-results}

I risultati della ricerca possono mostrare le risorse di più cartelle di risorse con impostazioni di pubblicazione di Dynamic Medie diverse. Se hai selezionato una o più risorse dai risultati della ricerca e le risorse hanno impostazioni diverse della modalità di pubblicazione di Dynamic Medie, puoi attivare **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti, per pubblicarle o annullarne la pubblicazione.

Vedi anche [Cercare risorse in Experience Manager](/help/assets/search-assets.md).

**Per pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca:**

1. Ad Experience Manager, nell’angolo superiore sinistro della pagina, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi vai a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Sulla barra degli strumenti, nell&#39;angolo superiore destro della pagina, selezionare l&#39;icona Ricerca (lente di ingrandimento).
1. Nel campo di testo **[!UICONTROL Digitare per cercare]**, immettere una parola chiave, quindi premere **[!UICONTROL Invio]**.
1. Fai clic sull&#39;icona **[!UICONTROL Vista a elenco]** nell&#39;angolo superiore destro della pagina.
1. Seleziona l&#39;icona **[!UICONTROL Filtri]** nell&#39;angolo superiore sinistro della pagina.

   ![Visualizzazione elenco e filtri nei risultati di ricerca](/help/assets/assets-dm/select-publish-search-result.png)

1. Nel pannello a sinistra, espandi **[!UICONTROL Stato]**, quindi espandi il predicato di ricerca **[!UICONTROL Dynamic Medie]**.
1. Utilizza le caselle di controllo **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]** per perfezionare ulteriormente i risultati della ricerca in base allo stato pubblicato delle risorse di Dynamic Medie.
Facoltativamente, è possibile utilizzare queste caselle di controllo con il predicato di ricerca **[!UICONTROL Publish]** per perfezionare i risultati della ricerca di risorse di Experience Manager **[!UICONTROL Pubblicate]** e **[!UICONTROL Non pubblicate]**.
1. Effettua una delle operazioni seguenti:
   * Seleziona una o più risorse da pubblicare o di cui annullare la pubblicazione.
   * Selezionare **[!UICONTROL Seleziona tutto]** nell&#39;angolo superiore destro della pagina **[!UICONTROL Risultati ricerca]**.
1. Sulla barra degli strumenti, selezionare **[!UICONTROL Gestisci pubblicazione]**. Se necessario, seleziona l&#39;icona con i puntini di sospensione sulla barra degli strumenti per visualizzare **[!UICONTROL Gestisci pubblicazione]**.
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]** selezionare l&#39;azione desiderata.

   | Azione selezionata | Impostazione di Publish Assets nella configurazione di Dynamic Medie | Assets sono |
   | --- | --- | --- |
   | Pubblicazione | Immediatamente o Al momento dell&#39;attivazione | Pubblicato in Experience Manager e Dynamic Medie. |
   | Pubblicazione | Pubblicazione selettiva | Pubblicato solo su Experience Manager. |
   | Annulla pubblicazione | Immediatamente o Al momento dell&#39;attivazione | Non più pubblicato su Experience Manager e Dynamic Medie. |
   | Annulla pubblicazione | Pubblicazione selettiva | Pubblicazione annullata solo da Experience Manager. |
   | Pubblica in Dynamic Media | Immediatamente o Al momento dell&#39;attivazione | Non pubblicato su Experience Manager, Dynamic Medie o entrambi. |
   | Pubblica in Dynamic Media | Pubblicazione selettiva | Pubblicato solo in Dynamic Medie. |
   | Annulla pubblicazione da Dynamic Media | Immediatamente o Al momento dell&#39;attivazione | Pubblicazione non annullata da Experience Manager, Dynamic Medie o entrambi. |
   | Annulla pubblicazione da Dynamic Media | Pubblicazione selettiva | Pubblicazione annullata solo da Dynamic Medie. |

1. In **[!UICONTROL Pianificazione]**, impostare la tempistica della disattivazione.

   | Pianificazione selezionata | Cosa succede |
   | --- | --- |
   | Adesso | L&#39;azione selezionata viene eseguita immediatamente. |
   | Più tardi | L&#39;azione selezionata viene eseguita nella data e ora specifiche selezionate. |

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]**, selezionare **[!UICONTROL Successivo]**.
1. (Facoltativo) Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, controlla la colonna **[!UICONTROL Publish Target]** nella tabella per le risorse selezionate.

   | Impostazione di Publish Assets nella configurazione di Dynamic Medie | Azione selezionata | destinazione Publish |
   | --- | --- | --- |
   | Immediatamente o <br>All&#39;attivazione | Pubblicazione | EXPERIENCE MANAGER e DYNAMIC MEDIE |
   | Immediatamente o <br>All&#39;attivazione | Pubblica in Dynamic Media | Nessuno |
   | Pubblicazione selettiva | Pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Pubblica in Dynamic Media | Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione | EXPERIENCE MANAGER e DYNAMIC MEDIE |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione da Dynamic Media | Nessuno |
   | Pubblicazione selettiva | Annulla pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Annulla pubblicazione da Dynamic Media | Dynamic Media |

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:
   * Seleziona una o più risorse da rimuovere dalla pubblicazione o dall’annullamento della pubblicazione.
   * Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, selezionare **[!UICONTROL Publish]** o **[!UICONTROL Annulla pubblicazione]** per iniziare l&#39;azione.
1. Selezionare **[!UICONTROL OK]**.

## Controllare lo stato di pubblicazione di una risorsa {#check-publish-status-of-asset}

Puoi utilizzare **[!UICONTROL Timeline]** con **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]** nell&#39;Experience Manager per verificare rapidamente lo stato di pubblicazione di una risorsa.

**Per verificare lo stato di pubblicazione di una risorsa:**

1. Ad Experience Manager, nell’angolo superiore sinistro della pagina, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi vai a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]** (la schermata seguente mostra la **[!UICONTROL Vista a elenco]**), apri una cartella contenente le risorse pubblicate o non pubblicate.
1. Seleziona una risorsa affinché venga visualizzata con un segno di spunta. Vedi la schermata seguente, ad esempio.
1. Seleziona **[!UICONTROL Timeline]** dal menu a discesa nell&#39;angolo superiore sinistro della pagina. L&#39;area **[!UICONTROL Stato]** nel pannello a sinistra mostra lo stato di pubblicazione della risorsa selezionata.
Quando si utilizza **[!UICONTROL Vista a elenco]**, viene visualizzata una colonna aggiuntiva per lo stato di pubblicazione **[!UICONTROL Dynamic Medie]**.
   * Una cartella configurata per la sincronizzazione con Dynamic Medie visualizza la colonna **[!UICONTROL Dynamic Medie]** per impostazione predefinita.
   * Una cartella *non* configurata per la sincronizzazione con Dynamic Medie non visualizza la colonna Dynamic Medie.
     ![Visualizzazione elenco e sequenza temporale](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Risolvere i problemi relativi a Selective Publish {#selective-publish-troubleshoot}

Una risorsa non sincronizzata in Dynamic Medie ma su cui è attivata un’azione di pubblicazione Dynamic Medie genera il messaggio di errore e la soluzione seguenti:

![Errore selettivo di Publish](/help/assets/assets-dm/selective-publish-error.png)
