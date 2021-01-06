---
title: Componenti di configurazione dei frammenti di contenuto per il rendering
description: Componenti di configurazione dei frammenti di contenuto per il rendering
translation-type: tm+mt
source-git-commit: a5d6a072dfd8df887309f56ad4a61b6b38b32fa7
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 6%

---


# Componenti di configurazione dei frammenti di contenuto per il rendering{#content-fragments-configuring-components-for-rendering}

Esistono diversi [servizi avanzati](#definition-of-advanced-services-that-need-configuration) correlati al rendering dei frammenti di contenuto. Per utilizzare questi servizi, i tipi di risorse di tali componenti devono essere resi noti al framework dei frammenti di contenuto.

Questa operazione viene eseguita configurando il [servizio OSGi - configurazione componente frammento di contenuto](#osgi-service-content-fragment-component-configuration).

Queste informazioni sono necessarie quando:

* È necessario implementare un proprio componente basato su frammenti di contenuto,
* E devono utilizzare i servizi avanzati.

Si consiglia di utilizzare i componenti core.

>[!CAUTION]
>
>* **Se non avete bisogno dei  [servizi](#definition-of-advanced-services-that-need-configuration)** avanzati descritti di seguito, potete ignorare questa configurazione.
>
>* **Quando si estendono o si utilizzano i componenti forniti**, non è consigliabile modificare la configurazione OSGi.
>
>* **È possibile scrivere un componente da zero che utilizza solo l&#39;API dei frammenti di contenuto, senza servizi** avanzati. Tuttavia, in tal caso, sarà necessario sviluppare il componente in modo che gestisca l’elaborazione appropriata.
>
>Si consiglia pertanto di utilizzare i componenti core.

## Definizione di servizi avanzati che richiedono la configurazione {#definition-of-advanced-services-that-need-configuration}

I servizi che richiedono la registrazione di un componente sono:

* Determinazione corretta delle dipendenze durante la pubblicazione (ad esempio, verificare che frammenti e modelli possano essere pubblicati automaticamente con una pagina se sono stati modificati dall’ultima pubblicazione).
* Supporto per i frammenti di contenuto nella ricerca full-text.
* Gestione/gestione di *contenuti intermedi.*
* Gestione/gestione di *risorse multimediali diverse.*
* Dispatcher flush per i frammenti di riferimento (se una pagina contenente un frammento viene pubblicata nuovamente).
* Utilizzo del rendering basato su paragrafo.

Se hai bisogno di una o più di queste funzionalità, in genere è più semplice utilizzare i servizi avanzati out-of-the-box, invece di svilupparli da zero.

## Servizio OSGi - Configurazione componente frammento di contenuto {#osgi-service-content-fragment-component-configuration}

La configurazione deve essere associata al servizio OSGi **Configurazione componente frammento di contenuto**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Configurazione OSGi](/help/implementing/deploying/overview.md#osgi-configuration).

Esempio:

![Configurazione del componente frammento di contenuto di configurazione OSGi](assets/cf-component-configuration-osgi.png)

La configurazione OSGi è:

<table>
 <thead>
  <tr>
   <td>Etichetta</td>
   <td>Configurazione OSGi<br /> </td>
   <td>Descrizione</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>Tipo risorsa</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>Il tipo di risorsa da registrare; ad esempio <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Proprietà Reference</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>Nome della proprietà contenente il riferimento al frammento; ad esempio <code>fragmentPath</code> oppure <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Proprietà Element(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>Il nome della proprietà che contiene i nomi degli elementi di cui eseguire il rendering; ad esempio<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Proprietà variante</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>Il nome della proprietà che contiene il nome della variante da rappresentare; ad esempio<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Per alcune funzionalità, il componente dovrà rispettare convenzioni predefinite. Nella tabella seguente sono illustrate le proprietà che devono essere definite dal componente per ciascun paragrafo (es. `jcr:paragraph` per ogni istanza di componente) in modo che i servizi possano rilevarli ed elaborarli correttamente.

<table>
 <thead>
  <tr>
   <td>Nome proprietà</td>
   <td>Descrizione</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Una proprietà stringa che definisce la modalità di output dei paragrafi in <em>modalità di rendering a elemento singolo</em>.</p> <p>Valori:</p>
    <ul>
     <li><code>all</code> : per eseguire il rendering di tutti i paragrafi</li>
     <li><code>range</code> : per eseguire il rendering dell'intervallo di paragrafi fornito da <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Una proprietà stringa che definisce l'intervallo di paragrafi da restituire se in <em>modalità di rendering elemento singolo</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> oppure <code>1-3</code> o <code>1-3;6;7-8</code> oppure <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> indicatore di gamma</li>
       <li><code>;</code> separatore elenco</li>
       <li><code>*</code> carattere jolly</li>
     </ul>
     </li>
     <li>valutato solo se <code>paragraphScope</code> è impostato su <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Una proprietà booleana che definisce se le intestazioni (ad esempio, <code>h1</code>, <code>h2</code>, <code>h3</code>) sono conteggiate come paragrafi (<code>true</code>) o meno (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## Esempio {#example}

Ad esempio, vedete quanto segue (in un&#39;istanza AEM out-of-the-box):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Contiene:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

