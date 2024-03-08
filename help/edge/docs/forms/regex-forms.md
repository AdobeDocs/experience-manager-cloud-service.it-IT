---
title: 'Servizi di distribuzione Edge di AEM Forms: espressioni regex comunemente utilizzate per la convalida dei campi modulo'
description: 'Servizi di distribuzione Edge di AEM Forms: espressioni regex comunemente utilizzate per la convalida dei campi modulo'
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 4%

---


# Espressioni regex di uso comune per le convalide

Di seguito sono riportate alcune espressioni regolari utilizzabili per migliorare la convalida dei moduli oltre le offerte dei browser moderni:

## Password sicura

```regex
^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$
```

Assicura almeno 8 caratteri con:

* Lettera minuscola (a-z)
* Lettera maiuscola (A-Z)
* Cifra (0-9)
* Carattere speciale (@$!%*?)


## Indirizzo e-mail


```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

Consente lettere, numeri e caratteri speciali nel nome utente e nel nome di dominio.


## Numero di telefono (formato Stati Uniti)

```regex
^\(?([0-9]{3})\)?[-. ]([0-9]{3})[-. ]([0-9]{4})$
```

Convalida i numeri di telefono nel formato (XXX) XXX-XXXX.



## URL

```regex
^(http|https)://.*$
```

Assicura un URL valido che inizia con http o https.



## Data (AAAA-MM-GG)

```regex
^\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12][0-9]|3[01])$
```

Convalida le date nel formato AAAA-MM-GG.


## Ora (HH:MM)

```regex
^([01][0-9]|2[0-3]):[0-5][0-9]$
```

Convalida gli orari nel formato HH:MM (formato 24 ore).


## Codice postale (formato Stati Uniti)

```regex
^\d{5}(?:[-\ ]\d{4})?$
```

Convalida i codici postali statunitensi a 5 cifre con un trattino e un&#39;estensione a 4 cifre facoltativi.


## Nome utente (alfanumerico e trattino basso)

```regex
^[a-zA-Z0-9_]+$
```

Consente lettere, numeri e trattini bassi.


## Codice esadecimale colore

```regex
^#[0-9a-fA-F]{6}$
```

Convalida i codici colore esadecimali a 6 cifre. Ad esempio, #FFFFFF.


## Indirizzo IP

```regex
^(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})$
```

Convalida gli indirizzi IPv4.



## Numero di previdenza sociale (formato Stati Uniti)

```regex
^\d{3}-\d{2}-\d{4}$
```



## Numero carta di credito

```regex
^(?:4[0-9]{12}(?:[0-9]{3})?|[25][1-7][0-9]{14}$
```

Convalida i numeri di telefono nel formato (XXX) XXX-XXXX.



## Numero di telefono (formato Stati Uniti):

```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

Convalida i numeri di telefono nel formato (XXX) XXX-XXXX.
