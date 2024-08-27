---
title: Gestione dei dati di tassonomia
description: Scopri come gestire i dati della tassonomia per utilizzare i tag con il tuo AEM con i siti Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 81aacb0c616490eed4589cb8927ea1316ca1670e
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 7%

---


# Gestione dei dati di tassonomia {#managing-taxonomy-data}

Scopri come gestire i dati della tassonomia per utilizzare i tag con il tuo AEM con i siti Edge Delivery Services.

## Introduzione {#introduction}

L’assegnazione tag è una funzione importante che consente di organizzare e gestire le pagine. [La console Assegnazione tag](/help/sites-cloud/administering/tags.md#tagging-console) in AEM consente di creare una tassonomia avanzata dei tag per organizzare le pagine.

Questi tag sono utili non solo per te e i tuoi autori nell’organizzazione dei contenuti, ma possono anche essere utili per i tuoi lettori. I tag e la relativa tassonomia possono essere utilizzati nei componenti della pagina per facilitare la navigazione del contenuto da parte dei lettori.

L’editor universale funziona solo con gli ID dei tag. Creando una pagina di tassonomia per il contenuto, è possibile esporre le descrizioni di questi tag in tutte le lingue all’Editor universale in modo che possa utilizzare tali informazioni durante il rendering del contenuto.

## Creazione di una pagina di tassonomia {#creating}

Viene creata una tassonomia come [qualsiasi altra pagina in AEM.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. Passa alla console [**Sites**.](/help/sites-cloud/authoring/sites-console/introduction.md)

1. Selezionare il percorso in cui si desidera creare la tassonomia.

1. Tocca o fai clic su **Crea** -> **Pagina**.

   ![Crea pagina](assets/taxonomy/create-page.png)

1. Nella scheda **Modello** della procedura guidata **Crea pagina**, seleziona il modello **Tassonomia** e tocca o fai clic su **Avanti**.

   ![Modello di tassonomia](assets/taxonomy/taxonomy-template.png)

1. Nella scheda **Proprietà** della procedura guidata **Crea pagina**, specifica un **Titolo** significativo per la pagina e nel campo **Tag**, [utilizza il selettore tag](/help/sites-cloud/authoring/sites-console/tags.md) per selezionare i tag o gli spazi dei nomi da includere nella tassonomia.

   ![Proprietà tassonomia](assets/taxonomy/create-page-wizard-properties.png)

1. Tocca o fai clic su **Crea**.

Viene creata la pagina della tassonomia. Nella finestra di dialogo **Operazione completata**, tocca o fai clic sulla finestra di dialogo **Operazione completata** per chiudere il messaggio o su **Apri** per modificare la pagina nell&#39;editor di [pagine.](/help/sites-cloud/authoring/page-editor/introduction.md)

Prendere nota del nome della pagina risultante della tassonomia da utilizzare nei passaggi seguenti.

## Modifica di una pagina di tassonomia {#editing}

Inizia a modificare una pagina della tassonomia come qualsiasi altra pagina in AEM.

1. Passa alla console [**Sites**.](/help/sites-cloud/authoring/sites-console/introduction.md)

1. Selezionare la tassonomia da modificare.

1. Tocca o fai clic su **Modifica** nella barra delle azioni.

1. Viene aperto l’Editor pagina, con la tassonomia.

   * La pagina della tassonomia è di sola lettura nell’Editor pagina.

   ![Modifica tassonomia](assets/taxonomy/edit-page.png)

1. Tocca o fai clic sull&#39;icona **Informazioni pagina** nella barra degli strumenti e seleziona **Apri proprietà**.

   ![Apri proprietà](assets/taxonomy/open-properties.png)

1. Nella finestra **Proprietà pagina**, è possibile aggiornare il nome della pagina e utilizzare il selettore di tag per aggiornare i tag e gli spazi dei nomi inclusi nella tassonomia.

   ![Modifica proprietà pagina](assets/taxonomy/edit-properties.png)

1. Toccare o fare clic su **Salva e chiudi**.

La pagina visualizzata nell’Editor pagina è di sola lettura perché il contenuto della tassonomia viene generato automaticamente dai tag e dagli spazi dei nomi selezionati. Fungono da filtro per generare automaticamente il contenuto della tassonomia. Pertanto, non c’è motivo di modificare direttamente la pagina nell’editor.

AEM aggiorna automaticamente il contenuto della pagina della tassonomia quando si aggiornano i tag e gli spazi dei nomi sottostanti. Tuttavia, è necessario [ripubblicare la tassonomia](#publishing) dopo eventuali modifiche per renderle disponibili agli utenti.

## Aggiornare paths.json per la pubblicazione della tassonomia {#paths-json}

Come quando [gestisci e pubblichi dati tabulari per il tuo sito Edge Delivery Services,](/help/edge/wysiwyg-authoring/tabular-data.md) devi aggiornare il file `paths.json` del tuo progetto per consentire la pubblicazione dei dati della tassonomia.

1. Apri la directory principale del progetto in GitHub.

1. Tocca o fai clic sul file `paths.json` per aprirne i dettagli e quindi l’icona **Modifica**.

   ![paths.json file](assets/taxonomy/paths-json.png)

1. Aggiungere una riga per mappare la nuova pagina della tassonomia a una risorsa `.json`.

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/<taxonomy-page-name>:/<taxonomy-json-name>.json"
     ]
   }
   ```

   * `<taxonomy-page-name>` deve corrispondere al nome della [pagina tassonomia creata.](#creating)
   * `<taxonomy-json-name>` può essere qualsiasi nome valido scelto.

1. Fai clic su **Conferma modifiche...** per salvare le modifiche apportate a `main`.

   * Conferma `main` o crea una richiesta di pull in base al processo.

Questo processo deve essere eseguito una sola volta per pagina di tassonomia. Al termine, puoi pubblicare la tassonomia.

## Pubblicazione di una tassonomia {#publishing}

Una tassonomia non è disponibile per l’Editor universale o per i tuoi utenti fino a quando non viene pubblicata.

Le pagine della tassonomia vengono pubblicate come qualsiasi altra pagina da [utilizzando le icone **Publish rapido** o **Gestisci pubblicazione** nella barra degli strumenti.](/help/sites-cloud/authoring/sites-console/publishing-pages.md)

È necessario ripubblicare la pagina della tassonomia ogni volta che:

* Modificare la pagina della tassonomia.
* Modifica o aggiungi ai tag e agli spazi dei nomi inclusi nella pagina della tassonomia.

Se si crea una nuova pagina di tassonomia, è necessario prima [aggiungervi un mapping al file `paths.json` del progetto.](#paths-json)

## Accesso alle informazioni sulla tassonomia {#accessing}

Una volta pubblicata la tassonomia, le relative informazioni possono essere utilizzate dall’Editor universale e rese visibili agli utenti.

Puoi accedere alla tassonomia come dati JSON al seguente indirizzo.

`https://<branch>--<repository>--<owner>.hlx.page/<taxonomy-json-name>.json`

Utilizza `<taxonomy-json-name>` definito durante il [mapping della tassonomia al file `paths.json` nel progetto.](#paths-json) I dati della tassonomia vengono restituiti come dati JSON, come nell&#39;esempio seguente.

```json
{
  "total": 3,
  "offset": 0,
  "limit": 3,
  "data": [
    {
      "tag": "default:",
      "title": "Standard Tags"
    },
    {
      "tag": "do-not-translate",
      "title": "Do Not Translate"
    },
    {
      "tag": "translate",
      "title": "Translate"
    }
  ],
  ":type": "sheet"
}
```

Questi dati JSON verranno aggiornati automaticamente durante l’aggiornamento della tassonomia e la loro ripubblicazione. L’app può accedere a queste informazioni a livello di programmazione per i tuoi utenti.

[Se si gestiscono i tag in più lingue,](/help/sites-cloud/administering/tags.md#managing-tags-in-different-languages) è possibile accedere a tali lingue passando il codice della lingua ISO2 come valore di un parametro `sheet=`.
