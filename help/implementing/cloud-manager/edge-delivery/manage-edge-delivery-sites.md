---
title: Gestire siti Edge Delivery in Cloud Manager
description: Scopri come aggiungere una configurazione CDN a un sito Edge Delivery o eliminare un sito Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Gestire il sito Edge Delivery in Cloud Manager {#manage-edge-delivery-sites}

Scopri come gestire i siti Edge Delivery in Cloud Manager aggiungendo una configurazione CDN a un sito esistente. In alternativa, elimina un sito Edge Delivery.

## Aggiungere una configurazione CDN a un sito Edge Delivery esistente {#add-cdn-to-edge-delivery-site}

Vedere [Aggiungere una configurazione CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Rinominare un sito Edge Delivery (#rename-edge-delivery-site)

In Adobe Cloud Manager, potrebbe essere utile rinominare un sito Edge Delivery per diversi motivi:

* **Chiarezza e organizzazione**: per descrivere meglio lo scopo del sito o l&#39;ambiente associato (ad esempio, produzione, gestione temporanea).
* **Non creare confusione**: se sono in uso più siti, rinominarli consente di distinguerli facilmente, riducendo la possibilità di applicare configurazioni o aggiornamenti al sito errato.
* **Standardizzazione**: seguire una convenzione di denominazione coerente che sia in linea con le linee guida della propria organizzazione per semplificare la gestione e il controllo.

**Per rinominare un sito Edge Delivery:**

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma con Edge Delivery Services configurati, in cui si desidera aggiungere un sito Edge Delivery.
1. Effettuare una delle seguenti operazioni:

   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Nella tabella del sito Edge Delivery, fai clic sui puntini di sospensione alla fine di una riga di cui desideri rinominare il sito.
Fare clic su **Rinomina**.
   * Nell’angolo in alto a sinistra della pagina, fai clic sull’icona dell’hamburger per visualizzare il menu di navigazione a sinistra. Nell&#39;intestazione **Services** fare clic su **Siti Edge Delivery**.
Nella tabella del sito Edge Delivery, fai clic sui puntini di sospensione alla fine di una riga di cui desideri rinominare il sito. Fare clic su **Rinomina**.

1. Nella finestra di dialogo **Modifica sito Edge Delivery** immettere il nuovo nome del sito nel campo di testo **Nome sito**.

1. Fai clic su **Modifica**.

## Eliminare un sito Edge Delivery {#delete-edge-delivery-site}

Se elimini un sito Edge Delivery Services, vengono rimosse anche le configurazioni CDN associate. Questa azione interrompe la connessione tra i domini personalizzati e il sito. Per ulteriori dettagli, consulta Configurazioni CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Per eliminare un sito Edge Delivery:**

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma con Edge Delivery Services configurati, in cui si desidera aggiungere un sito Edge Delivery.
1. Effettuare una delle seguenti operazioni:

   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Nella tabella del sito di Edge Delivery, fai clic sui puntini di sospensione alla fine di una riga di cui desideri rimuovere il sito.
Fai clic su **Elimina**, quindi fai di nuovo clic su **Elimina** per confermare la rimozione del sito.

     ![Aggiungi sito Edge Delivery dalla scheda Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * Nell’angolo in alto a sinistra della pagina, fai clic sull’icona dell’hamburger per visualizzare il menu di navigazione a sinistra. Nell&#39;intestazione **Services** fare clic su **Siti Edge Delivery**.
Nella tabella del sito di Edge Delivery, fai clic sui puntini di sospensione alla fine di una riga di cui desideri rimuovere il sito. Fai clic su **Elimina**, quindi fai di nuovo clic su **Elimina** per confermare la rimozione del sito.


     ![Aggiungi sito Edge Delivery dal pulsante Siti Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)