---
title: Implementazione di un valutatore del predicato personalizzato per il Generatore di query
description: Query Builder in AEM offre un modo semplice e personalizzabile per eseguire query sull’archivio dei contenuti
translation-type: tm+mt
source-git-commit: 6b754a866be7979984d613b95a6137104be05399
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# Implementazione di un valutatore del predicato personalizzato per il Query Builder {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

Questo documento descrive come estendere il [Generatore di query](query-builder-api.md) implementando un valutatore di predicati personalizzato.

## Panoramica {#overview}

Il [Query Builder](query-builder-api.md) offre un modo semplice per eseguire query sull&#39;archivio dei contenuti. AEM viene fornito con [un set di valutatori predicati](#query-builder-predicates.md) che ti aiutano a eseguire query dei dati.

Tuttavia, potrebbe essere utile semplificare le query implementando un valutatore di predicati personalizzato che nasconde una certa complessità e garantisce una semantica migliore.

Un predicato personalizzato potrebbe anche eseguire altre operazioni non direttamente possibili con XPath, ad esempio:

* Query dei dati da un altro servizio
* Filtri personalizzati basati su un calcolo

>[!NOTE]
>
>Quando si implementa un predicato personalizzato, è necessario considerare i problemi di prestazioni.

>[!TIP]
>
>Puoi trovare esempi di query nel documento [Query Builder](query-builder-api.md) .

>[!TIP]
>
>Puoi trovare il codice di questa pagina su GitHub
>
>* [Apri il progetto aem-search-custom-predicate-valutator su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)


>[!NOTE]
>
>Questo codice collegato su GitHub e i frammenti di codice in questo documento sono forniti solo a scopo dimostrativo.

### Predicatore valutatore in dettaglio {#predicate-evaluator-in-detail}

Un valutatore predicato gestisce la valutazione di alcuni predicati, che sono i vincoli di definizione di una query.

Mappa un vincolo di ricerca di livello superiore (ad esempio `width>200`) a una query JCR specifica che si adatta al modello di contenuto effettivo (ad esempio `metadata/@width > 200`). Oppure può filtrare manualmente i nodi e controllarne i vincoli.

>[!TIP]
>
>Per ulteriori informazioni sul `PredicateEvaluator` e sul pacchetto `com.day.cq.search`, consulta la [documentazione Java](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementazione di un valutatore del predicato personalizzato per i metadati di replica {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

Ad esempio, in questa sezione viene descritto come creare un valutatore di predicati personalizzato per aiutare i dati in base ai metadati di replica:

* `cq:lastReplicated` che memorizza la data dell&#39;ultima azione di replica
* `cq:lastReplicatedBy` che memorizza l&#39;id dell&#39;utente che ha attivato l&#39;ultima azione di replica
* `cq:lastReplicationAction` che memorizza l’ultima azione di replica (ad esempio Attivazione, Disattivazione)

#### Query dei metadati di replica con valutatori predefiniti {#querying-replication-metadata-with-default-predicate-evaluators}

La seguente query recupera l’elenco dei nodi nel ramo `/content` che sono stati attivati da `admin` dall’inizio dell’anno.

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

Questa query è valida ma difficile da leggere e non evidenzia la relazione tra le tre proprietà di replica. L’implementazione di un valutatore di predicati personalizzato ridurrà la complessità e migliorerà la semantica di questa query.

#### Obiettivi {#objectives}

L&#39;obiettivo di `ReplicationPredicateEvaluator` è quello di supportare la query di cui sopra utilizzando la seguente sintassi.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

Il raggruppamento dei predicati dei metadati di replica con un valutatore predicato personalizzato consente di creare una query significativa.

#### Aggiornamento delle dipendenze Maven {#updating-maven-dependencies}

>[!TIP]
>
>L&#39;impostazione dei nuovi progetti AEM compreso l&#39;utilizzo di maven è spiegata in dettaglio da [l&#39;esercitazione WKND.](develop-wknd-tutorial.md)

Prima devi aggiornare le dipendenze Maven del progetto. L’ `PredicateEvaluator` fa parte dell’artefatto `cq-search` in modo che debba essere aggiunto al file pom Maven.

>[!NOTE]
>
>L’ambito della dipendenza `cq-search` è impostato su `provided` perché `cq-search` verrà fornito dal contenitore `OSGi`.

Il frammento seguente mostra le differenze nel file `pom.xml`, in [formato diff unificato](https://en.wikipedia.org/wiki/Diff#Unified_format)

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

#### Scrittura di ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

Il progetto `cq-search` contiene la classe astratta `AbstractPredicateEvaluator`. Questo può essere esteso con alcuni passaggi per implementare un valutatore predicato personalizzato `(PredicateEvaluator`).

>[!NOTE]
>
>La procedura seguente spiega come creare un&#39;espressione `Xpath` per filtrare i dati. Un&#39;altra opzione consiste nell&#39;implementare il metodo `includes` che seleziona i dati su base di riga. Per ulteriori informazioni, consulta la [documentazione Java](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/PredicateEvaluator.html) .

1. Crea una nuova classe Java che estende `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Annota la classe con un `@Component` come mostrato nello snippet in [formato diff unificato](https://en.wikipedia.org/wiki/Diff#Unified_format)

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
   >Il nome della `PredicateEvaluator` è il nome del predicato, utilizzato durante la creazione di query.

1. Sostituisci:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   Nel metodo override si genera un&#39;espressione `Xpath` basata su `Predicate` indicato nell&#39;argomento.

### Esempio di un valutatore di predicati personalizzato per metadati di replica {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

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
