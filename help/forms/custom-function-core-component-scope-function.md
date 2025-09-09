---
title: Introduzione agli oggetti di ambito nelle funzioni personalizzate
description: Il modulo supporta gli oggetti ambito nelle funzioni personalizzate che vengono passati come ultimo argomento alle funzioni quando viene eseguita la regola.
keywords: oggetti di ambito in funzioni personalizzate, oggetti globali, oggetti campo.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 248c75a5-6335-41d2-aa0a-28a20a710f88
source-git-commit: e2bc958104bd9b75845ad2c213eec18d2560a3a4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# Oggetto ambito nelle funzioni personalizzate

In Adaptive Forms, un oggetto ambito viene passato come ultimo argomento alle funzioni quando viene eseguita una regola. Può essere utilizzato per leggere le proprietà di un modulo/campo e modificare il modulo dall’interno delle funzioni. L&#39;oggetto ambito contiene un oggetto proxy di sola lettura per il modulo, l&#39;evento attivato e il campo di destinazione. È possibile accedere alle proprietà del modulo e del campo utilizzando l&#39;oggetto ambito aggiungendo `$`, ad esempio `scope.form.$id` e `scope.field.$id`, rispettivamente.

## Funzioni di modifica dei moduli tramite l’oggetto ambito

L’oggetto ambito dispone delle seguenti funzioni per la modifica del modulo:

| Funzione | Sintassi | Descrizione | Esempio di codice |
|-----------------|--------|-------------|-------------|
| **setProperty** | `setProperty(any $element, any $payload)` | Imposta una proprietà sul campo di destinazione utilizzando `$payload`. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) per visualizzare l&#39;esempio. |
| **convalida** | `validate([any $element])` | Esegue la convalida nel campo di destinazione. Esegue la convalida sull&#39;intero modulo se non viene fornita alcuna destinazione e restituisce una matrice di errori di convalida. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) per visualizzare l&#39;esempio. |
| **reimposta** *(obsoleto)* | `reset([any $element])` | Obsoleto. Utilizza invece `dispatchEvent($target, 'reset')`. Reimposta il campo di destinazione o, se non viene fornita alcuna destinazione, reimposta l&#39;intero modulo. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) per visualizzare l&#39;esempio. |
| **importData** | `importData(any $payload)` | Importa i dati nel modulo, sostituendo eventuali dati del modulo esistenti. Se si specifica `qualifiedName`, i dati vengono importati solo nel campo contenitore. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) per visualizzare l&#39;esempio. |
| **exportData** | `exportData()` | Restituisce i dati del modulo. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) per visualizzare l&#39;esempio. |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | Attiva l&#39;invio di un modulo. È possibile specificare cosa inviare tramite il parametro `$payload` e impostare il tipo di contenuto tramite il parametro `$contentType`. I dati vengono inviati come `multipart/form-data` per impostazione predefinita. Il parametro facoltativo `$validateForm` specifica se il modulo deve essere convalidato prima dell&#39;invio (impostazione predefinita: true). Al completamento, `submitSuccess` viene attivato; in caso di errore, `submitError` viene attivato. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) per visualizzare l&#39;esempio. |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | Imposta lo stato attivo sul campo di destinazione, che può essere un pannello o un campo modulo. Se non viene fornita alcuna destinazione, lo stato attivo viene impostato sul campo che ha attivato la regola. Il parametro facoltativo `$focusOption` specifica se l&#39;elemento successivo o precedente relativo alla destinazione deve essere attivato. Valori supportati: `'nextItem'`, `'previousItem'`. Se utilizzato con un pannello, la navigazione è limitata a tale pannello. Se utilizzata con un campo, la navigazione avviene all’interno del pannello principale di tale campo. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) per visualizzare l&#39;esempio. |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | Invia un evento di tipo `$eventName` sull&#39;elemento determinato da `$target`. Se non viene fornita alcuna destinazione, l’evento viene inviato sul modulo. L&#39;elemento facoltativo `$payload` è disponibile per le espressioni che gestiscono l&#39;evento. Il parametro facoltativo `$dispatch` controlla il comportamento di propagazione degli eventi. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) per visualizzare l&#39;esempio. |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | Contrassegna il campo identificato da `$fieldIdentifier` come non valido e visualizza `$validationMessage`. Il parametro facoltativo `$option` specifica se `$fieldIdentifier` viene interpretato come `id`, `dataRef` o `qualifiedName`. Il valore predefinito è `{useId: true}`. Valori supportati: `{useId: true}`, `{useDataRef: true}`, `{useQualifiedName: true}`. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) per visualizzare l&#39;esempio. |

## Consulta anche

{{see-also-rule-editor}}

