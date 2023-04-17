---
title: Creare moduli efficaci utilizzando i componenti core e headless
seo-title: Build Engaging Forms Using Core Components and Headless
description: Creare moduli efficaci utilizzando i componenti core e headless
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: f65c5241e1e61e5a0bd9981778939caa313de76a
workflow-type: ht
source-wordcount: '3412'
ht-degree: 100%

---


# Creare moduli efficaci utilizzando i componenti core e headless

## Panoramica del workshop

In questo workshop pratico imparerai:

come utilizzare AEM Forms per creare facilmente moduli adattivi utilizzando i componenti core più recenti, coerenti con AEM Sites, per rendere possibili esperienze di acquisizione dei dati omnicanale grazie alla distribuzione di moduli adattivi come moduli headless al web, ai mobile e alle chat. Inoltre, puoi imparare le best practice relative allo stile, alle personalizzazioni e allo sviluppo front-end.

## Elementi principali da ricordare

* **Agilità dell’azienda**: in qualità di utente aziendale, posso creare facilmente un’esperienza con i moduli per più canali.

* **Più controllo per gli sviluppatori front-end**: in qualità di sviluppatore front-end, posso controllare l’esperienza dell’utente finale utilizzando moduli headless.

* **Velocità di sviluppo**: in qualità di sviluppatore, posso personalizzare i componenti Sites e Forms in modo facile e coerente.

## Prerequisiti


+++Sandbox di AEM Forms as Cloud Service



<table>
        <thead>
            <tr><th>ID workshop</th><th>URL dell’istanza di authoring</th><th>URL dell’istanza di pubblicazione</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## Lezione 1

### Obiettivo

Acquisisci familiarità con l’ambiente di AEM Forms as a Cloud Service.

### Contesto della lezione

In questa lezione imparerai a conoscere l’ambiente di AEM Forms as a Cloud Service navigando nell’interfaccia utente.

### Esercizio

1. Apri il browser e immetti l’URL dell’ambiente di authoring di Cloud Service. Ad esempio:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Accedi all’ambiente di authoring di Cloud Service. Le credenziali di accesso per l’ambiente di authoring verranno condivise con te durante il laboratorio.

1. Dopo aver effettuato l’accesso, passa all’interfaccia utente di AEM Forms. Fai clic su **Moduli**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Fai clic su **Moduli e documenti**. Ignora eventuali messaggi a comparsa relativi a preferenze o informazioni.

   ![](/help/forms/assets/screenshot2028113929.png)

   Vengono visualizzati tutti i moduli disponibili.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lezione 2

### Obiettivo

Crea un modulo adattivo utilizzando i componenti core più recenti, configuralo e invialo.

### Contesto della lezione

In questa lezione, in qualità di utente aziendale, verrà creato un modulo adattivo per più canali, come web, dispositivi mobili e chat, utilizzando l’authoring di moduli adattivi con componenti core standard predefiniti per l’acquisizione dei dati.

### Esercizio

