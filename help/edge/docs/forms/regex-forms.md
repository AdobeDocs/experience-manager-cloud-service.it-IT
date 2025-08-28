---
title: Espressioni regex di uso comune per convalidare i campi modulo in Edge Delivery Services per AEM Forms
description: Espressioni regex di uso comune per convalidare i campi modulo in Edge Delivery Services per AEM Forms
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 5cfe23bb-155f-4639-b7b7-5edc172ba92a
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '193'
ht-degree: 100%

---

# Espressioni regolari comunemente utilizzate per le convalide

Di seguito sono riportate alcune espressioni regolari utilizzabili per migliorare la convalida dei moduli oltre a quanto offerto dai browser moderni:

## Password sicura

```regex
^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$
```

La password deve contenere almeno 8 caratteri con:

- Lettera minuscola (a-z)
- Lettera maiuscola (A-Z)
- Cifra (0-9)
- Carattere speciale (@$!%*?&amp;)


## Indirizzo e-mail


```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

Nel nome utente e nel nome del dominio sono consentite lettere, numeri e caratteri speciali.


## Numero di telefono (formato USA)

```regex
^\(?([0-9]{3})\)?[-. ]([0-9]{3})[-. ]([0-9]{4})$
```

I numeri di telefono vanno convalidati nel formato (XXX) XXX-XXXX.



## URL

```regex
^(http|https)://.*$
```

L’URL è valido se inizia con http o https.



## Data (AAAA-MM-GG)

```regex
^\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12][0-9]|3[01])$
```

Le date vanno convalidate nel formato AAAA-MM-GG.


## Ora (HH:MM)

```regex
^([01][0-9]|2[0-3]):[0-5][0-9]$
```

Convalida gli orari nel formato HH:MM (formato di 24 ore).


## Codice postale (formato USA)

```regex
^\d{5}(?:[-\ ]\d{4})?$
```

I codici postali statunitensi a 5 cifre vanno convalidati con un trattino e un’estensione a 4 cifre facoltativi.


## Nome utente (alfanumerico e trattino basso)

```regex
^[a-zA-Z0-9_]+$
```

Sono consentiti lettere, numeri e trattini bassi.


## Codice esadecimale del colore

```regex
^#[0-9a-fA-F]{6}$
```

I codici esadecimali del colore vanno convalidati a 6 cifre. Ad esempio #FFFFFF.


## Indirizzo IP

```regex
^(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})$
```

Gli indirizzi IPv4 vanno convalidati.



## Numero di previdenza sociale (formato USA)

```regex
^\d{3}-\d{2}-\d{4}$
```



## Numero carta di credito

```regex
^(?:4[0-9]{12}(?:[0-9]{3})?|[25][1-7][0-9]{14}$
```

I numeri di telefono vanno convalidati nel formato (XXX) XXX-XXXX.



## Numero di telefono (formato USA):

```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

I numeri di telefono vanno convalidati nel formato (XXX) XXX-XXXX.
