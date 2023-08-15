---
title: Panoramica dei frammenti esperienza
description: Estendi i frammenti esperienza Adobe Experience Manager as a Cloud Service.
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 1%

---

# Frammenti di esperienza{#experience-fragments}

## Nozioni di base {#the-basics}

Un [Frammento esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) è un gruppo di uno o più componenti, inclusi il contenuto e il layout, a cui è possibile fare riferimento all’interno delle pagine.

Un Master Frammento esperienza, o una Variante, o entrambi, utilizza:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Perché non c&#39;è `/libs/cq/experience-fragments/components/xfpage/xfpage.html`, viene ripristinato

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Rendering HTML semplice {#the-plain-html-rendition}

Utilizzo di `.plain.` nell’URL, puoi accedere alla rappresentazione HTML semplice.

Questa rappresentazione è disponibile dal browser. Tuttavia, il suo scopo principale è quello di consentire ad altre applicazioni (ad esempio, applicazioni web di terze parti e implementazioni personalizzate per dispositivi mobili) di accedere ai contenuti del frammento di esperienza direttamente dall’URL.

La rappresentazione HTML semplice aggiunge il protocollo, l’host e il percorso di contesto ai percorsi seguenti:

* del tipo: `src`, `href`, o `action`

* oppure termina con: `-src`, o `-href`

Ad esempio:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>I collegamenti fanno sempre riferimento all’istanza Publish. Poiché sono destinati a essere utilizzati da terze parti, il collegamento viene sempre richiamato dall’istanza Publish e non dall’istanza Autore.

![Rendering di HTML semplice](assets/xf-14.png)

Il selettore della rappresentazione semplice utilizza un trasformatore invece di script aggiuntivi. Il [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) viene utilizzato come trasformatore. Questo trasformatore è configurato come segue:

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### Configurazione della generazione della rappresentazione HTML {#configuring-html-rendition-generation}

Il rendering HTML viene generato utilizzando le pipeline del rewriter di Sling. La pipeline è definita in `/libs/experience-fragments/config/rewriter/experiencefragments`. Il trasformatore HTML supporta le seguenti opzioni:

* `allowedCssClasses`
   * Un’espressione RegEx che corrisponde alle classi CSS che devono essere lasciate nella rappresentazione finale.
   * Questa opzione è utile se il cliente desidera eliminare alcune classi CSS specifiche
* `allowedTags`
   * Elenco di tag HTML consentiti nella rappresentazione finale.
   * Per impostazione predefinita sono consentiti i seguenti tag (non è necessaria alcuna configurazione): html, head, title, body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h4, h5, h6, br, noscript, div, link e script

L’Adobe consiglia di configurare il rewriter utilizzando una sovrapposizione. Consulta [Sovrapposizioni in AEM as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Modelli per frammenti esperienza {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Solo*** I modelli modificabili sono supportati per i Frammenti di esperienza.

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

Durante lo sviluppo di un nuovo modello per Frammenti esperienza, puoi seguire le procedure standard per un modello modificabile.

<!-- When developing a new template for Experience Fragments you can follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

Per creare un modello di Frammento esperienza rilevato da **Crea frammento esperienza** procedura guidata, è necessario seguire uno dei seguenti set di regole:

1. Entrambi:

   1. Il tipo di risorsa del modello (nodo iniziale) deve ereditare da:
      `cq/experience-fragments/components/xfpage`

   1. Il nome del modello deve iniziare con:
      `experience-fragments`
Questo modello consente agli utenti di creare frammenti di esperienza in /content/experience-fragments come `cq:allowedTemplates` Questa proprietà della cartella include tutti i modelli i cui nomi iniziano con `experience-fragment`. I clienti possono aggiornare questa proprietà per includere il proprio schema di denominazione o le posizioni dei modelli.

1. [Modelli consentiti](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) può essere configurato nella console Frammenti di esperienza.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componenti per frammenti esperienza {#components-for-experience-fragments}

Lo sviluppo di componenti da utilizzare con/in Frammenti esperienza segue le procedure standard.

L’unica configurazione aggiuntiva consiste nel garantire che i componenti siano consentiti nel modello. Questa tolleranza viene ottenuta con l’informativa sui contenuti.

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## Experience Fragment Link Rewriter Provider - HTML {#the-experience-fragment-link-rewriter-provider-html}

In AEM puoi creare frammenti esperienza. Un frammento esperienza:

* è costituito da un gruppo di componenti con un layout,
* può esistere indipendentemente da una pagina AEM.

Uno dei casi d’uso per tali gruppi è l’incorporamento di contenuto in punti di contatto di terze parti, ad esempio Adobe Target.

### Riscrittura collegamento predefinita {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

Utilizzando la funzione Esporta in Target puoi effettuare le seguenti operazioni:

* creare un frammento esperienza,
* aggiungervi componenti,
* e quindi esportarla come offerta Adobe Target, in formato HTML o JSON.

Questa funzione può essere abilitata su un’istanza Autore di AEM. Richiede una configurazione Adobe Target valida e configurazioni per Link Externalizer.

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

Link Externalizer viene utilizzato per determinare gli URL corretti necessari durante la creazione della versione HTML dell’offerta Target, che viene quindi inviata ad Adobe Target. Questo processo è necessario in quanto Adobe Target richiede che tutti i collegamenti all’interno dell’offerta Target HTML siano accessibili al pubblico. Ciò significa che tutte le risorse a cui fanno riferimento i collegamenti e il frammento di esperienza stesso devono essere pubblicati prima di poter essere utilizzati.

Per impostazione predefinita, quando crei un’offerta Target HTML, viene inviata una richiesta a un selettore Sling personalizzato nell’AEM. Questo selettore si chiama `.nocloudconfigs.html`. Come suggerisce il nome, viene creato un rendering HTML semplice di un frammento di esperienza, ma non sono incluse le configurazioni cloud (che sarebbero informazioni superflue).

Dopo aver generato la pagina HTML, la pipeline del rewriter di Sling viene modificata nell’output:

1. Il `html`, `head`, e `body` gli elementi vengono sostituiti con `div` elementi. Il `meta`, `noscript`, e `title` elementi vengono rimossi (sono elementi figlio dell&#39;originale) `head` e non vengono considerati quando vengono sostituiti dall&#39; `div` elemento ).

   Questa procedura garantisce che l’offerta HTML Target possa essere inclusa nelle attività di Target.

2. L’AEM modifica eventuali collegamenti interni presenti nel HTML in modo che puntino a una risorsa pubblicata.

   Per determinare i collegamenti da modificare, AEM segue questo modello per gli attributi degli elementi HTML:

   1. `src` attributi
   2. `href` attributi
   3. `*-src` attributi (come `data-src`, e `custom-src`)
   4. `*-href` attributi (come `data-href`, `custom-href`, e `img-href`)

   >[!NOTE]
   >
   >I collegamenti interni in HTML sono collegamenti relativi, ma in alcuni casi i componenti personalizzati forniscono URL completi in HTML. Per impostazione predefinita, l’AEM ignora questi URL completi e non apporta modifiche.

   I collegamenti in questi attributi vengono eseguiti tramite AEM Link Externalizer `publishLink()` per ricreare l’URL come se si trovasse in un’istanza pubblicata e come tale, disponibile al pubblico.

Quando si utilizza un’implementazione standard, il processo descritto sopra deve essere sufficiente per generare l’offerta Target dal frammento di esperienza e quindi esportarla in Adobe Target. Tuttavia, ci sono alcuni casi d’uso che non vengono presi in considerazione in questo processo. Alcuni di questi casi che non sono considerati includono i seguenti:

* Mappatura Sling disponibile solo nell’istanza Publish
* Reindirizzamenti di Dispatcher

Per questi casi d’uso, AEM fornisce l’interfaccia Link Rewriter Provider.

### Collega interfaccia provider rewriter {#link-rewriter-provider-interface}

Per i casi più complicati, non coperti dal [predefinito](#default-link-rewriting), AEM offre l’interfaccia Link Rewriter Provider. Questa interfaccia è un `ConsumerType` che puoi implementare nei bundle come servizio. Ignora le modifiche che AEM esegue sui collegamenti interni di un’offerta HTML riprodotta da un frammento di esperienza. Questa interfaccia consente di personalizzare la procedura di riscrittura dei collegamenti interni di HTML in base alle esigenze aziendali.

Esempi di casi d’uso per l’implementazione di questa interfaccia come servizio includono:

* Le mappature Sling sono abilitate nelle istanze di pubblicazione, ma non nell’istanza di authoring
* Dispatcher o tecnologia simile viene utilizzata per reindirizzare gli URL internamente
* Il `sling:alias mechanisms` sono disponibili per le risorse

>[!NOTE]
>
>Questa interfaccia elabora solo i collegamenti HTML interni dall’offerta Target generata.

Interfaccia del provider del rewriter di collegamento ( `ExperienceFragmentLinkRewriterProvider`) è il seguente:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Come utilizzare l&#39;interfaccia del provider del rewriter di collegamento {#how-to-use-the-link-rewriter-provider-interface}

Per utilizzare l’interfaccia, devi innanzitutto creare un bundle contenente un nuovo componente del servizio che implementa l’interfaccia Link Rewriter Provider.

Questo servizio viene utilizzato per collegarsi alla riscrittura del file Esportazione frammento di esperienza in Target in modo da poter accedere ai vari collegamenti.

Ad esempio, `ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

Affinché il servizio funzioni, è ora necessario implementare tre metodi all’interno del servizio:

* `[shouldRewrite](#shouldrewrite)`
* `[rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* `[getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Indica al sistema se deve riscrivere i collegamenti quando viene effettuata una chiamata per l’esportazione in Target per una determinata variante del frammento di esperienza. Puoi implementare il seguente metodo:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Ad esempio:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Questo metodo riceve come parametro la variante del frammento di esperienza riscritta dal sistema di esportazione in Target.

Nell’esempio precedente, desideri riscrivere:

* collegamenti presenti in `src`

* `href` solo attributi

* per un frammento di esperienza specifico:
  `/content/experience-fragment/master`

Qualsiasi altro frammento di esperienza che passa attraverso il sistema di esportazione in Target viene ignorato e non è interessato dalle modifiche implementate in questo Servizio.

#### rewriteLink {#rewritelink}

Per la variante del frammento di esperienza interessata dal processo di riscrittura, procede quindi lasciando che il servizio gestisca la riscrittura del collegamento. Ogni volta che si verifica un collegamento in Internal HTML, viene richiamato il seguente metodo:

`rewriteLink(String link, String tag, String attribute)`

Come input, il metodo riceve i parametri:

* `link`
Il `String` rappresentazione del collegamento in fase di elaborazione. Questa rappresentazione è in genere un URL relativo che punta alla risorsa nell’istanza di authoring.

* `tag`
Nome dell&#39;elemento HTML in fase di elaborazione.

* `attribute`
Il nome esatto dell’attributo.

Ad esempio, se il sistema Export to Target elabora questo elemento, puoi definire `CSSInclude` come:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

La chiamata al `rewriteLink()` viene eseguito utilizzando i seguenti parametri:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Quando crei il servizio, le decisioni si basano sull’input fornito e quindi riscrivi il collegamento di conseguenza.

Ad esempio, si desidera rimuovere il `/etc.clientlibs` parte dell’URL e aggiungi il dominio esterno appropriato. Per semplificare le operazioni, è consigliabile avere accesso a un Resource Resolver per il servizio, ad esempio `rewriteLinkExample2`:

>[!NOTE]
>
>Per ulteriori informazioni su come ottenere un risolutore risorse tramite un utente del servizio, consulta Utenti del servizio in AEM.

<!--
>For more information on how to get a resource resolver through a service user see [Service Users in AEM](/help/sites-administering/security-service-users.md).
-->

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>Se il metodo precedente restituisce `null`, quindi il sistema di esportazione in Target lascia il collegamento così com’è, un collegamento relativo a una risorsa.

#### Priorità - getPriority {#priorities-getpriority}

Non è raro che siano necessari diversi servizi per soddisfare diversi tipi di frammenti esperienza o persino un servizio generico che gestisca l’esternalizzazione e la mappatura di tutti i frammenti esperienza. In questi casi, potrebbero sorgere conflitti sul servizio da utilizzare, per cui l&#39;AEM fornisce la possibilità di definire **Priorità** per diversi servizi. Le priorità sono specificate utilizzando il metodo:

* `getPriority()`

Questo metodo consente l&#39;utilizzo di diversi servizi in cui `shouldRewrite()` Il metodo restituisce true per lo stesso frammento di esperienza. Il servizio che restituisce il numero più alto dal relativo `getPriority()`Il metodo è il servizio che gestisce la variante del frammento di esperienza.

Ad esempio, puoi avere `GenericLinkRewriterProvider` che gestisce la mappatura di base per tutti i frammenti esperienza e quando `shouldRewrite()` restituisce il metodo `true` per tutte le varianti di frammenti esperienza. Per diversi frammenti di esperienza specifici, potrebbe essere utile una gestione particolare; in questo caso, puoi fornire `SpecificLinkRewriterProvider` per i quali `shouldRewrite()` Il metodo restituisce true solo per alcune varianti di frammenti esperienza. Per assicurarsi che `SpecificLinkRewriterProvider` è stato scelto per gestire tali varianti di frammento esperienza, deve restituire nel suo `getPriority()` metodo un numero maggiore di `GenericLinkRewriterProvider.`
