---
title: Introduzione agli oggetti di ambito nelle funzioni personalizzate
description: Il modulo supporta gli oggetti ambito nelle funzioni personalizzate che vengono passati come ultimo argomento alle funzioni quando viene eseguita la regola.
keywords: oggetti di ambito in funzioni personalizzate, oggetti globali, oggetti campo.
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: af211649a4f22d06f4e8669335a8267ee948a408
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Oggetto ambito nelle funzioni personalizzate

In Adaptive Forms, un oggetto ambito viene passato come ultimo argomento alle funzioni quando viene eseguita una regola. Può essere utilizzato per leggere le proprietà di un modulo/campo e modificare il modulo dall’interno delle funzioni. L&#39;oggetto ambito contiene un oggetto proxy di sola lettura per il modulo, l&#39;evento attivato e il campo di destinazione. È possibile accedere alle proprietà del modulo e del campo utilizzando l&#39;oggetto ambito aggiungendo `$`, ad esempio `scope.form.$id` e `scope.field.$id`, rispettivamente.

## Funzioni di modifica dei moduli tramite l’oggetto ambito

L’oggetto ambito dispone delle seguenti funzioni per la modifica del modulo:

| Funzione | Sintassi | Descrizione | Esempio di codice |
|-----------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------|
| **setProperty** | `setProperty(any $element, any $payload)` | Imposta una proprietà di `$element` utilizzando `$payload`. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) per visualizzare l&#39;esempio. |
| **convalida** | `validate([any $element])` | Esegue la convalida su `$element`. Se non viene fornito alcun elemento, viene convalidato l’intero modulo. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) per visualizzare l&#39;esempio. |
| **reimposta** | `reset([any $element])` | Reimposta `$element`. Se non viene fornito alcun elemento, viene ripristinato l’intero modulo. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) per visualizzare l&#39;esempio. |
| **importData** | `importData(any $payload)` | Importa i dati nel modulo, sostituendo eventuali dati del modulo esistenti. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) per visualizzare l&#39;esempio. |
| **exportData** | `exportData()` | Restituisce i dati del modulo. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) per visualizzare l&#39;esempio. |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | Attiva l&#39;invio di un modulo. Il parametro `$data` specifica cosa inviare e `$submit_as` definisce il tipo di contenuto (impostazione predefinita: &#39;multipart/form-data&#39;). L&#39;elemento facoltativo `$validate_form` determina se il modulo deve essere convalidato (impostazione predefinita: true). Al completamento, `submitSuccess` viene attivato; in caso di errore, `submitError` viene attivato. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) per visualizzare l&#39;esempio. |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | Attiva `$element`, che può essere un pannello o un campo. Se non viene fornito alcun elemento, lo stato attivo viene impostato sul campo che ha attivato la regola. Il parametro facoltativo `$focusOption` (di tipo enum `FocusOption`) specifica se concentrarsi su &#39;nextItem&#39; o &#39;previousItem&#39; relativo a `$element`. Se è specificato un pannello, la navigazione è limitata a tale pannello; con un campo, la navigazione avviene nel pannello principale. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) per visualizzare l&#39;esempio. |
| **dispatchEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | Invia un evento di tipo `$eventName` sull&#39;elemento specificato da `$element`. Se non viene fornito alcun elemento, l’evento viene inviato sul modulo. L&#39;elemento facoltativo `$payload` è disponibile per le espressioni che gestiscono l&#39;evento. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) per visualizzare l&#39;esempio. |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | Contrassegna il campo identificato da `$fieldIdentifier` come non valido e imposta il messaggio di convalida su `$validationMessage`. Il parametro facoltativo `$option` specifica se `$fieldIdentifier` viene interpretato come `id`, `name` o `dataRef`. Il valore predefinito è `{useId: true}` e i valori supportati includono `{useId: true}`, `{useDataRef: true}` e `{useQualifiedName: true}`. | [Fare clic qui](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) per visualizzare l&#39;esempio. |

## Consulta anche

{{see-also-rule-editor}}