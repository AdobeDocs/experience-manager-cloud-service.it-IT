---
title: Creare Forms coinvolgente utilizzando i componenti core e headless
seo-title: Build Engaging Forms Using Core Components and Headless
description: Creare Forms coinvolgente utilizzando i componenti core e headless
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: 26a4450c8b722fd4ca074abb3c260983c1ae0c64
workflow-type: tm+mt
source-wordcount: '3411'
ht-degree: 3%

---


# Creare Forms coinvolgente utilizzando i componenti core e headless

## Panoramica di Lab

In questo laboratorio pratico imparate:

Come utilizzare AEM Forms per creare facilmente moduli adattivi utilizzando i componenti core più recenti, coerenti con AEM Sites, abilitare esperienze di acquisizione dati omnicanale consegnando i moduli adattivi come moduli headless al web, mobile e chat. Inoltre, puoi imparare le best practice relative allo stile, alle personalizzazioni e allo sviluppo front-end.

## Principali aspetti

* **Agilità aziendale**: In qualità di utente aziendale, posso creare facilmente un’esperienza Form per più canali.

* **Sviluppatore da potenza a frontend**: In qualità di sviluppatore front-end, posso controllare l’esperienza dell’utente finale utilizzando moduli headless.

* **Velocity per sviluppatori**: In qualità di sviluppatore, posso personalizzare facilmente e in modo coerente i componenti Sites e Forms.

## Prerequisiti


+++AEM Forms come sandbox di Cloud Service



<table>
        <thead>
            <tr><th>name</th><th>URL istanza autore</th><th>URL dell’istanza di pubblicazione</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## Lezione 1

### Obiettivo

Acquisisci familiarità con l’ambiente as a Cloud Service di AEM Forms.

### Contesto della lezione

In questa lezione imparerai a conoscere l’ambiente as a Cloud Service di AEM Forms navigando nell’interfaccia utente.

### Esercizio

1. Apri il browser e immetti l’URL dell’ambiente di authoring di Cloud Service. Esempio:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Accedi all’ambiente di authoring di Cloud Service. Le credenziali di accesso per l’ambiente di authoring verranno condivise con te durante il laboratorio.

1. Dopo aver effettuato l’accesso, passa all’interfaccia utente di AEM Forms. Fai clic su **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Fai clic su **Forms e documenti**. Ignora eventuali pop-up relativi a preferenze o informazioni.

   ![](/help/forms/assets/screenshot2028113929.png)

   Vengono visualizzati tutti i moduli disponibili.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lezione 2

### Obiettivo

Crea un modulo adattivo utilizzando i componenti core più recenti, configuralo e invialo.

### Contesto della lezione

In questa lezione, in qualità di utente aziendale, verrà creato un modulo adattivo per più canali, come web, dispositivi mobili e chat, utilizzando l’authoring di moduli adattivi con componenti OOTB standard di base per l’acquisizione dei dati.

### Esercizio

