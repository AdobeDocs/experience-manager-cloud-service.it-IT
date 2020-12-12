---
sub-product: Implementazione per AEM as a Cloud Service
user-guide-title: Implementazione per AEM as a Cloud Service
breadcrumb-title: Guida all’implementazione
user-guide-description: Questa guida spiega come personalizzare l’implementazione di Experience Manager as a Cloud Service, e contiene argomenti utili per lo sviluppo e l’implementazione.
translation-type: tm+mt
source-git-commit: c82622ad26fecd547c12fff6994713488b9759df
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 45%

---


# Implementazione {#implementing}

+ [Implementazione di applicazioni per AEM as a Cloud Service](/help/implementing/home.md)
+ Utilizzo di Cloud Manager {#using-cloud-manager}
   + [Gestione degli ambienti](cloud-manager/manage-environments.md)
   + [Configurazione della pipeline CI/CD](cloud-manager/configure-pipeline.md)
   + [Implementazione del codice](cloud-manager/deploy-code.md)
   + Risultati dei test {#test-results}
      + [Panoramica](/help/implementing/cloud-manager/overview-test-results.md)
      + [Verifica della qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md)
      + [Regole per la qualità del codice personalizzato](cloud-manager/custom-code-quality-rules.md)
      + [Test funzionale](/help/implementing/cloud-manager/functional-testing.md)
      + [Verifica esperienza](/help/implementing/cloud-manager/experience-audit-testing.md)
      + [Test interfaccia](/help/implementing/cloud-manager/ui-testing.md)
   + [Accesso e gestione dei registri](cloud-manager/manage-logs.md)
   + [Notifiche](cloud-manager/notifications.md)
   + Gestione certificati SSL {#manage-ssl-certificates}
      + [Introduzione](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
      + [Ottenimento di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)
      + [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
      + [Visualizzazione e aggiornamento e sostituzione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
      + [Verifica dello stato di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md)
      + [Eliminazione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
   + Gestione dei nomi di dominio personalizzati {#custom-domain-names}
      + [Introduzione](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
      + [Ottenimento di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/get-custom-domain-name.md)
      + [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
      + [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)
      + [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)
      + [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)
      + [Verifica dello stato del record DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md)
      + [Visualizzazione e aggiornamento e sostituzione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)
      + [Aggiornamento del certificato SSL di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/update-cdn-ssl-certificate.md)
      + [Eliminazione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)
   + Gestione dei Elenchi consentiti di  IP {#ip-allow-lists}
      + [Introduzione](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)
      + [Aggiunta di un Elenco consentiti di  IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
      + [Visualizzazione e aggiornamento di un Elenco consentiti di  IP](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
      + [Applicazione di un Elenco consentiti di  IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
      + [Annullamento dell&#39;applicazione di un elenco di indirizzi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/unapply-ip-allow-list.md)
      + [Eliminazione di un Elenco consentiti di  IP](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)
      + [Verifica dello stato di un Elenco consentiti  IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md)
+ Gestione del codice {#managing-code}
   + [Gestione delle versioni dei progetti Maven](cloud-manager/project-version-handling.md)
   + [Accesso a Git](cloud-manager/accessing-git.md)
   + [Integrazione di Git con Adobe Cloud Manager](cloud-manager/integrating-with-git.md)
   + [Utilizzo di più repository Git di origine](/help/implementing/cloud-manager/working-with-multiple-source-git-repositories.md)
+ Sviluppo per AEM as a Cloud Service {#developing}
   + [Struttura dei progetti AEM](developing/introduction/aem-project-content-package-structure.md)
   + [Pacchetto per la struttura dell’archivio dei progetti AEM](developing/introduction/repository-structure-package.md)
   + [SDK di AEM as a Cloud Service](developing/introduction/aem-as-a-cloud-service-sdk.md)
   + [Linee guida per lo sviluppo per AEM as a Cloud Service](developing/introduction/development-guidelines.md)
   + [Registrazione](developing/introduction/logging.md)
   + [Configurazioni e browser di configurazione](developing/introduction/configurations.md)
   + [AEM Fondamenti Tecnici](/help/implementing/developing/introduction/aem-technologies.md)
   + [API di AEM as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/ref/javadoc/index.html)
   + Sviluppo AEM stack completo {#full-stack}
      + [Guida introduttiva allo sviluppo per AEM Sites - Esercitazione WKND](developing/introduction/develop-wknd-tutorial.md)
      + [Struttura dell’interfaccia AEM](developing/introduction/ui-structure.md)
      + [Guida di riferimento rapido per Sling](developing/introduction/sling-cheatsheet.md)
      + [Utilizzo di adattatori Sling](developing/introduction/sling-adapters.md)
      + [Utilizzo di Sling Resource Merger in AEM as a Cloud Service](developing/introduction/sling-resource-merger.md)
      + [Sovrapposizioni in AEM as a Cloud Service](developing/introduction/overlays.md)
      + [Utilizzo delle librerie lato client](developing/introduction/clientlibs.md)
      + [Differenze tra pagine](/help/implementing/developing/introduction/page-diff.md)
      + [Limitazioni per l’editor](/help/implementing/developing/introduction/editor-limitations.md)
      + [Convenzioni di denominazione](/help/implementing/developing/introduction/naming-conventions.md)
      + Componenti e modelli {#components-templates}
         + [Panoramica sui componenti](developing/components/overview.md)
         + [Modelli](developing/components/templates.md)
         + [Componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html)
         + [Sistema di stili](/help/sites-cloud/authoring/features/style-system.md)
         + [Esportatore JSON per Content Services](developing/components/json-exporter.md)
         + [Abilitazione dell&#39;esportazione JSON per un componente](developing/components/enabling-json-exporter.md)
         + [Editor immagine](developing/components/image-editor.md)
         + [Tag per decorazione](developing/components/decoration-tag.md)
         + [Utilizzo di Nascondi condizioni](developing/components/hide-conditions.md)
         + [Guida di riferimento ai componenti](developing/components/reference.md)
      + [AEM Tagging Framework](/help/implementing/developing/introduction/tagging-framework.md)
      + [Creazione di tag nelle applicazioni AEM](/help/implementing/developing/introduction/tagging-applications.md)
      + Ricerca {#search}
         + [API Query Builder](/help/implementing/developing/introduction/query-builder-api.md)
         + [Riferimento predicato Query Builder](/help/implementing/developing/introduction/query-builder-predicates.md)
         + [Implementazione di un valutatore di predicati personalizzato](/help/implementing/developing/introduction/query-builder-custom-predicate.md)
      + [Pagine di errore personalizzate](/help/implementing/developing/introduction/custom-error-page.md)
      + [Tipi di nodo AEM](/help/implementing/developing/introduction/node-types.md)
      + [Linee guida API Java](/help/implementing/developing/introduction/java-api-guidelines.md)
   + Sviluppo AEM ibrido {#hybrid}
      + [Ibrido e SPA con AEM](https://www.adobe.com/content/dam/www/us/en/marketing/experience-manager-sites/headless-content-management-system/pdfs/aem-hybrid-architecture-wp-1-18-19.pdf)
      + [Abilitazione dell&#39;esportazione JSON per un componente](developing/components/enabling-json-exporter.md)
      + [Introduzione SPA e Procedura dettagliata](developing/hybrid/introduction.md)
      + [SPA Esercitazione WKND](developing/hybrid/wknd-tutorial.md)
      + [Guida introduttiva a React](developing/hybrid/getting-started-react.md)
      + [Guida introduttiva all’uso di Angular](developing/hybrid/getting-started-angular.md)
      + [SPA Dives](developing/hybrid/deep-dives.md)
      + [Sviluppo di SPA per AEM](developing/hybrid/developing.md)
      + [Panoramica dell’editor SPA](developing/hybrid/editor-overview.md)
      + [Blueprint SPA](developing/hybrid/blueprint.md)
      + [Componente pagina SPA](developing/hybrid/page-component.md)
      + [Mappatura modello dinamico a componente](developing/hybrid/model-to-component-mapping.md)
      + [Routing modello](developing/hybrid/routing.md)
      + [Launch Integration](developing/hybrid/launch-integration.md)
      + [Rendering lato server](developing/hybrid/ssr.md)
      + [SPA documenti di riferimento](developing/hybrid/reference-materials.md)
   + Gestione delle esperienze headless {#headless}
      + [Senza testa e AEM](developing/headless/introduction.md)
      + Guide introduttive {#getting-started}
         + [Creazione di una configurazione](developing/headless/getting-started/create-configuration.md)
         + [Creazione di un modello di frammento di contenuto](developing/headless/getting-started/create-content-model.md)
         + [Creazione di una cartella di risorse](developing/headless/getting-started/create-assets-folder.md)
         + [Creazione di un frammento di contenuto](developing/headless/getting-started/create-content-fragment.md)
         + [Accesso e distribuzione di frammenti di contenuto](developing/headless/getting-started/create-api-request.md)
      + Frammenti di contenuto {#content-fragments}
         + [Distribuzione senza titolo con frammenti di contenuto e GraphQL](/help/assets/content-fragments/content-fragments-graphql.md)
         + [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
         + [Abilita funzionalità frammento di contenuto per la tua istanza](/help/assets/content-fragments/content-fragments-configuration-browser.md)
         + [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
         + [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md)
         + [Varianti - Authoring dei contenuti di frammenti](/help/assets/content-fragments/content-fragments-variations.md)
         + [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
         + [Uso di contenuti associati ](/help/assets/content-fragments/content-fragments-assoc-content.md)
         + [Metadati - Proprietà dei frammenti](/help/assets/content-fragments/content-fragments-metadata.md)
         + [Albero struttura](/help/assets/content-fragments/content-fragments-structure-tree.md)
         + [Anteprima - RAPPRESENTAZIONE JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
      + API di consegna {#delivery-api}
         + [API REST per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md)
         + [API GraphQL per frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md)
         + [AEM GraphQL API con frammenti di contenuto - Contenuto di esempio e query](/help/assets/content-fragments/content-fragments-graphql-samples.md)
+ Strumenti per gli sviluppatori {#developer-tools}
   + [AEM Developer Tools for Eclipse](/help/implementing/developing/tools/eclipse.md)
   + [Plug-in Confezione Contenuto](/help/implementing/developing/tools/maven-plugin.md)
   + [AEM Repo Tool](/help/implementing/developing/tools/repo-tool.md)
   + [Utilizzo di CRXDE Lite](/help/implementing/developing/tools/crxde.md)
+ Personalizzazione {#personalization}
   + [ContextHub](developing/personalization/contexthub.md)
   + [Configurazione di ContextHub](developing/personalization/configuring-contexthub.md)
   + [Aggiunta di ContextHub alle pagine](developing/personalization/adding-contexthub.md)
   + [Candidati store di esempio](developing/personalization/sample-stores.md)
   + [Moduli store di esempio](developing/personalization/sample-modules.md)
   + [Diagnostica ContextHub](developing/personalization/contexthub-diagnostics.md)
   + [Estensione di ContextHub](developing/personalization/extending-contexthub.md)
   + [API ContextHub](developing/personalization/contexthub-api.md)
   + [Integrazione con Adobe Target](/help/sites-cloud/integrating/adobe-target.md)
   + [Configurazione della segmentazione con ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
+ Configurazione ed estensione di AEM as a Cloud Service {#configuring-and-extending}
   + [Estensione dei frammenti esperienza](developing/extending/experience-fragments.md)
   + [Personalizzazione ed estensione dei frammenti di contenuto](developing/extending/content-fragments-customizing.md)
   + [Componenti di configurazione dei frammenti di contenuto per il rendering](developing/extending/content-fragments-configuring-components-rendering.md)
   + [Configurazione dei moduli di ricerca](developing/extending/search-forms.md)
   + [Configurare l’editor Rich Text](/help/implementing/developing/extending/rich-text-editor.md)
   + [Configurare i plug-in dell’editor Rich Text](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md)
   + [Configurare l’editor Rich Text per creare siti accessibili](/help/implementing/developing/extending/rte-accessible-content.md)
+ Implementazione in AEM as a Cloud Service {#deploying}
   + [Implementazione in AEM as a Cloud Service](deploying/overview.md)
   + [Aggiornamenti AEM versione](deploying/aem-version-updates.md)
   + [Configurazione di OSGi per AEM as a Cloud Service](deploying/configuring-osgi.md)
+ Livello di authoring {#author-tier}
   + [Accesso al livello di authoring](/help/implementing/author-tier/accessing-the-author-tier.md)
   + [Protezione del livello di authoring](/help/implementing/author-tier/securing-the-author-tier.md)
+ Panoramica della distribuzione dei contenuti {#content-delivery}
   + [Flusso di distribuzione dei contenuti](dispatcher/overview.md)
   + [Dispatcher nel cloud](dispatcher/disp-overview.md)
   + [CDN in AEM as a Cloud Service](dispatcher/cdn.md)
   + [Memorizzazione in cache in AEM as a Cloud Service](dispatcher/caching.md)