---
title: Implementazione di un valutatore predefinito personalizzato per il Generatore di query
description: Query Builder in AEM offre un modo semplice e personalizzabile per eseguire query sull'archivio dei contenuti
translation-type: tm+mt
source-git-commit: 21a0e6967a17ea30435d0343c4aa497f54134cda
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---


# Implementazione di un valutatore predefinito personalizzato per Query Builder {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

Questo documento descrive come estendere il Generatore di query [implementando un valutatore di predicati personalizzato.](query-builder-api.md)

## Panoramica {#overview}

Il [Query Builder](query-builder-api.md) offre un modo semplice per eseguire query nell&#39;archivio dei contenuti. AEM viene fornito con [un set di valutatori predicati](#query-builder-predicates.md) che aiutano a eseguire query sui dati.

Tuttavia, potrebbe essere utile semplificare le query implementando un valutatore di predicati personalizzato che nasconde una certa complessità e assicura una semantica migliore.

Un predicato personalizzato potrebbe anche eseguire altre operazioni non direttamente possibili con XPath, ad esempio:

* Query dei dati da un altro servizio
* Filtro personalizzato basato su un calcolo

>[!NOTE]
>
>Durante l&#39;implementazione di un predicato personalizzato è necessario tenere in considerazione i problemi di prestazioni.

>[!TIP]
>
>Potete trovare esempi di query nel documento [Query Builder](query-builder-api.md).

>[!TIP]
>
>Puoi trovare il codice di questa pagina su GitHub
>
>* [Apri il progetto Aem-search-custom-predicate-evaluate su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)


>[!NOTE]
>
>Questo codice collegato su GitHub e gli snippet di codice in questo documento sono forniti solo a scopo dimostrativo.

### Predicate Valutator in Detail {#predicate-evaluator-in-detail}

Un valutatore predicato gestisce la valutazione di determinati predicati, che sono i vincoli di definizione di una query.

Mappa un vincolo di ricerca di livello superiore (ad esempio `width>200`) a una query JCR specifica che si adatta al modello di contenuto effettivo (ad esempio `metadata/@width > 200`). Oppure può filtrare manualmente i nodi e controllarne i vincoli.

>[!TIP]
>
>Per ulteriori informazioni sul pacchetto `PredicateEvaluator` e `com.day.cq.search`, consultare la [documentazione Java](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementazione di un valutatore personalizzato per i metadati di replica {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

Ad esempio, in questa sezione viene illustrato come creare un valutatore di predicati personalizzato che supporti i dati in base ai metadati di replica:

* `cq:lastReplicated` che memorizza la data dell&#39;ultima azione di replica
* `cq:lastReplicatedBy` che memorizza l&#39;ID dell&#39;utente che ha attivato l&#39;ultima azione di replica
* `cq:lastReplicationAction` che memorizza l&#39;ultima azione di replica (ad esempio Attivazione, Disattivazione)

#### Query dei metadati di replica con gli strumenti di valutazione predefiniti {#querying-replication-metadata-with-default-predicate-evaluators}

La seguente query recupera l&#39;elenco di nodi nel ramo `/content` che sono stati attivati da `admin` dall&#39;inizio dell&#39;anno.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

Questa query è valida ma difficile da leggere e non evidenzia la relazione tra le tre proprietà di replica. L&#39;implementazione di un valutatore di predicati personalizzato ridurrà la complessità e migliorerà la semantica di questa query.

#### Obiettivi {#objectives}

L&#39;obiettivo di `ReplicationPredicateEvaluator` è quello di supportare la query precedente utilizzando la seguente sintassi.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

Il raggruppamento dei predicati di metadati di replica con un valutatore predicato personalizzato consente di creare una query significativa.

#### Aggiornamento delle dipendenze del cielo {#updating-maven-dependencies}

>[!TIP]
>
>La configurazione di nuovi progetti AEM compreso l&#39;utilizzo di maven è spiegata in dettaglio con l&#39;esercitazione WKND.[](develop-wknd-tutorial.md)

Prima devi aggiornare le dipendenze Paradiso del tuo progetto. Il `PredicateEvaluator` fa parte dell&#39;artefatto `cq-search` e quindi deve essere aggiunto al file pom di Maven.

>[!NOTE]
>
>L&#39;ambito della dipendenza `cq-search` è impostato su `provided` perché `cq-search` sarà fornito dal contenitore `OSGi`.

Lo snippet di codice seguente mostra le differenze nel file `pom.xml`, in [formato diff unificato](https://en.wikipedia.org/wiki/Diff#Unified_format)

```text
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

#### Scrittura di ReplicationPredicateEevaluate {#writing-the-replicationpredicateevaluator}

Il progetto `cq-search` contiene la classe astratta `AbstractPredicateEvaluator`. Questo può essere esteso con alcuni passaggi per implementare il proprio valutatore predicato personalizzato `(PredicateEvaluator`).

>[!NOTE]
>
>La procedura seguente spiega come creare un&#39;espressione `Xpath` per filtrare i dati. Un&#39;altra opzione consiste nell&#39;implementare il metodo `includes` che seleziona i dati su base di riga. Per ulteriori informazioni, consultare la [documentazione Java](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29).

1. Creare una nuova classe Java che si estende su `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Annota la tua classe con un `@Component` come gli snippet show in [formato diff unificato](https://en.wikipedia.org/wiki/Diff#Unified_format)

   ```text
   @@ -19,8 +19,11 @@
     */
    package com.adobe.aem.docs.search;
   
   +import org.apache.felix.scr.annotations.Component;
   +import com.day.cq.search.eval.AbstractPredicateEvaluator;
   
   +@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
    public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {
   
    }
   ```

   >[!NOTE]
   >
   >La `factory`deve essere una stringa univoca che inizia con `com.day.cq.search.eval.PredicateEvaluator/`e termina con il nome della `PredicateEvaluator` personalizzata.

   >[!NOTE]
   >
   >Il nome dell&#39; `PredicateEvaluator` è il nome del predicato, utilizzato per la creazione di query.

1. Ignora:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   Nel metodo override si crea un&#39;espressione `Xpath` basata sull&#39;argomento `Predicate` fornito in.

### Esempio di un valutatore predefinito personalizzato per metadati di replica {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

L&#39;implementazione completa di questo `PredicateEvaluator` potrebbe essere simile alla classe seguente.

```java
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```
