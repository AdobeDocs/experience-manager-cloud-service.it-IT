---
title: Riferimento schema metadati
description: 'Scoprite le convenzioni standard per la descrizione dei metadati delle risorse, inclusi Dublin Core, IPTC e altri schemi di metadati. '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Riferimento schema metadati {#metadata-schemata-reference}

Il riferimento seguente contiene informazioni su uno specifico schema di metadati (in ordine alfabetico), un elenco delle proprietà e delle relative definizioni.

## Dublin Core {#dublin-core}

I metadati Dublin Core forniscono un set standardizzato di convenzioni per la descrizione delle risorse, al fine di facilitarne la ricerca. In Risorse AEM, Dublin Core descrive le risorse digitali come video, audio, immagini e documenti.

Il semplice set di metadati Dublin Core Metadata Element Set (DCMES) contiene 15 elementi di metadati, come elencato nella tabella seguente. Ciascun elemento Dublin Core è facoltativo e può essere ripetuto. Potete aggiungere o eliminare i metadati Dublin Core come fareste per i metadati specifici per i tipi di supporti.

Oltre al DCMES, esistono altri elementi di metadati creati dall&#39;iniziativa Dublin Core. Per ulteriori informazioni, consulta la [Dublin Core Initiative](https://dublincore.org/) .

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td> 
   <td><strong>Descrizione</strong></td> 
  </tr>
  <tr>
   <td>collaboratore</td> 
   <td>La persona o la società responsabile del contributo al contenuto.</td> 
  </tr>
  <tr>
   <td>cover</td> 
   <td>La posizione geografica o il periodo di tempo coperto dall'attività.<br /> </td> 
  </tr>
  <tr>
   <td>creatore</td> 
   <td>Persona o società responsabile della creazione del contenuto.</td> 
  </tr>
  <tr>
   <td>data</td> 
   <td>Data o periodo di tempo associato alla risorsa.<br /> </td> 
  </tr>
  <tr>
   <td>descrizione</td> 
   <td>Ulteriori informazioni sulla risorsa.</td> 
  </tr>
  <tr>
   <td>format</td> 
   <td>Formato file, supporto fisico o dimensioni della risorsa. AEM utilizza <code>dc:format</code> per indicare il tipo mime della risorsa.<br /> </td> 
  </tr>
  <tr>
   <td>identifier</td> 
   <td>Un riferimento univoco alla risorsa.</td> 
  </tr>
  <tr>
   <td>language</td> 
   <td>La lingua della risorsa (ad esempio, en per l’inglese).</td> 
  </tr>
  <tr>
   <td>publisher</td> 
   <td>La persona o la società responsabile della messa a disposizione della risorsa.</td> 
  </tr>
  <tr>
   <td>relation</td> 
   <td>Una risorsa correlata.</td> 
  </tr>
  <tr>
   <td>rights</td> 
   <td>Informazioni su chi dispone dei diritti per questa risorsa.</td> 
  </tr>
  <tr>
   <td>source</td> 
   <td>Un'attività correlata da cui è derivata l'attività.</td> 
  </tr>
  <tr>
   <td>subject</td> 
   <td>Argomento della risorsa.<br /> </td> 
  </tr>
  <tr>
   <td>titolo</td> 
   <td>Un nome per la risorsa.</td> 
  </tr>
  <tr>
   <td>tipo</td> 
   <td>La natura o il genere del bene.</td> 
  </tr>
 </tbody>
</table>

## IPTC {#iptc}

L&#39;International Press Telecommunications Council (IPTC) è un consorzio di agenzie di informazione di tutto il mondo, uno dei suoi obiettivi è quello di sviluppare e mantenere gli standard tecnici. L&#39;IPTC ha definito una serie di standard di metadati fotografici per le immagini che sono quasi universalmente accettati dai fotografi. Questi standard di metadati facevano parte dello standard più ampio noto come IPTC Information Interchange Model (IIM) creato negli anni &#39;90.

Sebbene le informazioni dell&#39;intestazione IPTC siano state in gran parte sostituite da XMP, per XMP sono disponibili uno schema di base IPTC e uno schema di estensione. Nei programmi per immagini, le proprietà XMP e IPTC sono sincronizzate.