1. Creare un endpoint di invio per il modulo:

   1. Apri <https://requestbin.com/> in una nuova scheda del browser.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Fai clic su **Creare un bin pubblico** e copia l&#39;URL dell&#39;endpoint.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Creare un modulo adattivo utilizzando l’interfaccia della procedura guidata:

   1. Nella scheda del browser utilizzata nella lezione 1, accedi ad AEM Forms come interfaccia Web di Cloud Service e passa a Forms e Documenti.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Fai clic su **Crea** e selezionare Modulo adattivo.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Seleziona la **Vuoto con componenti core** modello dalla schermata di selezione del modello come mostrato di seguito:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Fai clic sul pulsante **Stile** e seleziona la **wknd-theme** tema come mostrato di seguito:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Fai clic sul pulsante **Invio** e seleziona la **Invia a punto finale REST** e specifica il bin pubblico nel
      **URL della richiesta POST** come mostrato di seguito:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Fai clic su **Crea**. Specificare un nome e un titolo per il modulo. Ad esempio: **contacto**. Fai clic su **Crea**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. Viene aperto l’editor di moduli adattivi. Ignora finestre a comparsa o finestre di dialogo per preferenze o informazioni. Fai clic sul browser Componenti nella barra a sinistra e aggiungi la **Piè di pagina** nella parte inferiore del modulo vuoto.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. L’intestazione fa parte del modello di modulo adattivo. Consente di fornire in modo semplice un’intestazione/piè di pagina coerente in tutti i moduli adattivi. In alternativa, puoi anche scegliere di mantenere la modifica nel modulo, come mostrato per il componente Piè di pagina nel passaggio successivo.

   1. Aggiungi un **Titolo** al centro del modulo.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Aggiungi un **Input testo** dopo il componente titolo.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Aggiungi un **Ingresso numero** componente.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Aggiungi un **Pulsante Invia** al modulo.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Fai clic sul pulsante **Titolo** in modo che **menu a comparsa** viene visualizzato. Fai clic sul pulsante **Icona Modifica** nel menu per modificare l’etichetta.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Invio `Contact Us` come testo del titolo.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Fai clic sul pulsante **Input testo** in modo da visualizzare il menu a comparsa. Fai clic sul pulsante **Icona Modifica** nel menu per modificare l’etichetta.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Invio **Nome completo** come etichetta di campo.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Fai clic sul pulsante **Ingresso numero** in modo da visualizzare il menu a comparsa. Fai clic sul pulsante **Icona Modifica** nel menu per modificare l’etichetta.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Inserisci il **Numero di telefono** come etichetta del campo.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Aggiungi convalide al modulo:

   1. Fai clic sul pulsante **Numero di telefono** in modo da visualizzare il menu a comparsa. Fai clic sul pulsante **Icona chiave** nel menu per configurare il campo .
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Apri **scheda convalide**, contrassegna il campo **Obbligatorio** e fai clic su **Fine**. Viene visualizzato il messaggio di successo.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Fai clic su **Anteprima** per visualizzare l’anteprima del modulo dal punto di vista dell’utente finale.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Compila il modulo con dati fittizi
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Invia il modulo
      ![](/help/forms/assets/screenshot2028125729.png)

   1. Nella scheda Raccoglitore richieste , controlla i dati inviati.
      ![](/help/forms/assets/screenshot2028125829.png)

Ora, per lo scopo dell’esercizio rimanente, utilizza un modulo di registrazione precreato.

