---
title: Elabora risorse tramite gestori di file multimediali e flussi di lavoro
description: Scopri i diversi gestori di contenuti multimediali e come utilizzarli nei flussi di lavoro per eseguire attività sulle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Elabora risorse tramite gestori di file multimediali e flussi di lavoro {#processing-assets-using-media-handlers-and-workflows}

Risorse Adobe Experience Manager (AEM) viene fornito con una serie di flussi di lavoro e gestori di contenuti multimediali predefiniti per l’elaborazione delle risorse. Il flusso di lavoro definisce le attività generali da eseguire sulle risorse, quindi delega le attività specifiche ai gestori dei contenuti multimediali, ad esempio generazione di miniature o estrazione di metadati.

Potete definire un flusso di lavoro che verrà eseguito automaticamente quando una risorsa di un particolare tipo viene caricata sul server. I passaggi di elaborazione sono definiti in termini di una serie di gestori di file multimediali di AEM Assets. AEM offre alcuni gestori [integrati,](#default-media-handlers) e altri possono essere sviluppati [o definiti](#creating-a-new-media-handler) personalizzati delegando il processo a uno strumento [della riga di](#command-line-based-media-handler)comando.

I gestori di file multimediali sono servizi all’interno di Risorse AEM che eseguono azioni specifiche sulle risorse. Ad esempio, quando un file audio MP3 viene caricato in AEM, un flusso di lavoro attiva un gestore MP3 che estrae i metadati e genera una miniatura. I gestori di file multimediali vengono generalmente utilizzati in combinazione con i flussi di lavoro. La maggior parte dei tipi MIME comuni è supportata in AEM. Per eseguire specifiche attività sulle risorse è possibile estendere/creare flussi di lavoro, estendere/creare gestori di contenuti multimediali o disattivare/abilitare i gestori di contenuti multimediali.

>[!NOTE]
>
>Consulta l’articolo Formati [di file supportati da](file-format-support.md) Risorse per una descrizione di tutti i formati supportati da Risorse AEM, nonché delle funzioni supportate per ciascun formato.

## Gestori file multimediali predefiniti {#default-media-handlers}

I seguenti gestori di file multimediali sono disponibili in AEM Assets e gestiscono i tipi MIME più comuni:

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

<table>
 <tbody>
  <tr>
   <td>Nome gestore</td>
   <td>Nome servizio (nella console di sistema)</td>
   <td>Tipi MIME supportati</td>
  </tr>
  <tr>
   <td>TextHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.TextHandler</p> </td>
   <td>text/plain</td>
  </tr>
  <tr>
   <td>PdfHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pdf.PdfHandler</p> </td>
   <td><p>application/pdf<br /> application/illustrator</p> </td>
  </tr>
  <tr>
   <td>JpegHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.JpegHandler</p> </td>
   <td>image/jpeg</td>
  </tr>
  <tr>
   <td>Mp3Handler</td>
   <td><p>com.day.cq.dam.handler.standard.mp3.Mp3Handler</p> </td>
   <td><p>audio/mpeg</p> </td>
  </tr>
  <tr>
   <td>ZipHandler</td>
   <td><p>com.day.cq.dam.handler.standard.zip.ZipHandler</p> </td>
   <td><p>application/java-archive</p> <p>application/zip</p> </td>
  </tr>
  <tr>
   <td>PictHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pict.PictHandler</p> </td>
   <td><p>image/pict</p> </td>
  </tr>
  <tr>
   <td>StandardImageHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.StandardImageHandler</p> </td>
   <td><p>image/gif</p> <p>image/png</p> <p>application/photoshop</p> <p>image/jpeg</p> <p>image/tiff</p> <p>image/x-ms-bmp</p> <p>image/bmp</p> </td>
  </tr>
  <tr>
   <td>MSOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler</td>
   <td>application/msword<br /> </td>
  </tr>
  <tr>
   <td>MSPwerPointHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler</td>
   <td>application/vnd.ms-powerpoint<br /> </td>
  </tr>
  <tr>
   <td>OpenOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler</td>
   <td>application/vnd.openxmlformats-officedocument.wordprocessingml.document<br /> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet<br /> application/vnd.openxmlformats-officedocument.presentationml.presentation<br /><br /> </td>
  </tr>
  <tr>
   <td>EPubHandler</td>
   <td>com.day.cq.dam.handler.standard.epub.EPubHandler</td>
   <td>application/epub+zip</td>
  </tr>
  <tr>
   <td>GenericAssetHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.GenericAssetHandler</p> </td>
   <td>fallback nel caso in cui non sia stato trovato nessun altro gestore per estrarre dati da una risorsa</td>
  </tr>
 </tbody>
</table>

Tutti i gestori eseguono le seguenti operazioni:

* estrazione di tutti i metadati disponibili dalla risorsa.
* creazione di una miniatura della risorsa.

È possibile visualizzare i gestori di contenuti multimediali attivi:

1. In your browser, navigate to `http://localhost:4502/system/console/components`.
1. Fate clic sul collegamento `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Viene visualizzato un elenco con tutti i gestori di contenuti multimediali attivi.

## Utilizzo dei gestori di file multimediali nei flussi di lavoro per eseguire attività sulle risorse {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

I gestori di file multimediali sono servizi solitamente utilizzati in combinazione con i flussi di lavoro.

In AEM sono disponibili alcuni flussi di lavoro predefiniti per l’elaborazione delle risorse. Per visualizzarli, aprite la console Flusso di lavoro e fate clic sulla scheda **[!UICONTROL Modelli]** : i titoli dei flussi di lavoro che iniziano con Risorse AEM sono le risorse specifiche.

I flussi di lavoro esistenti possono essere estesi e possono essere creati nuovi per elaborare le risorse in base a requisiti specifici.

L’esempio seguente mostra come migliorare il flusso di lavoro di **[!UICONTROL Sincronizzazione AEM Assets]** in modo che vengano generate le risorse secondarie di tutte le risorse, eccetto i documenti PDF.

### Disattivazione/abilitazione di un gestore di file multimediali {#disabling-enabling-a-media-handler}

I gestori di contenuti multimediali possono essere disabilitati o abilitati tramite la console di gestione Web Apache Felix. Quando il gestore multimediale è disattivato, le attività non vengono eseguite sulle risorse.

Per attivare/disattivare un gestore di supporti:

1. In your browser, navigate to `https://<host>:<port>/system/console/components`.
1. Fate clic su **[!UICONTROL Disattiva]** accanto al nome del gestore multimediale. Esempio: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Aggiorna la pagina: accanto al gestore multimediale viene visualizzata un&#39;icona che indica che è disattivato.
1. Per abilitare il gestore di file multimediali, fate clic su **[!UICONTROL Abilita]** accanto al nome del gestore.

### Creazione di un nuovo gestore multimediale {#creating-a-new-media-handler}

Per supportare un nuovo tipo di supporto o eseguire attività specifiche su una risorsa, è necessario creare un nuovo gestore di supporti. Questa sezione descrive come procedere.

#### Classi e interfacce importanti {#important-classes-and-interfaces}

Il modo migliore per avviare un&#39;implementazione consiste nell&#39;ereditare da un&#39;implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: la `com.day.cq.dam.core.AbstractAssetHandler` classe.

Questa classe fornisce già un descrittore di servizio astratto. Quindi se ereditate da questa classe e utilizzate il plug-in maven-sling, accertatevi di impostare il flag inherit su `true`.

Implementate i seguenti metodi:

* `extractMetadata()`: estrae tutti i metadati disponibili.
* `getThumbnailImage()`: crea una miniatura della risorsa passata.
* `getMimeTypes()`: restituisce i tipi MIME della risorsa.

Di seguito è riportato un modello di esempio:

`package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts } `

L&#39;interfaccia e le classi includono:

* `com.day.cq.dam.api.handler.AssetHandler` interfaccia: Questa interfaccia descrive il servizio che aggiunge il supporto per tipi MIME specifici. L&#39;aggiunta di un nuovo tipo MIME richiede l&#39;implementazione di questa interfaccia. L&#39;interfaccia contiene metodi per importare ed esportare i documenti specifici, per creare miniature ed estrarre metadati.
* `com.day.cq.dam.core.AbstractAssetHandler` class: Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni utilizzate.
* Classe `com.day.cq.dam.core.AbstractSubAssetHandler`:
   * Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni, oltre a quelle generiche per l’estrazione di risorse secondarie.
   * Il modo migliore per avviare un&#39;implementazione consiste nell&#39;ereditare da un&#39;implementazione astratta fornita che si occupa della maggior parte delle cose e fornisce un comportamento predefinito ragionevole: la classe com.day.cq.dam.core.AbstractAssetHandler.
   * Questa classe fornisce già un descrittore di servizio astratto. Quindi se ereditate da questa classe e utilizzate il plug-in maven-sling, accertatevi di impostare il flag inherit su true.

È necessario implementare i seguenti metodi:

* `extractMetadata()`: questo metodo estrae tutti i metadati disponibili.
* `getThumbnailImage()`: questo metodo crea una miniatura della risorsa passata.
* `getMimeTypes()`: questo metodo restituisce i tipi MIME della risorsa.

Di seguito è riportato un modello di esempio:

package my.own.things; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ classe pubblica MyMediaHandler estende com.day.cq.dam.core.AbstractAssetHandler { // implementa le parti pertinenti }

L&#39;interfaccia e le classi includono:

* `com.day.cq.dam.api.handler.AssetHandler` interfaccia: Questa interfaccia descrive il servizio che aggiunge il supporto per tipi MIME specifici. L&#39;aggiunta di un nuovo tipo MIME richiede l&#39;implementazione di questa interfaccia. L&#39;interfaccia contiene metodi per importare ed esportare i documenti specifici, per creare miniature ed estrarre metadati.
* `com.day.cq.dam.core.AbstractAssetHandler` class: Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni utilizzate.
* `com.day.cq.dam.core.AbstractSubAssetHandler` class: Questa classe funge da base per tutte le altre implementazioni dei gestori di risorse e fornisce funzionalità comuni più comuni per l’estrazione di risorse secondarie.

<!--
#### Example: create a specific Text Handler {#example-create-a-specific-text-handler}

In this section, you will create a specific Text Handler that generates thumbnails with a watermark.

Proceed as follows:

Refer to [Development Tools](../sites-developing/dev-tools.md) to install and set up Eclipse with a Maven plugin and for setting up the dependencies that are needed for the Maven project.

After you perform the following procedure, when you upload a txt file into AEM, the file's metadata are extracted and two thumbnails with a watermark are generated.

1. In Eclipse, create `myBundle` Maven project:

    1. In the Menu bar, click **[!UICONTROL File > New > Other]**.
    1. In the dialog, expand the Maven folder, select Maven Project and click **[!UICONTROL Next]**.
    1. Check the Create a simple project box and the Use default Workspace locations box, then click **[!UICONTROL Next]**.
    1. Define the Maven project:

        * Group Id: com.day.cq5.myhandler
        * Artifact Id: myBundle
        * Name: My AEM bundle
        * Description: This is my AEM bundle

    1. Click **[!UICONTROL Finish]**.

1. Set the Java Compiler to version 1.5:

    1. Right-click the `myBundle` project, select Properties.
    1. Select Java Compiler and set following properties to 1.5:

        * Compiler compliance level
        * Generated .class files compatibility
        * Source compatibility

    1. Click **[!UICONTROL OK]**. In the dialog window, click Yes.

1. Replace the code in the pom.xml file with the following code:

1. Create the package `com.day.cq5.myhandler` that contains the Java classes under `myBundle/src/main/java`:

    1. Under myBundle, right-click `src/main/java`, select New, then Package.
    1. Name it `com.day.cq5.myhandler` and click Finish.

1. Create the Java class `MyHandler`:

    1. In Eclipse, under `myBundle/src/main/java`, right-click the `com.day.cq5.myhandler` package, select New, then Class.
    1. In the dialog window, name the Java Class MyHandler and click Finish. Eclipse creates and opens the file MyHandler.java.
    1. In `MyHandler.java` replace the existing code with the following and then save the changes:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;

   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/

   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }

    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compile the Java class and create the bundle:

    1. Right-click the myBundle project, select **[!UICONTROL Run As]**, then **[!UICONTROL Maven Install]**.
    1. The bundle `myBundle-0.0.1-SNAPSHOT.jar` (containing the compiled class) is created under `myBundle/target`.

1. In CRX Explorer, create a new node under `/apps/myApp`. Name = `install`, Type = `nt:folder`.
1. Copy the bundle `myBundle-0.0.1-SNAPSHOT.jar` and store it under `/apps/myApp/install` (for example with WebDAV). The new text handler is now active in AEM.
1. In your browser, open the Apache Felix Web Management Console. Select the Components tab and disable the default text handler `com.day.cq.dam.core.impl.handler.TextHandler`.

-->

## Gestore multimediale basato su riga di comando {#command-line-based-media-handler}

AEM consente di eseguire qualsiasi strumento della riga di comando all’interno di un flusso di lavoro per convertire le risorse (ad esempio ImageMagick) e aggiungere la nuova rappresentazione alla risorsa. È sufficiente installare lo strumento della riga di comando sul disco in cui risiede il server AEM e aggiungere e configurare un passaggio del processo al flusso di lavoro. Il processo invocato, denominato `CommandLineProcess`, consente inoltre di filtrare in base a tipi MIME specifici e di creare più miniature in base alla nuova rappresentazione.

Le seguenti conversioni possono essere eseguite e memorizzate automaticamente in Risorse AEM:

* Trasformazione EPS e AI tramite [ImageMagick](https://www.imagemagick.org/script/index.php) e [Ghostscript](https://www.ghostscript.com/)
* Transcodifica video FLV tramite [FFmpeg](https://ffmpeg.org/)
* Codifica MP3 con [LAME](http://lame.sourceforge.net/)
* Elaborazione audio con [SOX](http://sox.sourceforge.net/)

>[!NOTE]
>
>Sui sistemi non Windows, lo strumento FFMpeg restituisce un errore durante la generazione di rappresentazioni per una risorsa video con un&#39;unica citazione (&#39;) nel nome del file. Se il nome del file video include un’unica citazione, rimuoverla prima di caricare in AEM.

Il `CommandLineProcess` processo esegue le seguenti operazioni nell&#39;ordine in cui sono elencate:

* Filtra il file in base a tipi MIME specifici, se specificato.
* Crea una directory temporanea sul disco in cui risiede il server AEM.
* Invia il file originale alla directory temporanea.
* Esegue il comando definito dagli argomenti del passaggio. Il comando viene eseguito all’interno della directory temporanea con le autorizzazioni dell’utente che esegue AEM.
* Invia di nuovo il risultato nella cartella di rappresentazione del server AEM.
* Elimina la directory temporanea.
* Crea le miniature in base a tali rappresentazioni, se specificate. Il numero e le dimensioni delle miniature sono definiti dagli argomenti del passaggio.

### Esempio di utilizzo di ImageMagick {#an-example-using-imagemagick}

L’esempio seguente mostra come impostare il passaggio del processo della riga di comando in modo che ogni volta che una risorsa con gif o tiff mime viene aggiunta a /content/dam sul server AEM, un’immagine capovolta dell’originale viene creata insieme a tre miniature aggiuntive (140x100, 48x48 e 10x250).

A questo scopo, si utilizzerà ImageMagick. ImageMagick è una suite software gratuita per creare, modificare e comporre immagini bitmap ed è in genere utilizzata dalla riga di comando.

Prima installa ImageMagick sul disco che ospita il server AEM:

1. Installa ImageMagick: Consulta la documentazione [di](https://www.imagemagick.org/script/download.php)ImageMagick.
1. Impostare lo strumento in modo da poter eseguire la conversione sulla riga di comando.
1. Per verificare se lo strumento è installato correttamente, eseguire il comando seguente `convert -h` sulla riga di comando.

   Viene visualizzata una schermata della guida con tutte le opzioni possibili dello strumento di conversione.

   >[!NOTE]
   >
   >In alcune versioni di Windows (ad esempio, Windows SE), il comando convert potrebbe non essere eseguito in quanto è in conflitto con l&#39;utilità di conversione nativa che fa parte dell&#39;installazione di Windows. In questo caso, indicare il percorso completo per l&#39;utilità ImageMagick utilizzata per convertire i file immagine in miniature. Esempio, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Per verificare se lo strumento viene eseguito correttamente, aggiungete un&#39;immagine .jpg alla directory di lavoro ed eseguite il comando convert `<image-name>.jpg -flip <image-name>-flipped.jpg` sulla riga di comando.

   Un’immagine capovolta viene aggiunta alla directory.

Quindi, aggiungi il passaggio della riga di comando al flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**:

1. Passate alla console **[!UICONTROL Flusso di lavoro]** .
1. Nella scheda **[!UICONTROL Modelli]** , modificate il modello di risorse **[!UICONTROL di aggiornamento]** DAM.
1. Modificate le impostazioni del passaggio di rappresentazione **[!UICONTROL abilitato per il]** Web come segue:

   **Argomenti**:

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. Salvare il flusso di lavoro.

Per testare il flusso di lavoro modificato, aggiungete una risorsa a `/content/dam`.

1. Nel file system, ottenere un&#39;immagine .tiff di vostra scelta. Rinominarlo in `myImage.tiff` e copiarlo in `/content/dam`, ad esempio utilizzando WebDAV.
1. Passate alla console **[!UICONTROL CQ5 DAM]** , ad esempio `http://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Aprite la risorsa **[!UICONTROL myImage.tiff]** e verificate che l’immagine capovolta e le tre miniature siano state create.

#### Configurazione del passo del processo CommandLineProcess {#configuring-the-commandlineprocess-process-step}

Questa sezione descrive come impostare **Argomenti processo** di **CommandLineProcess**.

I valori degli argomenti di **processo** devono essere separati da una virgola e non devono iniziare con uno spazio vuoto.

<table>
 <tbody>
  <tr>
   <td> Argument-Format</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td> mime:&lt;mime-type&gt;</td>
   <td><p>Argomento facoltativo. Il processo viene applicato se la risorsa ha lo stesso tipo MIME dell’argomento.</p> <p>È possibile definire diversi tipi di mime.</p> </td>
  </tr>
  <tr>
   <td> tn:&lt;larghezza&gt;:&lt;altezza&gt;</td>
   <td><p>Argomento facoltativo. Viene creata una miniatura con le dimensioni definite nell’argomento.</p> <p>È possibile definire diverse miniature.<br /> </p> </td>
  </tr>
  <tr>
   <td> cmd: &lt;comando&gt;</td>
   <td><p>Definisce il comando che verrà eseguito. La sintassi dipende dallo strumento della riga di comando.</p> <p>È possibile definire un solo comando.</p> <p>Per creare il comando è possibile utilizzare le seguenti variabili:<br/></p> <p><code>${filename}</code>: nome del file di input, ad esempio `Original.jpg`<br/><code>${file}</code>: nome percorso completo del file di input, ad esempio, `/tmp/cqdam0816.tmp/original.jpg`<br/><code>${directory}</code>: directory del file di input, ad esempio "/tmp/cqdam0816.tmp".<br/> <code>${basename}</code>: nome del file di input senza estensione, ad esempio originale<br/><code>${extension}</code>: estensione del file di input, ad esempio JPG<br/></p></td>
  </tr>
 </tbody>
</table>

Ad esempio, se ImageMagick è installato sul disco che ospita il server AEM e se create un passaggio di processo utilizzando **CommandLineProcess** come implementazione e i seguenti valori come Argomenti **di** processo:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

quindi, quando il flusso di lavoro viene eseguito, il passaggio viene applicato solo alle risorse con immagini/gif o mime:image/tiff come tipi mime, crea un’immagine capovolta dell’originale, la converte in .jpg e crea tre miniature con le dimensioni: 140x100, 48x48 e 10x250.

Per creare le tre miniature standard utilizzando ImageMagick, usate i seguenti argomenti di **processo** :

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Utilizzate i seguenti argomenti **di** processo per creare la rappresentazione abilitata per il Web utilizzando ImageMagick:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>Il passaggio **CommandLineProcess** si applica solo alle risorse (nodi di tipo `dam:Asset`) o ai discendenti di una risorsa.