1. Crea un endpoint di invio per il modulo:

   1. Apri <https://requestbin.com/> in una nuova scheda del browser.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Fai clic su **Crea un bin pubblico** e copia l’URL dell’endpoint.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Crea un modulo adattivo utilizzando l’interfaccia della procedura guidata:

   1. Nella scheda del browser utilizzata nella lezione 1, vai all’interfaccia web di AEM Forms as Cloud Service e passa a moduli e documenti.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Fai clic su **Crea** e seleziona Modulo adattivo.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Seleziona il modello **Vuoto con i componenti core** dalla schermata di selezione del modello come mostrato di seguito:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Fai clic sulla scheda **Stile** e seleziona il tema **wknd-theme** come mostrato di seguito:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Fai clic sulla scheda **Invio** e seleziona la scheda **Invia a endpoint REST** e specifica il bin pubblico nel
      campo **URL della richiesta POST** come illustrato di seguito:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Fai clic su **Crea**. Specifica un nome e un titolo per il modulo. Ad esempio: **contattaci**. Fai clic su **Crea**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. Viene aperto l’editor di moduli adattivi. Chiudi eventuali pop-up o finestre di dialogo relativi a preferenze o informazioni. Fai clic sul browser componenti nella barra a sinistra e aggiungi il componente **Piè di pagina** nella parte inferiore del modulo vuoto.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. L’intestazione fa parte del modello di modulo adattivo. Consente di applicare in maniera semplice un’intestazione/piè di pagina coerente in tutti i moduli adattivi. In alternativa, è possibile anche scegliere di mantenerla modificabile nel modulo, come illustrato per il componente Piè di pagina nel passaggio successivo.

   1. Aggiungi un componente **Titolo** al centro del modulo.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Aggiungi un componente **Inserimento testo** dopo il componente titolo.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Aggiungi un componente **Inserimento numero**.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Aggiungi un componente **Pulsante Invia** al modulo.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Fai clic sul componente **Titolo** in modo da visualizzare il **menu a comparsa**. Fai clic sull’**icona Modifica** nel menu per modificare l’etichetta.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Inserisci `Contact Us` come testo del titolo.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Fai clic sul componente **Inserimento testo** in modo da visualizzare il menu a comparsa. Fai clic sull’**icona Modifica** nel menu per modificare l’etichetta.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Inserisci il **Nome completo** come etichetta del campo.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Fai clic sul componente **Inserimento numero** in modo da visualizzare il menu a comparsa. Fai clic sull’**icona Modifica** nel menu per modificare l’etichetta.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Inserisci il **Numero di telefono** come etichetta del campo.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Aggiungi convalide al modulo:

   1. Fai clic sul componente **Numero di telefono** in modo da visualizzare il menu a comparsa. Fai clic sull’**icona a forma di chiave inglese** nel menu per configurare il campo.
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Apri la **scheda convalide**, contrassegna il campo come **Obbligatorio** e fai clic su **Fine**. Viene visualizzato il messaggio di operazione riuscita.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Fai clic su **Anteprima** per visualizzare l’anteprima del modulo dal punto di vista dell’utente finale.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Compila il modulo con dati fittizi
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Invia il modulo
      ![](/help/forms/assets/screenshot2028125729.png)

   1. Nella scheda Raccoglitore richieste, controlla i dati inviati.
      ![](/help/forms/assets/screenshot2028125829.png)

Ora, per lo scopo dell’esercizio rimanente, utilizza un modulo di registrazione già creato.