1. Apri l’interfaccia di gestione di AEM Forms, ad esempio: `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`, quindi seleziona il modulo di registrazione.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Fate clic su **Pubblica**. 

   ![](/help/forms/assets/screenshot2028115629.png)

   Viene visualizzato il messaggio di successo.

   ![](/help/forms/assets/screenshot2028115729.png)

   L’URL di pubblicazione del modulo sarà simile a `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Per visualizzare il modulo pubblicato, sostituisci l’ID del programma (pXXXX) e l’ID dell’ambiente (eXXXX) nell’URL precedente con gli ID dell’ambiente.

## Lezione 3

### Obiettivo

Aggiornare gli stili utilizzando le best practice di sviluppo front-end.

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, viene illustrato come aggiornare facilmente lo stile del modulo adattivo creato in precedenza.

### Esercizio

Imposta archivio locale del tema:

1. Apri il prompt dei comandi o la shell con i diritti di amministratore:

   ![](/help/forms/assets/screenshot2028115829.png)

1. Al prompt dei comandi, utilizzare il comando seguente per passare a **c:\git** cartella

   ```Shell
   cd c:\git
   ```

1. Usa il seguente comando per clonare il codice di front-end del tema:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Utilizza il seguente comando nell’ordine elencato per passare alla **aem-forms-theme-canvas** e aprire Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Seleziona **Considera attendibili gli autori di tutti i file presenti nella cartella principale** e fai clic su **Sì, mi fido degli autori**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Per eseguire il rendering del modulo ospitato nell’ambiente di pubblicazione del servizio cloud, rinominare il `env_template` file.  Per rinominare il file, fai clic con il pulsante destro del mouse sul **env_template** e seleziona il **Rinomina** opzione .

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Imposta i seguenti valori per le variabili nel file .env e salva il file :

   * **AEM_URL**: Specifica l’ambiente di pubblicazione del servizio cloud. Esempio, `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**: Specificare il percorso del modulo. Ad esempio, se il percorso del modulo è `/content/forms/af/registration`, il valore di questa variabile è `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. Nella finestra Prompt dei comandi eseguire il comando seguente:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Se ricevi un messaggio che chiede di aggiornare npm tramite il `npm notice Run npm nstall -g npm@9.6.0`ignorare il messaggio.
   > * Non eseguire altri comandi npm a meno che non sia indicato nella cartella di lavoro.


1. Esegui il comando seguente per visualizzare l’anteprima del modulo.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   Una volta eseguito il comando precedente, attendi che `webpack compiled` messaggio. Il modulo viene visualizzato in una scheda del browser.

   >[!NOTE]
   >
   >Se si verifica una schermata vuota nel browser dopo l&#39;esecuzione `npm run live` per più di 3-4 minuti, cambiare `localhost` nell’URL del browser a 127.0.0.1 e hit **Invio**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. In Codice di Visual Studio aprire la `PROJECT\src\site\_variables.scss` file. Osserva che `$error` il colore è un&#39;ombra di ROSSO.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Nel browser, invia il modulo per visualizzare il colore rosso nel **Nome** campo .

   ![](/help/forms/assets/screenshot2028120829.png)

1. Imposta la **$error** a colori **#5736eb** e salva il file.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Aggiornare il browser e inviare il modulo. Il colore di errore nel campo del nome è stato modificato di conseguenza.

   ![](/help/forms/assets/screenshot2028121129.png)

1. Nel prompt dei comandi, premere **CTRL+C**, inserisci **Y**, e premere **Invio** chiave per interrompere il processo npm. È importante arrestare il server npm in modo che non sia in conflitto con il successivo set di esercizi.
1. Chiudere le finestre di Visual Studio Code e Command Prompt.

## Lezione 4

### Obiettivo

Eseguire il rendering del modulo su web/mobile e altre interfacce come modulo headless.

### Contesto della lezione

In questa lezione, in qualità di sviluppatore principale, imparerai come eseguire il rendering del modulo adattivo creato in precedenza come modulo headless utilizzando il framework di progettazione dello spettro di reazione.

### Esercizio

Imposta l’archivio locale utilizzando il progetto di avvio react:

1. Apri il prompt dei comandi utilizzando i diritti di amministratore.

   ![](/help/forms/assets/screenshot2028115829.png)

1. Al prompt dei comandi, utilizzare il comando seguente per passare a **c:\git** cartella

   ```Shell
   cd c:\git
   ```

1. Usa il seguente comando per clonare il progetto iniziale react del modulo adattivo:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Utilizza i seguenti comandi nell&#39;ordine elencato per passare alla **react-starter-kit-aem-headless forms** e aprire Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Viene visualizzata la finestra Codice di Visual Studio.

   ![](/help/forms/assets/screenshot2028117429.png)

Per eseguire il rendering del modulo ospitato nell’ambiente di pubblicazione del servizio cloud:

1. Rinomina il file env_template in file .env. Per rinominare, fai clic con il pulsante destro del mouse sul pulsante **env_template** e seleziona il **Rinomina** opzione .

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Imposta i seguenti valori per le variabili nel file .env . Dopo aver aggiornato le variabili, salva il file .

   * **AEM_URL**: Specifica l’URL dell’ambiente di pubblicazione del servizio cloud. Esempio, `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**: Specifica il percorso del modulo adattivo creato nella lezione precedente. Esempio, `/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Apri la finestra dei comandi, assicurati di essere nella directory react-starter-kit-aem-headless-forms ed esegui il seguente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. Nella finestra Prompt dei comandi eseguire il comando seguente:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   Il comando precedente avvia un server di sviluppo locale che eseguirà il rendering della definizione del modulo recuperata da AEM in modo headless utilizzando la libreria front-end a spettro di risposta.

   >[!NOTE]
   >
   > 
   > Se si verifica una schermata vuota nel browser dopo l&#39;esecuzione `npm start` per più di 3-4 minuti, cambiare `localhost` nell’URL del browser a 127.0.0.1 e hit **Invio**.

   ![](/help/forms/assets/screenshot2028118229.png)

Controlliamo l&#39;esecuzione delle regole in questo modulo headless:

1. Seleziona la **Seleziona la casella per ricevere il 5% di sconto** opzione . L&#39;opzione successiva per l&#39;applicazione della carta di credito è disabilitata.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Deseleziona **Seleziona la casella per ricevere il 5% di sconto** per abilitare l&#39;opzione della carta di credito.

   ![](/help/forms/assets/screenshot2028126329.png)

Apporta le modifiche al modulo sul server come utente aziendale e visualizza automaticamente le modifiche nel modulo headless.

1. Apri l’interfaccia di gestione di AEM Forms nel browser. Ad esempio: [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Seleziona la **registrazione** modulo e fai clic su **Modifica.** Apre il modulo nell’editor di moduli adattivi.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Seleziona la **Numero di telefono** e fai clic sul campo **Icona Modifica (icona a forma di matita)** nella barra degli strumenti. Se la barra degli strumenti a comparsa non è visibile, passare alla modalità Modifica facendo clic su **Modifica** in alto a destra, da sinistra a sinistra **Anteprima** pulsante .

   ![](/help/forms/assets/screenshot2028119629.png)

1. Cambia l’etichetta in Numero mobile. Fare clic su uno spazio vuoto nel modulo per salvare le modifiche apportate al modulo.

   ![](/help/forms/assets/screenshot2028119729.png)

Pubblichiamo il modulo aggiornato per propagare le modifiche all’ambiente di pubblicazione.

1. Nella scheda dell’interfaccia di gestione di AEM Forms, seleziona il modulo di registrazione e fai clic su **Annulla pubblicazione**. Se non visualizzi il **Annulla pubblicazione** , passa al passaggio 3 per pubblicare direttamente le modifiche.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Fai clic su **Annulla pubblicazione**. Fai clic su **Chiudi** nel rispettivo dialogo.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. Dopo l&#39;aggiornamento del browser, seleziona il modulo di registrazione e fai clic su **Pubblica**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Fai clic su **Pubblica**. Fai clic su **Chiudi** nel rispettivo dialogo.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Aggiorna la scheda del browser con il modulo headless visualizzato. Nota che l’etichetta del numero di telefono è stata modificata in Mobile Number (Numero cellulare).

   ![](/help/forms/assets/screenshot2028120529.png)

1. Apri la finestra del prompt dei comandi utilizzata per avviare la **react-starter-kit-aem-headless forms** progetto, stampa **CTRL+C**, quindi immetti **Y** e premere il tasto Enter per terminare il processo npm. È importante arrestare il server npm in modo che non sia in conflitto con il successivo set di esercizi.

1. Chiudere le finestre di Visual Studio Code e Command Prompt.


## Lezione 5

### Obiettivo

Eseguire il rendering del modulo come modulo headless utilizzando l’interfaccia utente Google Material

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, viene illustrato come eseguire il rendering del modulo adattivo creato in precedenza come modulo headless utilizzando l’interfaccia utente Google Material.

### Esercizio

Imposta archivio locale utilizzando il progetto iniziale dell’interfaccia utente materiale:

1. Apri il prompt dei comandi utilizzando i diritti di amministratore.

   ![](/help/forms/assets/screenshot2028115829.png)


1. Al prompt dei comandi, utilizzare il comando seguente per passare a **c:\git** cartella:

   ```Shell
   cd c:\git
   ```

1. Esegui i seguenti comandi nell&#39;ordine elencato per creare una cartella denominata mui e passa alla cartella mui utilizzando i seguenti comandi:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Usa il seguente comando per clonare il progetto iniziale react del modulo adattivo:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Utilizza il seguente comando nell’ordine elencato per passare alla **react-starter-kit-aem-headless forms** e aprire il codice in Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Per eseguire il rendering del modulo ospitato nell’ambiente di pubblicazione del servizio cloud:

1. Rinomina il **env_template** file a **.env** file. Per rinominare, fai clic con il pulsante destro del mouse sul pulsante **env_template** e seleziona **Rinomina**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Imposta i seguenti valori per le variabili nel file .env . Dopo aver aggiornato le variabili, salva il file . Utilizza la **CTRL+S** cambiare combinazione per salvare il file.

   * **AEM_URL**: Specifica l’URL dell’ambiente di pubblicazione del servizio cloud. Ad esempio: [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**: Specifica il percorso del modulo adattivo creato nella lezione precedente. Ad esempio, /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Apri la finestra dei comandi e assicurati di essere nella **react-starter-kit-aem-headless forms** ed esegui il comando seguente:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. Nella finestra Prompt dei comandi eseguire il comando seguente:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   Il comando avvia un server di sviluppo locale ed esegue il rendering della definizione del modulo recuperata da AEM in modo headless utilizzando la libreria front-end dell’interfaccia utente di Google Material.

   >[!NOTE]
   >
   >Se si verifica una schermata vuota nel browser dopo l&#39;esecuzione `npm start` per più di 3-4 minuti, cambiare `localhost` nell’URL del browser a 127.0.0.1 e hit **Invio**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Per valutare l’esecuzione della stessa logica di business nel rendering del modulo:

   Seleziona **Seleziona la casella per ricevere il 5% di sconto**. Opzione successiva **Desideri richiedere il modulo di carta di credito aziendale We.Finance?** viene disattivato.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lezione 6

### Obiettivo

Crea un aspetto e un aspetto alternativi del modulo headless utilizzando le varianti dei componenti dell’interfaccia utente materiale

### Contesto della lezione

In questa lezione, in qualità di sviluppatore front-end, viene illustrato come creare una rappresentazione alternativa di diversi componenti utilizzando l’interfaccia utente di Material per il modulo adattivo creato in precedenza dall’utente aziendale.

### Esercizio

Aggiorna la variazione dei componenti nel progetto headless. Per modificare la variante del componente di input di testo dell’interfaccia utente del materiale in `OutlinedInput`:

1. In Codice visivo, passa al componente di input del testo aprendo la `index.tsx` file a `src/components/textinput/index.tsx`.

1. Aggiungi `//` all&#39;inizio della riga codice 103. Converte la riga in un commento.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Aggiungi quanto segue alla riga 104 per utilizzare una variante diversa del componente e salva il file. Utilizza la **CTRL+S** cambiare combinazione per salvare il file.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   È essenziale utilizzare la maiuscola corretta per la variante &#39;OutlineInput&#39; altrimenti la compilazione avrebbe esito negativo. La compilazione dell&#39;ambiente di sviluppo locale inizia automaticamente nel prompt dei comandi. Attendi che venga visualizzato il seguente messaggio

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Aggiorna il browser, se non si aggiorna automaticamente, per visualizzare che il componente di input di testo utilizzi una variante diversa.

   ![](/help/forms/assets/screenshot2028127729.png)


   Questa modifica viene applicata agli utenti finali senza alcuna modifica alla definizione del modulo in AEM Forms Server ed è specifica per il canale headless in esame. Per esempio, un canale web in questo laboratorio.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Chiudere le finestre di prompt dei comandi e codice di Visual Studio.

