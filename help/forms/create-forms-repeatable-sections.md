---
title: Come si creano pannelli ripetibili nei componenti core modulo adattivo?
description: Scopri come creare sezioni o campi ripetibili in un modulo adattivo.
role: Architect, Developer, Admin, User
feature: Adaptive Forms, Core Components
exl-id: 02521bf3-83c1-40a0-8fe6-23af240727e9
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1258'
ht-degree: 8%

---

# Creare moduli con sezioni ripetibili (Componenti core) {#repeat-panel}


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-forms-repeatable-sections.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Una sezione ripetibile fa riferimento a una parte di un modulo che può essere duplicata o ripetuta più volte per raccogliere informazioni per più istanze degli stessi dati.

Si consideri, ad esempio, un modulo utilizzato per raccogliere informazioni sull’esperienza lavorativa di una persona. È possibile che sia disponibile una sezione ripetibile per l’acquisizione dei dettagli di ogni processo precedente. In genere, la sezione ripetibile contiene campi quali il nome dell’azienda, la qualifica, le date di assunzione e le responsabilità lavorative. L’utente può aggiungere più istanze della sezione ripetibile per immettere informazioni su ogni lavoro svolto.

![Ripetibilità](/help/forms/assets/repeatable-adaptive-form-example.gif)

Alla fine di questo articolo imparerai a:

* Creare una sezione ripetibile in un modulo adattivo
* Impostare il numero minimo o massimo di ripetizioni per un componente Modulo adattivo
* Utilizza l’editor di regole per configurare azioni di aggiunta o eliminazione per le sezioni ripetibili

È possibile utilizzare i componenti [Pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel), [Pannello a soffietto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=it), [Schede orizzontali](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=it), [Schede verticali](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) o [Procedura guidata](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=it) per rendere ripetibili le sezioni di un modulo adattivo. È possibile aggiungere componenti figlio a questi componenti per creare una sezione ripetibile in un modulo.


Gli esempi in questo documento si basano sul componente [Panel](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel). È possibile eseguire gli stessi passaggi per rendere ripetibili i componenti [Pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel), [Pannello a soffietto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=it), [Schede orizzontali](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=it), [Schede verticali](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) o [Procedura guidata](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=it).

## Aggiungere o eliminare sezioni ripetibili in un modulo {#add-or-delete-repeatable-section-in-panel-container}

Per ripetere un pannello nel modulo o rimuovere pannelli ripetibili, un autore del modulo utilizza un componente pulsante per aggiungere o rimuovere un’istanza del pannello. Per aggiungere o eliminare sezioni ripetibili (pannelli) in un modulo:

