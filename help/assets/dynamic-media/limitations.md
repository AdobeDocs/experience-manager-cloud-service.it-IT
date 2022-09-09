---
title: Limiti di Dynamic Media
description: Scopri le best practice e i limiti applicati quando crei un set di immagini o un set 360 gradi o carichi un PDF. Scopri anche le combinazioni non supportate di browser web e sistemi operativi per visualizzatori Dynamic Media.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: 479349d2dad841a782519de3302993ea2a9f5162
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 5%

---

# Limitazioni di Dynamic Media

Le sezioni seguenti descrivono le limitazioni in Dynamic Media.

Questo argomento include le sezioni seguenti:

* [Best practice e limiti applicati da Dynamic Media sui tipi di risorse](#best-practice-enforced-limits)
* [Combinazioni di browser web e sistemi operativi non supportati per visualizzatori Dynamic Media](#unsupported-browser-os)

## Best practice e limiti applicati da Dynamic Media sui tipi di risorse {#best-practice-enforced-limits}

Quando crei un set 360 gradi o un set di immagini o carichi PDF per l’estrazione della pagina, Adobe consiglia le seguenti best practice e applica i seguenti limiti:

| Risorsa - Tipo limite | Best practice | Limite imposto | Modifica del limite il 31 dicembre 2022 |
| --- | --- | --- | --- |
| **Immagine** - Numero di ritagli avanzati per immagine | 5 | 100 | 20 |
| **Tutti i set** - Numero di risorse duplicate per set | Nessun duplicato | 20 | Non applicabile |
| **Tutti i set** - Numero massimo di risorse per set | 5-10 immagini per set | 1000 | Non applicabile |
| **Set 360 gradi** - Numero massimo di righe/colonne per set 2D | 12-18 immagini per set | 1000 | Non applicabile |
| **PDF** - Numero massimo di pagine per un PDF da considerare per l’estrazione |  | 5000 (per nuovi caricamenti) | 100 (per tutti i PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Combinazioni di browser web e sistemi operativi non supportati per visualizzatori Dynamic Media {#unsupported-browser-os}

I visualizzatori Dynamic Media non supportano le seguenti combinazioni di browser Web e sistemi operativi.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Aggiornamento di Internet Explorer 11 + Windows Phone 8.1
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## Fine del supporto per TLS 1.0 e 1.1 {#tls}

<!-- CQDOC-19433 -->

A partire dal 30 settembre 2022, i visualizzatori Adobe Dynamic Media termineranno il supporto per i seguenti elementi:

* TLS (Transport Layer Security) 1.0 e 1.1
* Le seguenti crittografie deboli in TLS 1.2:
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_RSA_WITH_AES_256_GCM_SHA384`
   * `TLS_RSA_WITH_AES_256_CBC_SHA256`
   * `TLS_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_AES_128_GCM_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
   * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

