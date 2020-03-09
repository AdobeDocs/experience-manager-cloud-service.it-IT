---
title: Utilizzo dei tag
description: I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web
translation-type: ht
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Utilizzo dei tag   {#using-tags}

I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web. I tag possono essere paragonati a parole chiave o etichette assegnate a una pagina, una risorsa o ad altro contenuto per consentire la ricerca di contenuti specifici e correlati.

* Per informazioni sulla creazione e la gestione dei tag, nonché sulla modalità di applicazione dei tag di contenuto, consulta Gestione dei tag. <!-- See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.-->
* Per informazioni sul framework dei tag e sull’inclusione e l’estensione dei tag in applicazioni personalizzate, consulta Assegnazione tag per sviluppatori. <!-- See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.-->

## Dieci motivi per utilizzare l’assegnazione tag {#ten-reasons-to-use-tagging}

1. **Organizzazione dei contenuti**: l’assegnazione tag semplifica il lavoro degli autori, che possono organizzare rapidamente i contenuti con il minimo sforzo.
1. **Organizzazione dei tag**: i tag consentono di organizzare contenuti, mentre le tassonomie o i namespace gerarchici consentono di organizzare i tag.
1. **Tag estremamente organizzati**: grazie all’assegnazione di tag principali e secondari, è possibile creare tassonomie complete che includono termini, termini derivati e relazioni che li collegano. In questo modo è possibile creare una seconda (o terza) gerarchia di contenuti parallela a quella ufficiale.
1. **Assegnazione tag controllata**: per gestire l’assegnazione tag, è possibile applicare autorizzazioni ai tag e/o ai namespace e controllare la creazione e l’applicazione di tag.
1. **Assegnazione tag flessibile**: i tag possono avere nomi diversi, come tag, termini di tassonomia, categorie, etichette e molto altro ancora. Sono flessibili dal punto di vista del modello di contenuto e della modalità di utilizzo. Possono essere ad esempio utilizzati per sintetizzare le caratteristiche demografiche del target, suddividere in categorie e classificare i contenuti o creare una gerarchia di contenuti secondaria.
1. **Ricerca migliorata**: il componente di ricerca predefinito in AEM include i tag creati e assegnati a cui possono essere applicati filtri per restringere i risultati solo a quelli pertinenti.
1. **Abilitazione SEO**: i tag applicati come proprietà della pagina vengono visualizzati automaticamente nei metatag della pagina, rendendola visibile ai motori di ricerca.
1. **Funzionalità sofisticate e al contempo semplici**: per creare i tag, basta selezionare una parola e fare clic su un pulsante. In seguito, è possibile aggiungere un titolo, una descrizione ed etichette illimitate per fornire ulteriore semantica al tag.
1. **Coerenza di base**: il sistema di assegnazione tag è un componente di base di AEM ed è utilizzato in tutte le funzioni AEM per la classificazione dei contenuti. Inoltre, per gli sviluppatori è disponibile l’API di assegnazione tag che consente di creare applicazioni abilitate per l’assegnazione tag con accesso alle stesse tassonomie.
1. **Struttura e flessibilità**: AEM è ideale per lavorare con informazioni strutturate, grazie alla nidificazione di pagine e percorsi. È molto efficace anche per la gestione delle informazioni non strutturate, grazie alla funzione integrata di ricerca testuale. L’assegnazione di tag offre i vantaggi delle struttura e della flessibilità.

Quando progetti la struttura dei contenuti di un sito e lo schema di metadati per le risorse, considera l’approccio leggero e accessibile fornito dai tag.

## Applicazione dei tag   {#applying-tags}

Nell’ambiente di authoring gli autori possono applicare i tag accedendo alle proprietà della pagina e immettendo uno o più tag nel campo **Tag/Parole chiave**.

Per applicare tag predefiniti, nella finestra **Proprietà pagina** utilizza il campo **Tag** e la finestra **Seleziona tag**. La scheda **Tag standard** è il namespace predefinito, il che significa che non esiste una `namespace-string:` aggiunta come prefisso alla tassonomia. <!-- To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window.-->

![Selezione di più tag](/help/sites-cloud/authoring/assets/tags-select.png)

## Pubblicazione dei tag {#publishing-tags}

Analogamente a quanto avviene per la pubblicazione e l’annullamento della pubblicazione delle pagine, è possibile effettuare le seguenti operazioni su tag e namespace:

### Attiva {#activate}

* Consente di attivare singoli tag.

   Come per le pagine, è necessario attivare i nuovi tag creati prima che siano disponibili nell’ambiente di pubblicazione.

>[!NOTE]
>
>Quando si attiva una pagina, si apre automaticamente una finestra di dialogo che consente di attivare i tag non attivati appartenenti alla pagina.

### Disattiva {#deactivate}

* Consente di disattivare i tag selezionati.