* [Rendi il contenitore del pannello ripetibile](#make-panel-container-repeatable)
* [Aggiungi sezione ripetibile](#add-repeatable-section-using-instance-manager-via-scripts)
* [Elimina sezioni ripetibili](#delete-repeatable-section-using-instance-manager-via-scripts)

### Rendi il contenitore pannello ripetibile {#make-panel-container-repeatable}

![Scheda Accessibilità](/help/forms/assets/repeat-panel.png)

Per rendere ripetibile un pannello, effettuate le seguenti operazioni:

1. Selezionare un contenitore di pannelli e selezionare ![cmppr](/help/forms/assets/cmppr.png).
1. Fai clic sul **pannello di ripetizione** e attiva l&#39;opzione per **rendere il pannello ripetibile**.
1. Imposta **ripetizioni minime** come richiesto per le sezioni ripetibili minime. Puoi impostare **ripetizioni minime** su zero per la mancata ripetizione dei pannelli o per rimuovere i pannelli ripetuti. Per impostazione predefinita, il valore minimo di ripetizione è zero.
1. Imposta **il numero massimo di ripetizioni** per ripetere il numero di volte richieste nel pannello; per impostazione predefinita il valore è infinito.

   >[!NOTE]
   >
   > 
   > * Il valore di ripetizione minima non può essere -ve.
   > * Per creare un pannello non ripetibile, imposta il valore del campo massimo e minimo su uno.

### Aggiungi sezione ripetibile utilizzando Gestione istanze (tramite script) {#add-repeatable-section-using-instance-manager-via-scripts}

L’elemento principale del pannello da ripetere deve contenere un pulsante Aggiungi per gestire l’istanza di ripetizione del pannello. Per inserire pulsanti nell&#39;elemento padre e attivare gli script sui pulsanti, effettuare le seguenti operazioni:

1. Aggiungi un **componente pulsante** all&#39;elemento padre del pannello. Nell&#39;esempio di video seguente, viene utilizzato un componente pulsante con il nome dell&#39;etichetta **Add** e il nome del campo **AddPanel**. Selezionare il componente e selezionare ![edit-rules](/help/forms/assets/edit-rules.png). Le regole del componente Pulsante si aprono nell’editor di regole.
1. Nella finestra Editor regole, fai clic su **Crea**.

   Selezionare **Editor visivo** nella riga Oggetti e funzioni modulo.

   1. Nell&#39;area delle regole, in WHEN, selezionare lo stato **su cui fare clic**.
   1. In THEN, seleziona **Aggiungi istanza** e trascina il pannello utilizzando ![toggle-side-panel](/help/forms/assets/toggle-side-panel.png) oppure selezionalo utilizzando **Rilascia oggetto o seleziona qui.**

   Selezionare **Editor di codice** nella riga Oggetti e funzioni modulo. Fai clic su **Modifica regole** e nell&#39;area del codice:

   * Per creare un pulsante Aggiungi pannello, specificare `this.panel.instanceManager.addInstance()`

   Fai clic su **Fine**.

>[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)


### Eliminare le sezioni ripetibili utilizzando Gestione istanze (tramite script) {#delete-repeatable-section-using-instance-manager-via-scripts}

L’elemento padre del pannello deve contenere un pulsante Elimina per eliminare l’istanza dei pannelli ripetibili. Per inserire pulsanti nell&#39;elemento padre e abilitare gli script sui pulsanti per eliminare i pannelli ripetibili, effettuare le seguenti operazioni:

1. Aggiungi un **componente pulsante** all&#39;elemento padre del pannello. Nel video seguente viene utilizzato un componente pulsante con il nome etichetta **delete** e il nome campo **DeletePanel**. Selezionare il componente e selezionare ![edit-rules](/help/forms/assets/edit-rules.png). Le regole del componente Pulsante si aprono nell’editor di regole.
1. Nella finestra Editor regole, fai clic su **Crea**.

   Selezionare **Editor visivo** nella riga Oggetti e funzioni modulo.

   1. Nell&#39;area delle regole, in WHEN **DeletePanel**, selezionare lo stato **su cui si fa clic**.
   1. In THEN, seleziona **Rimuovi istanza** e trascina il pannello tramite ![toggle-side-panel](/help/forms/assets/toggle-side-panel.png) oppure selezionalo tramite **Rilascia oggetto o seleziona qui.**

   Selezionare **Editor di codice** nella riga Oggetti e funzioni modulo. Fai clic su **Modifica regole** e nell&#39;area del codice:

   * Per creare un pulsante Elimina pannello, specificare `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

   Fai clic su **Fine**.

>[!VIDEO](https://video.tv.adobe.com/v/3421620/adaptive-forms-repeatable-sections)

>[!NOTE]
>
>Se un campo appartiene a un pannello ripetibile, non è possibile accedervi direttamente utilizzando il relativo nome negli script. Per accedere al campo, specificare l&#39;istanza ripetibile a cui appartiene il campo utilizzando l&#39;API `instances` in `InstanceManager`. Sintassi per l&#39;utilizzo dell&#39;API `instances` in `InstanceManager`:
>
>
>`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
>
>
>Ad esempio, puoi creare un modulo adattivo con un pannello ripetibile con una casella di testo. Quando si precompila il modulo con tre caselle di testo ripetibili, è necessario il codice xml seguente:
>
>
>`<panel1><textbox1>AA1</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA2</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA3</panel1></textbox1>`
>
>
>Per leggere i dati AA1, specifica:
>
>
>`Panel1.instanceManager.instances[0].textbox.value`
>
>
>Per leggere i dati AA2, specifica:
>
>
>`Panel1.instanceManager.instances[1].textbox.value`
>
>
>

>[!NOTE]
>
> Quando tutte le istanze di un pannello vengono rimosse da un modulo adattivo, per aggiungere un’istanza del pannello rimosso, utilizza la sintassi _panelName per acquisire la gestione delle istanze del pannello e l’API addInstance di gestione istanze per aggiungere l’istanza eliminata. Ad esempio, &quot;_panelName.addInstance()&quot;. Aggiunge un’istanza del pannello rimosso.

## Utilizzo di sottomaschere ripetute dal modello di modulo (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

La sottomaschera ripetibile è simile ai pannelli ripetibili in Adaptive Forms. Per creare una sottomaschera ripetuta in AEM Forms Designer, effettuare le seguenti operazioni:

1. Nella tavolozza Gerarchia selezionare la sottomaschera padre della sottomaschera che si desidera ripetere.
1. Nella tavolozza Oggetto fare clic sulla scheda Sottomodulo e nell&#39;elenco Contenuto selezionare Flussi.
1. Selezionare la sottomaschera da ripetere.
1. Nella tavolozza Oggetto, fare clic sulla scheda Sottomodulo e selezionare Posizionato o Flusso nell&#39;elenco Contenuto.
1. Fare clic sulla scheda Associazione e selezionare Ripeti sottomaschera per ogni elemento dati.
1. Per specificare il numero minimo di ripetizioni, selezionare Conteggio minimo e digitare un numero nella casella associata. Se questa opzione è impostata su 0 e non vengono forniti dati per gli oggetti nel sottomodulo al momento dell&#39;unione dei dati, il sottomodulo non viene posizionato al momento del rendering del modulo.
1. Per specificare il numero massimo di ripetizioni di sottomaschera, selezionare Max e digitare un numero nella casella associata. Se non si specifica un valore nella casella Max, il numero di ripetizioni della sottomaschera è illimitato.
1. Per specificare un numero impostato di ripetizioni di sottomaschera, indipendentemente dalla quantità di dati, selezionare Conteggio iniziale e digitare un numero nella casella associata. Se si seleziona questa opzione e non sono disponibili dati o sono presenti meno voci di dati rispetto al valore Conteggio iniziale specificato, le istanze vuote del sottomodulo verranno comunque inserite nel modulo.
1. Aggiungere due pulsanti nella sottomaschera padre: uno per aggiungere un&#39;istanza e un altro per eliminare un&#39;istanza di una sottomaschera ripetibile. Per i passaggi dettagliati, vedi [Generare un&#39;azione](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Collega ora il modello di modulo al modulo adattivo. Per i passaggi dettagliati, consulta [Creare un modulo adattivo basato su un modello](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=en#create-an-adaptive-form-based-on-an-xfa-form-template).
1. Utilizzare i pulsanti creati nel passaggio 9 per aggiungere e rimuovere sottomaschere.

Il file .zip allegato contiene un modulo secondario ripetibile di esempio.

[Ottieni file](/help/forms/assets/samplerepeatablesubform.zip)

## Utilizzo delle impostazioni di ripetizione di uno schema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

È possibile creare pannelli ripetibili da uno schema XML e dalla proprietà minOccours &amp; maxOccurs di qualsiasi elemento di tipo complesso. Per informazioni dettagliate sullo schema XML, vedere [Creare moduli adattivi utilizzando lo schema XML come modello di modulo](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-xml-schema-form-model.html).

Nel codice seguente, il pannello `SampleType` utilizza la proprietà minOccours &amp; maxOccurs.

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
                <xs:element name="assignmentStartDate" type="xs:date"/>
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


## Consulta anche {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
>* [Create style or themes for your forms](using-themes-in-core-components.md)
>* [Add dynamic behavior to forms using the rule editor](rule-editor.md)
>* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/console-layout.md)

-->