## Domande frequenti

+++ La procedura guidata Moduli adattivi è disponibile pubblicamente?

Sì, è disponibile con AEM Forms come Cloud Service.

+++


+++ I componenti core sono disponibili pubblicamente?

Sì, i componenti core Forms adattivi sono disponibili con AEM Forms come Cloud Service.

+++

+++ I moduli headless sono disponibili pubblicamente?

Sì, i moduli headless sono disponibili con AEM Forms come Cloud Service.

+++

+++ I moduli headless richiedono una licenza separata?

No, i moduli headless utilizzano la stessa metrica del valore di licenza, del numero di invii dei moduli.

+++

+++ I componenti core e i moduli headless sono disponibili con Forms 6.5 AEM?

Sì, sia i componenti core dei moduli adattivi che i moduli headless sono disponibili con AEM Forms 6.5 Service Pack 16 e successivi.

+++


## Passaggi successivi

Ora che hai imparato a creare moduli adattivi e a distribuirli a più canali utilizzando moduli headless, dovresti cercare di mettere in atto le tue nuove competenze. Divertiti e continua creando e distribuendo esperienze di acquisizione dati eccezionali agli utenti finali, dove sono, su larga scala!

## Riferimenti

* [Introduzione ai componenti core per moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [Creare un modulo adattivo utilizzando i componenti core](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [Stile di aggiornamento per AF basato su componenti core](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Moduli adattivi headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [Utilizzo del kit iniziale Headless React](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


