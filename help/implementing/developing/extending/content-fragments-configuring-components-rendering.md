---
title: Componenti di configurazione dei frammenti di contenuto per il rendering
description: Componenti di configurazione dei frammenti di contenuto per il rendering
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 6%

---

# Componenti di configurazione dei frammenti di contenuto per il rendering{#content-fragments-configuring-components-for-rendering}

Ce ne sono diversi [servizi avanzati](#definition-of-advanced-services-that-need-configuration) relativo al rendering di frammenti di contenuto. Per utilizzare questi servizi, i tipi di risorse di tali componenti devono diventare noti al framework dei frammenti di contenuto.

Questa operazione viene eseguita configurando il [Servizio OSGi - Configurazione del componente Frammento di contenuto](#osgi-service-content-fragment-component-configuration).

Queste informazioni sono necessarie quando:

* È necessario implementare un proprio componente basato su frammenti di contenuto,
* E devono utilizzare i servizi avanzati.

Si consiglia di utilizzare i componenti core.

>[!CAUTION]
>
>* **Se non hai bisogno del [servizi avanzati](#definition-of-advanced-services-that-need-configuration)** come descritto di seguito, puoi ignorare questa configurazione.
>
>* **Quando estendi o utilizzi i componenti predefiniti**, si sconsiglia di modificare la configurazione OSGi.
>
>* **È possibile scrivere un componente da zero che utilizza solo l’API Frammenti di contenuto, senza servizi avanzati**. Tuttavia, in questo caso, sarà necessario sviluppare il componente in modo che gestisca l’elaborazione appropriata.
>
>Pertanto, si consiglia di utilizzare i componenti core .

## Definizione di servizi avanzati che richiedono la configurazione {#definition-of-advanced-services-that-need-configuration}

I servizi che richiedono la registrazione di un componente sono:

* Determinare correttamente le dipendenze durante la pubblicazione (ad esempio, verificare che frammenti e modelli possano essere pubblicati automaticamente con una pagina se sono cambiati dopo l’ultima pubblicazione).
* Supporto dei frammenti di contenuto nella ricerca full-text.
* Gestione/gestione delle *contenuto intermedio.*
* Gestione/gestione delle *risorse multimediali diverse.*
* Svuotamento del dispatcher per i frammenti a cui si fa riferimento (se una pagina contenente un frammento viene pubblicata nuovamente).
* Utilizzo del rendering basato su paragrafi.

Se hai bisogno di una o più di queste funzioni, in genere è più semplice utilizzare i servizi avanzati preconfigurati, anziché svilupparli da zero.

## Servizio OSGi - Configurazione del componente Frammento di contenuto {#osgi-service-content-fragment-component-configuration}

La configurazione deve essere associata al servizio OSGi **Configurazione del componente Frammento di contenuto**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Vedi [Configurazione OSGi](/help/implementing/deploying/overview.md#osgi-configuration) per ulteriori dettagli.

Ad esempio:

![Configurazione del componente Frammento di contenuto di configurazione OSGi](assets/cf-component-configuration-osgi.png)

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
   <td><strong>Proprietà di riferimento</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>Nome della proprietà contenente il riferimento al frammento; ad esempio <code>fragmentPath</code> o <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Proprietà elemento/i</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>Nome della proprietà che contiene i nomi degli elementi da riprodurre; ad esempio<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Proprietà variante</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>Il nome della proprietà che contiene il nome della variante di cui eseguire il rendering; ad esempio<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Per alcune funzionalità, il componente dovrà rispettare le convenzioni predefinite. La tabella seguente descrive le proprietà che devono essere definite dal componente per ogni paragrafo (ovvero `jcr:paragraph` per ogni istanza di componente) in modo che i servizi possano rilevarli ed elaborarli correttamente.

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
   <td><p>Proprietà stringa che definisce la modalità di output dei paragrafi in <em>modalità di rendering di un singolo elemento</em>.</p> <p>Valori:</p>
    <ul>
     <li><code>all</code> : rendering di tutti i paragrafi</li>
     <li><code>range</code> : per rendere l'intervallo di paragrafi fornito da <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Proprietà stringa che definisce l'intervallo di paragrafi da visualizzare se in <em>modalità di rendering di un singolo elemento</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> o <code>1-3</code> o <code>1-3;6;7-8</code> o <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> indicatore di gamma</li>
       <li><code>;</code> separatore di elenco</li>
       <li><code>*</code> carattere jolly</li>
     </ul>
     </li>
     <li>solo se <code>paragraphScope</code> è impostato su <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Una proprietà booleana che definisce se le intestazioni (ad esempio, <code>h1</code>, <code>h2</code>, <code>h3</code>) sono conteggiati come paragrafi (<code>true</code>) o no (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## Esempio {#example}

Ad esempio, consulta quanto segue (in un’istanza di AEM preconfigurata):

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