1. Apri l’interfaccia di gestione di AEM Forms, ad esempio: `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`, quindi seleziona il modulo di registrazione.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Fai clic su **Pubblica**.

   ![](/help/forms/assets/screenshot2028115629.png)

   Viene visualizzato il messaggio di operazione riuscita.

   ![](/help/forms/assets/screenshot2028115729.png)

   L’URL di pubblicazione del modulo sarà simile a `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Per visualizzare il modulo pubblicato, sostituisci l’ID del programma (pXXXXXX) e l’ID dell’ambiente (eXXXXXX) nell’URL precedente con l’ID 
del tuo ambiente.

## Lezione 3

### Obiettivo

Aggiornare gli stili utilizzando le best practice di sviluppo front-end.

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, ti verrà illustrato come aggiornare facilmente lo stile del modulo adattivo creato in precedenza.

### Esercizio

Configurazione dell’archivio locale del tema:

1. Apri il prompt o la shell dei comandi con i diritti di amministratore:

   ![](/help/forms/assets/screenshot2028115829.png)

1. Sul prompt dei comandi, utilizza il comando seguente per passare alla cartella **c:\git**

   ```Shell
   cd c:\git
   ```

1. Per clonare il codice di front-end del tema, utilizza il comando seguente:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Per passare alla directory **aem-forms-theme-canvas** e aprire Visual Studio Code, utilizza il seguente comando nell’ordine elencato.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Seleziona **Considera affidabili gli autori di tutti i file presenti nella cartella principale** e fai clic su **Sì, considero affidabili gli autori**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Per eseguire il rendering del modulo ospitato nell’ambiente di pubblicazione del cloud service, rinomina il file `env_template`.  Per rinominare il file, fai clic con il pulsante destro del mouse sul file **env_template** e seleziona l’opzione **Rinomina**.

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Imposta i seguenti valori per le variabili nel file .env e salva il file:

   * **AEM_URL**: specifica l’ambiente di pubblicazione del cloud service. Ad esempio `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**: specifica il percorso del modulo. Ad esempio, se il percorso del modulo è `/content/forms/af/registration`, il valore di questa variabile sarà `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. Nella finestra del prompt dei comandi esegui il comando seguente:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Se ricevi un messaggio che chiede di aggiornare npm tramite il comando `npm notice Run npm nstall -g npm@9.6.0`, ignora il messaggio.
   > * Non eseguire altri comandi npm a meno che non sia indicato nella cartella di lavoro.


1. Ora, per visualizzare l’anteprima del modulo, esegui il comando seguente.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   Una volta eseguito il comando precedente, attendi il messaggio `webpack compiled`. Il modulo viene visualizzato in una scheda del browser.

   >[!NOTE]
   >
   >Se, dopo l’esecuzione del comando `npm run live`, nel browser viene visualizzata una schermata vuota per più di 3-4 minuti, cambia `localhost` nell’URL del browser con 127.0.0.1 e premi **Invio**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. In Visual Studio Code, apri il file `PROJECT\src\site\_variables.scss`. Nota che il colore `$error` è una tonalità di rosso.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Nel browser, invia il modulo per visualizzare il colore rosso nel campo **Nome**.

   ![](/help/forms/assets/screenshot2028120829.png)

1. Imposta il colore di **$error** su **#5736eb** e salva il file.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Aggiorna il browser e invia il modulo. Nota che il colore dell’errore è stato modificato anche nel campo del nome.

   ![](/help/forms/assets/screenshot2028121129.png)

1. Nel prompt dei comandi, premi **CTRL+C**, immetti **Y** e premi il tasto **Invio** per interrompere il processo npm. È importante interrompere il server npm in modo che non entri in conflitto con il successivo set di esercizi.
1. Chiudi le finestre di Visual Studio Code e il prompt dei comandi.

## Lezione 4

### Obiettivo

Eseguire il rendering del modulo per web/mobile e altre interfacce come modulo headless.

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, ti verrà illustrato come eseguire il rendering del modulo adattivo creato in precedenza come modulo headless utilizzando il framework di progettazione di React Spectrum.

### Esercizio

Configurazione dell’archivio locale utilizzando il progetto iniziale di React:

1. Apri il prompt dei comandi utilizzando i diritti di amministratore.

   ![](/help/forms/assets/screenshot2028115829.png)

1. Sul prompt dei comandi utilizza il comando seguente per passare alla cartella **c:\git**

   ```Shell
   cd c:\git
   ```

1. Per clonare il progetto iniziale di React del modulo adattivo, utilizza il comando seguente:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Per passare alla directory **react-starter-kit-aem-headless forms** e aprire Visual Studio Code, utilizza i comandi seguenti nell’ordine elencato.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Si apre la finestra di Visual Studio Code.

   ![](/help/forms/assets/screenshot2028117429.png)

Per eseguire il rendering del modulo ospitato nell’ambiente di pubblicazione del cloud service:

1. Rinomina il file env_template in file .env. Per rinominarlo, fai clic con il pulsante destro del mouse sul file **env_template** e seleziona l’opzione **Rinomina**.

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Imposta i seguenti valori per le variabili nel file .env. Dopo aver aggiornato le variabili, salva il file.

   * **AEM_URL**: specifica l’URL dell’ambiente di pubblicazione del cloud service. Ad esempio `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**: specifica il percorso del modulo adattivo creato nella lezione precedente. Ad esempio `/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Apri la finestra dei comandi, assicurati di essere nella directory react-starter-kit-aem-headless-forms ed esegui il seguente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. Nella finestra del prompt dei comandi esegui il comando seguente:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   Il comando precedente avvia un server di sviluppo locale che eseguirà il rendering della definizione del modulo recuperata da AEM in modo headless utilizzando la libreria front-end di React Spectrum.

   >[!NOTE]
   >
   > 
   > Se, dopo l’esecuzione del comando `npm start`, nel browser viene visualizzata una schermata vuota per più di 3-4 minuti, cambia `localhost` nell’URL del browser con 127.0.0.1 e premi **Invio**.

   ![](/help/forms/assets/screenshot2028118229.png)

Verifichiamo l’esecuzione delle regole in questo modulo headless:

1. Scegli l’opzione **Seleziona la casella per ricevere il 5% di sconto**. L’opzione successiva per la richiesta della carta di credito è disabilitata.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Deseleziona **Seleziona la casella per ricevere il 5% di sconto** per abilitare l’opzione della carta di credito.

   ![](/help/forms/assets/screenshot2028126329.png)

Apporta le modifiche al modulo sul server come utente aziendale e visualizza le modifiche riprodotte automaticamente nel modulo headless.

1. Apri l’interfaccia di gestione di AEM Forms nel browser. Ad esempio: [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Seleziona il modulo di **registrazione** e fai clic su **Modifica.** Il modulo viene aperto nell’editor di moduli adattivi.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Seleziona il campo **Numero di telefono** e fai clic sull’**icona Modifica (a forma di matita)** nella barra degli strumenti. Se la barra degli strumenti a comparsa non è visibile, passa alla modalità Modifica facendo clic sul pulsante **Modifica** in alto a destra, a sinistra del pulsante **Anteprima**.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Cambia l’etichetta in Numero cellulare. Fai clic su uno spazio vuoto nel modulo per salvare le modifiche apportate.

   ![](/help/forms/assets/screenshot2028119729.png)

Pubblichiamo il modulo aggiornato per propagare le modifiche all’ambiente di pubblicazione.

1. Nella scheda dell’interfaccia di gestione di AEM Forms, seleziona il modulo di registrazione e fai clic su **Annulla pubblicazione**. Se non viene visualizzato il pulsante **Annulla pubblicazione**, vai al passaggio 3 per pubblicare le modifiche direttamente.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Fai clic su **Annulla pubblicazione**. Fai clic su **Chiudi** nella rispettiva finestra di dialogo.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. Dopo l’aggiornamento del browser, seleziona il modulo di registrazione e fai clic su **Pubblica**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Fai clic su **Pubblica**. Fai clic su **Chiudi** nella rispettiva finestra di dialogo.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Aggiorna la scheda del browser con il modulo headless visualizzato. Nota che l’etichetta del numero di telefono è stata modificata in Numero cellulare.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Apri la finestra del prompt dei comandi utilizzata per avviare il progetto **react-starter-kit-aem-headless forms**, premi **CTRL+C**, quindi 
immetti **Y** e premi il tasto Invio per terminare il processo npm. È importante interrompere il server npm in modo che non entri in conflitto con il successivo set di esercizi.

1. Chiudi le finestre di Visual Studio Code e il prompt dei comandi.


## Lezione 5

### Obiettivo

Eseguire il rendering del modulo come modulo headless utilizzando l’interfaccia utente Google Material

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, ti verrà illustrato come eseguire il rendering del modulo adattivo creato in precedenza come modulo headless utilizzando l’interfaccia utente Google Material.

### Esercizio

Imposta l’archivio locale utilizzando il progetto iniziale dell’interfaccia utente Material:

1. Apri il prompt dei comandi utilizzando i diritti di amministratore.

   ![](/help/forms/assets/screenshot2028115829.png)


1. Al prompt dei comandi, utilizza il comando seguente per passare alla cartella **c:\git**:

   ```Shell
   cd c:\git
   ```

1. Esegui i seguenti comandi nell’ordine elencato per creare una cartella denominata “mui” e passa alla cartella “mui” utilizzando i seguenti comandi:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Per clonare il progetto iniziale di React del modulo adattivo, utilizza il comando seguente:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Per passare alla cartella **react-starter-kit-aem-headless forms** e aprire il codice in Visual Studio Code, utilizza il comando seguente nell&#39;ordine elencato:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Per eseguire il rendering del modulo ospitato nell’ambiente di pubblicazione del cloud service:

1. Rinomina il file **env_template** in file **.env**. Per rinominarlo, fai clic con il pulsante destro del mouse sul file **env_template** e seleziona **Rinomina**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Imposta i seguenti valori per le variabili nel file .env. Dopo aver aggiornato le variabili, salva il file. Utilizza la combinazione di tasti **CTRL+S** per salvare il file.

   * **AEM_URL**: specifica l’URL dell’ambiente di pubblicazione del cloud service. Ad esempio: [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**: specifica il percorso del modulo adattivo creato nella lezione precedente. Ad esempio, /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Apri la finestra dei comandi, assicurati di essere nella directory **react-starter-kit-aem-headless forms** ed esegui il comando seguente:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. Nella finestra del prompt dei comandi esegui il comando seguente:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   Il comando avvia un server di sviluppo locale che esegue il rendering della definizione del modulo recuperata da AEM in modo headless utilizzando la libreria front-end 
dell’interfaccia utente Google Material.

   >[!NOTE]
   >
   >Se, dopo l’esecuzione del comando `npm start`, nel browser viene visualizzata una schermata vuota per più di 3-4 minuti, cambia `localhost` nell’URL del browser con 127.0.0.1 e premi **Invio**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Per valutare l’esecuzione della stessa logica di business nella rappresentazione del modulo:

   Fai clic su **Seleziona la casella per ricevere il 5% di sconto**. L’opzione successiva **Desideri richiedere il modulo per la carta di credito della società We.Finance?** viene disattivata.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lezione 6

### Obiettivo

Creare un aspetto alternativo del modulo headless utilizzando le varianti dei componenti dell’interfaccia utente Material

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, ti verrà illustrato come creare una rappresentazione alternativa di componenti diversi utilizzando l’interfaccia utente Material per il modulo adattivo creato in precedenza dall’utente aziendale.

### Esercizio

Aggiorna la variante dei componenti nel progetto headless. Per modificare la variante del componente di inserimento testo dell’interfaccia utente Material in `OutlinedInput`:

1. In Visual Code, passa al componente di inserimento testo aprendo il file `index.tsx` in `src/components/textinput/index.tsx`.

1. Aggiungi `//` all’inizio della riga di codice 103. Converte la riga in un commento.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Aggiungi quanto segue alla riga 104 per utilizzare una variante diversa del componente e salva il file. Utilizza la combinazione di tasti **CTRL+S** per salvare il file.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   È necessario utilizzare le maiuscole corrette per la variante “OutlineInput”; in caso contrario la compilazione avrà esito negativo. La compilazione dell’ambiente di sviluppo locale inizia automaticamente nel prompt dei comandi. Attendi che venga visualizzato il seguente messaggio:

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Se la pagina nel browser non si aggiorna automaticamente, aggiornala per visualizzare il componente di input di testo con una variante diversa.

   ![](/help/forms/assets/screenshot2028127729.png)


   Questa modifica viene applicata agli utenti finali senza alcuna modifica alla definizione del modulo nel server di AEM Forms ed è specifica per il canale headless in esame. Per esempio, un canale web in questo workshop.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Chiudi le finestre di Visual Studio Code e il prompt dei comandi.

