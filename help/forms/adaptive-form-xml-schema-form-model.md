---
title: Come si progetta lo schema XML per un modulo adattivo?
description: Scopri come creare uno schema XML per un modulo adattivo e un modulo adattivo basato sullo schema per produrre i dati dei reclami relativi allo schema.
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 5b8ad9a8-77d4-4234-a4d7-c8964b975e96
hide: true
hidefromtoc: true
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 6%

---

# Progettare uno schema XML per un modulo adattivo {#creating-adaptive-forms-using-xml-schema}

## Prerequisiti {#prerequisites}

Per creare un modulo adattivo utilizzando uno schema XML come modello di modulo è necessario conoscere a fondo gli schemi XML. Inoltre, si consiglia di leggere il seguente contenuto prima di questo articolo.

* [Creazione di un modulo adattivo](creating-adaptive-form.md)
* [Schema XML](https://www.w3.org/TR/xmlschema-2/)

## Utilizzo di uno schema XML come modello di modulo {#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] supporta la creazione di un modulo adattivo utilizzando uno schema XML esistente come modello di modulo. Questo schema XML rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end dell&#39;organizzazione.

Le caratteristiche principali dell&#39;utilizzo di uno schema XML sono:

* La struttura dell’XSD viene visualizzata come una struttura nella scheda Content Finder nella modalità di authoring di un modulo adattivo. Puoi trascinare e aggiungere un elemento dalla gerarchia XSD al modulo adattivo.
* È possibile precompilare il modulo utilizzando XML conforme allo schema associato.
* Al momento dell’invio, i dati immessi dall’utente vengono inviati come XML in linea con lo schema associato.

Uno schema XML è costituito da tipi di elementi semplici e complessi. Gli elementi dispongono di attributi che aggiungono regole all’elemento. Quando questi elementi e attributi vengono trascinati in un modulo adattivo, vengono mappati automaticamente al corrispondente componente Modulo adattivo.

Di seguito è riportata la mappatura degli elementi XML con i componenti del modulo adattivo:

<table>
 <tbody>
  <tr>
   <th><strong>Elemento o attributo XML </strong></th>
   <th><strong>Componente modulo adattivo</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>Casella di testo</td>
  </tr>
  <tr>
   <td><code>xs:boolean</code></td>
   <td>Casella di selezione</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>Tutti i tipi di valori numerici</li>
    </ul> </td>
   <td>Casella numerica</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>Selettore data</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>Elenchi a discesa</td>
  </tr>
  <tr>
   <td>Qualsiasi elemento di tipo complesso</td>
   <td>Pannello</td>
  </tr>
 </tbody>
</table>

## Schema XML di esempio {#sample-xml-schema}

Di seguito è riportato un esempio di schema XML.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartBirth" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>Verificare che lo schema XML contenga un solo elemento principale. Schema XML con più elementi radice non supportato.

## Aggiunta di proprietà speciali ai campi utilizzando lo schema XML {#adding-special-properties-to-fields-using-xml-schema}

È possibile aggiungere i seguenti attributi agli elementi dello schema XML per aggiungere proprietà speciali ai campi del modulo adattivo associato.

<table>
 <tbody>
  <tr>
   <th><strong>Proprietà schema</strong></th>
   <th><strong>Uso in un modulo adattivo</strong></th>
   <th><strong>Supportato in </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>Contrassegna un campo come obbligatorio<br /> </td>
   <td>Attributo</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>Aggiunge un valore predefinito</td>
   <td>Elemento e attributo</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>Specifica le occorrenze minime</p> <p>(Per sottomaschere ripetibili (tipi complessi))</p> </td>
   <td>Elemento (tipo complesso)</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>Specifica le occorrenze massime</p> <p>(Per sottomaschere ripetibili (tipi complessi))</p> </td>
   <td>Elemento (tipo complesso)</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Quando trascini un elemento schema in un modulo adattivo, viene generata una didascalia predefinita da:
>
>* Uso dell&#39;iniziale maiuscola nel nome dell&#39;elemento
>* Inserimento di uno spazio vuoto nei limiti della Camel Case.
>
>Ad esempio, se si aggiunge l&#39;elemento dello schema `userFirstName`, la didascalia generata nel modulo adattivo è `User First Name`.

## Limitare valori accettabili per un componente Modulo adattivo {#limit-acceptable-values-for-an-adaptive-form-component}

Per limitare i valori accettabili per un componente Modulo adattivo, è possibile aggiungere le seguenti restrizioni agli elementi dello schema XML:

<table>
 <tbody>
  <tr>
   <td><p><strong> Proprietà schema</strong></p> </td>
   <td><p><strong>Tipo di dati</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero massimo di cifre consentite in un componente. Il numero di cifre specificato deve essere maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite superiore per valori numerici e date. Per impostazione predefinita, il valore massimo è incluso.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico<br /> </li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite inferiore per i valori numerici e le date. Per impostazione predefinita, è incluso il valore minimo.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere inferiori al valore numerico o alla data specificati per la proprietà maximum.</p> <p>Se false, il valore numerico o la data specificati nel componente del modulo deve essere minore o uguale al valore numerico o alla data specificati per la proprietà maximum.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere maggiori del valore numerico o della data specificati per la proprietà minimum.</p> <p>Se false, il valore numerico o la data specificati nel componente del modulo devono essere maggiori o uguali al valore numerico o alla data specificati per la proprietà minimum.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero minimo di caratteri consentito in un componente. La lunghezza minima deve essere uguale o maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero massimo di caratteri consentiti in un componente. La lunghezza massima deve essere maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero esatto di caratteri consentiti in un componente. La lunghezza deve essere uguale o maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero massimo di posizioni decimali consentite in un componente. FractionDigits deve essere uguale o maggiore di zero.</p> </td>
   <td>
    <ul>
     <li> Casella numerica con tipo di dati float o decimal</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica la sequenza dei caratteri. Un componente accetta i caratteri se questi sono conformi al modello specificato.</p> <p>La proprietà pattern viene mappata sul pattern di convalida del componente Modulo adattivo corrispondente.</p> </td>
   <td>
    <ul>
     <li>Tutti i componenti Forms adattivi mappati su uno schema XSD </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Domande frequenti {#frequently-asked-questions}

**Ho una struttura lunga e complessa in Content Finder. Come trovare un elemento specifico?**

Sono disponibili due opzioni:

* Scorri nella struttura ad albero
* Utilizzare la casella di ricerca per trovare un elemento

**Cos&#39;è un bindRef?**

`bindRef` è la connessione tra un componente Modulo adattivo e un elemento o un attributo dello schema. Determina `XPath` dove il valore acquisito da questo componente o campo è disponibile nell&#39;XML di output. `bindRef` viene utilizzato anche quando si precompila un valore di campo da XML precompilato (precompilato).

**Perché non è possibile trascinare singoli elementi di una sottomaschera (struttura generata da qualsiasi tipo complesso) per sottomaschere ripetibili (i valori minOccours o maxOccurs sono maggiori di 1)?**

In una sottomaschera ripetibile è necessario utilizzare la sottomaschera Completa. Se desideri solo campi selettivi, utilizza l’intera struttura ed elimina quelli indesiderati.

>[!MORELIKETHIS]
>
>* [Progetta schema JSON per un modulo adattivo](/help/forms/adaptive-form-json-schema-form-model.md)