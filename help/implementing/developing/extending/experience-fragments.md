---
title: Panoramica dei frammenti esperienza
description: Estendere i frammenti di esperienza per Adobe Experience Manager as a Cloud Service
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
feature: Developing, Experience Fragments
role: Admin, Architect, Developer
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 0%

---

# Frammenti di esperienza{#experience-fragments}

## Nozioni di base {#the-basics}

Un [frammento esperienza](/help/sites-cloud/authoring/fragments/content-fragments.md) è un gruppo di uno o più componenti, inclusi il contenuto e il layout, a cui è possibile fare riferimento all&#39;interno delle pagine.

Un Master Frammento esperienza, o una Variante, o entrambi, utilizza:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Poiché non è presente `/libs/cq/experience-fragments/components/xfpage/xfpage.html`, viene ripristinato

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Rendering HTML semplice {#the-plain-html-rendition}

Utilizzando il selettore `.plain.` nell&#39;URL, puoi accedere al rendering HTML normale.

Questa rappresentazione è disponibile dal browser. Tuttavia, il suo scopo principale è quello di consentire ad altre applicazioni (ad esempio, applicazioni web di terze parti e implementazioni personalizzate per dispositivi mobili) di accedere ai contenuti del frammento di esperienza direttamente dall’URL.

Il rendering HTML semplice aggiunge il protocollo, l’host e il percorso di contesto ai percorsi che sono:

* di tipo: `src`, `href` o `action`

* oppure terminare con: `-src` o `-href`

Ad esempio:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>I collegamenti fanno sempre riferimento all’istanza Publish. Poiché sono destinati a essere utilizzati da terze parti, il collegamento viene sempre richiamato dall’istanza Publish e non dall’istanza Autore.
>
>Per ulteriori informazioni, vedere [Esternalizzazione degli URL](/help/implementing/developing/tools/externalizer.md).

![Rendering HTML normale](assets/xf-14.png)

Il selettore della rappresentazione semplice utilizza un trasformatore invece di script aggiuntivi. Il [rewriter Sling](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) è utilizzato come trasformatore. Questo trasformatore è configurato come segue:

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### Configurazione della generazione della rappresentazione HTML {#configuring-html-rendition-generation}

Il rendering di HTML viene generato utilizzando le pipeline del rewriter di Sling. La pipeline è definita in `/libs/experience-fragments/config/rewriter/experiencefragments`. HTML Transformer supporta le seguenti opzioni:

* `allowedCssClasses`
   * Un’espressione RegEx che corrisponde alle classi CSS che devono essere lasciate nella rappresentazione finale.
   * Questa opzione è utile se il cliente desidera eliminare alcune classi CSS specifiche
* `allowedTags`
   * Elenco di tag HTML consentiti nella rappresentazione finale.
   * Per impostazione predefinita sono consentiti i seguenti tag (non è necessaria alcuna configurazione): html, head, title, body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h4, h5, h6, br, noscript, div, link e script

Adobe consiglia di configurare il rewriter utilizzando una sovrapposizione. Vedi [Sovrapposizioni in AEM as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Modelli per frammenti esperienza {#templates-for-experience-fragments}

>[!CAUTION]
>
>Per i frammenti di esperienza sono supportati ***solo*** modelli modificabili.
>
>I frammenti di esperienza possono essere utilizzati solo su pagine basate su modelli modificabili.

<!-- 
***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

Durante lo sviluppo di un nuovo modello per Frammenti esperienza, puoi seguire le procedure standard per un modello modificabile.

<!-- 
When developing a new template for Experience Fragments you can follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

Per creare un modello di frammento esperienza rilevato dalla procedura guidata **Crea frammento esperienza**, è necessario seguire uno dei seguenti set di regole:

1. Entrambi:

   1. Il tipo di risorsa del modello (nodo iniziale) deve ereditare da:
      `cq/experience-fragments/components/xfpage`

   1. Il nome del modello deve iniziare con:
      `experience-fragments`
Questo modello consente agli utenti di creare frammenti di esperienza in /content/experience-fragments, in quanto la proprietà `cq:allowedTemplates` di questa cartella include tutti i modelli i cui nomi iniziano con `experience-fragment`. I clienti possono aggiornare questa proprietà per includere il proprio schema di denominazione o le posizioni dei modelli.

1. È possibile configurare [Modelli consentiti](/help/sites-cloud/authoring/fragments/content-fragments.md#configure-allowed-templates-folder) nella console Frammenti esperienza.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- 
>[!NOTE]
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

## Provider del rewriter di collegamento a frammenti esperienza - HTML {#the-experience-fragment-link-rewriter-provider-html}

In AEM puoi creare frammenti esperienza. Un frammento di esperienza:

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

Link Externalizer viene utilizzato per determinare gli URL corretti necessari durante la creazione della versione HTML dell’offerta Target, che viene quindi inviata ad Adobe Target. Questo processo è necessario in quanto Adobe Target richiede che tutti i collegamenti all’interno dell’offerta HTML di Target siano accessibili al pubblico. Ciò significa che tutte le risorse a cui fanno riferimento i collegamenti e il frammento di esperienza stesso devono essere pubblicati prima di poter essere utilizzati.

Per impostazione predefinita, quando crei un’offerta HTML di Target, viene inviata una richiesta a un selettore Sling personalizzato in AEM. Questo selettore si chiama `.nocloudconfigs.html`. Come suggerisce il nome, viene creato un rendering HTML semplice di un frammento di esperienza, ma non sono incluse le configurazioni cloud (che sarebbero informazioni superflue).

Dopo aver generato la pagina HTML, la pipeline del rewriter di Sling viene modificata nell’output:

1. Gli elementi `html`, `head` e `body` sono sostituiti con `div` elementi. Gli elementi `meta`, `noscript` e `title` vengono rimossi (sono elementi figlio dell&#39;elemento `head` originale e non vengono considerati quando vengono sostituiti dall&#39;elemento `div`).

   Questa procedura garantisce che l’offerta HTML Target possa essere inclusa nelle attività di Target.

2. AEM modifica tutti i collegamenti interni presenti in HTML in modo che puntino a una risorsa pubblicata.

   Per determinare i collegamenti da modificare, AEM segue questo modello per gli attributi degli elementi HTML:

   1. Attributi `src`
   2. Attributi `href`
   3. Attributi `*-src` (ad esempio `data-src` e `custom-src`)
   4. Attributi `*-href` (come `data-href`, `custom-href` e `img-href`)

   >[!NOTE]
   >
   >I collegamenti interni in HTML sono collegamenti relativi, ma in alcuni casi i componenti personalizzati forniscono URL completi in HTML. Per impostazione predefinita, AEM ignora questi URL completi e non apporta modifiche.

   I collegamenti in questi attributi vengono eseguiti tramite AEM Link Externalizer `publishLink()` per ricreare l&#39;URL come se si trovasse in un&#39;istanza pubblicata e quindi disponibile pubblicamente.

Quando si utilizza un’implementazione standard, il processo descritto sopra deve essere sufficiente per generare l’offerta Target dal frammento di esperienza e quindi esportarla in Adobe Target. Tuttavia, ci sono alcuni casi d’uso che non vengono presi in considerazione in questo processo. Alcuni di questi casi che non sono considerati includono i seguenti:

* Mappatura Sling disponibile solo nell’istanza Publish
* Reindirizzamenti Dispatcher

Per questi casi d’uso, AEM fornisce l’interfaccia Link Rewriter Provider.

### Collega interfaccia provider rewriter {#link-rewriter-provider-interface}

Per casi più complessi, non coperti dal [default](#default-link-rewriting), AEM offre l&#39;interfaccia Link Rewriter Provider. Questa è un&#39;interfaccia `ConsumerType` che puoi implementare nei bundle come servizio. Ignora le modifiche eseguite da AEM sui collegamenti interni di un’offerta HTML riprodotta da un frammento di esperienza. Questa interfaccia consente di personalizzare il processo di riscrittura dei collegamenti interni di HTML per allinearli alle esigenze aziendali.

Esempi di casi d’uso per l’implementazione di questa interfaccia come servizio includono:

* Le mappature Sling sono abilitate nelle istanze di pubblicazione, ma non nell’istanza di authoring
* Per reindirizzare gli URL internamente viene utilizzato un Dispatcher o una tecnologia simile
* `sling:alias mechanisms` sono presenti per le risorse

>[!NOTE]
>
>Questa interfaccia elabora solo i collegamenti HTML interni dall’offerta Target generata.

Interfaccia provider rewriter collegamento ( `ExperienceFragmentLinkRewriterProvider`):

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

* Solo attributi `href`

* per un frammento di esperienza specifico:
  `/content/experience-fragment/master`

Qualsiasi altro frammento di esperienza che passa attraverso il sistema di esportazione in Target viene ignorato e non è interessato dalle modifiche implementate in questo Servizio.

#### rewriteLink {#rewritelink}

Per la variante del frammento di esperienza interessata dal processo di riscrittura, procede quindi lasciando che il servizio gestisca la riscrittura del collegamento. Ogni volta che si verifica un collegamento nel HTML interno, viene richiamato il seguente metodo:

`rewriteLink(String link, String tag, String attribute)`

Come input, il metodo riceve i parametri:

* `link`
La rappresentazione `String` del collegamento in fase di elaborazione. Questa rappresentazione è in genere un URL relativo che punta alla risorsa nell’istanza di authoring.

* `tag`
Nome dell&#39;elemento HTML in fase di elaborazione.

* `attribute`
Il nome esatto dell’attributo.

Ad esempio, se il sistema di esportazione in Target sta elaborando questo elemento, è possibile definire `CSSInclude` come:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

La chiamata al metodo `rewriteLink()` viene eseguita utilizzando i seguenti parametri:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Quando crei il servizio, le decisioni si basano sull’input fornito e quindi riscrivi il collegamento di conseguenza.

Ad esempio, si desidera rimuovere la parte `/etc.clientlibs` dell&#39;URL e aggiungere il dominio esterno appropriato. Per semplificare le operazioni, si supponga di avere accesso a un Resource Resolver per il servizio, ad esempio `rewriteLinkExample2`:

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
>Se il metodo precedente restituisce `null`, il sistema Esporta in Target lascia il collegamento così com&#39;è, un collegamento relativo a una risorsa.

#### Priorità - getPriority {#priorities-getpriority}

Non è raro che siano necessari diversi servizi per soddisfare diversi tipi di frammenti esperienza o persino un servizio generico che gestisca l’esternalizzazione e la mappatura di tutti i frammenti esperienza. In questi casi potrebbero verificarsi conflitti sul servizio da utilizzare, pertanto AEM offre la possibilità di definire **Priorità** per servizi diversi. Le priorità sono specificate utilizzando il metodo:

* `getPriority()`

Questo metodo consente di utilizzare diversi servizi in cui il metodo `shouldRewrite()` restituisce true per lo stesso frammento di esperienza. Il servizio che restituisce il numero più alto dal relativo metodo `getPriority()` è il servizio che gestisce la variante del frammento di esperienza.

Ad esempio, puoi avere un `GenericLinkRewriterProvider` che gestisce la mappatura di base per tutti i frammenti di esperienza e quando il metodo `shouldRewrite()` restituisce `true` per tutte le varianti di frammenti di esperienza. Per diversi frammenti di esperienza specifici, potrebbe essere utile una gestione speciale. In questo caso, puoi fornire `SpecificLinkRewriterProvider` per il quale il metodo `shouldRewrite()` restituisce true solo per alcune varianti di frammenti di esperienza. Per assicurarsi che `SpecificLinkRewriterProvider` sia scelto per gestire tali varianti di frammenti esperienza, deve restituire nel suo metodo `getPriority()` un numero maggiore di `GenericLinkRewriterProvider.`