## Domande frequenti (FAQ)

+++ La procedura guidata per moduli adattivi è disponibile pubblicamente?

Sì, è disponibile in AEM Forms as Cloud Service.

+++


+++ I componenti core sono disponibili pubblicamente?

Sì, i componenti core per moduli adattivi sono disponibili in AEM Forms as Cloud Service.

+++

+++ I moduli headless sono disponibili pubblicamente?

Sì, i moduli headless sono disponibili in AEM Forms as Cloud Service.

+++

+++ I moduli headless richiedono una licenza separata?

No, i moduli headless utilizzano la stessa metrica del valore di licenza, numero di invii dei moduli.

+++

+++ I componenti core e i moduli headless sono disponibili in AEM Forms 6.5?

Sì, sia i componenti core per moduli adattivi che i moduli headless sono disponibili in AEM Forms 6.5 Service Pack 16 e versioni successive.

+++


## Passaggi successivi

Ora che hai imparato a creare i moduli adattivi e a distribuirli su più canali utilizzando moduli headless, puoi provare a mettere in pratica le tue nuove competenze. Buon lavoro, e continua a creare e distribuire esperienze eccezionali con acquisizione dati, per i tuoi utenti finali ovunque si trovano e su larga scala!

## Riferimenti

* [Introduzione ai componenti core per moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it)

* [Creare un modulo adattivo utilizzando i componenti core](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=it)

* [Aggiornare lo stile per moduli adattivi basati su componenti core](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=it)

* [Moduli adattivi headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it)

* [Utilizzo dello starter kit Headless React](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=it)


