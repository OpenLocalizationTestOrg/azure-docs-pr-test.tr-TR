---
title: aaaUse etiketler SQL Data Warehouse tooinstrument sorgularda | Microsoft Docs
description: "Kullanımı hakkında ipuçları çözümleri geliştirmek için Azure SQL Data Warehouse tooinstrument sorgularda etiketler."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>SQL veri ambarı'nda etiketleri tooinstrument sorgularını kullan
SQL veri ambarı sorgusu etiketleri adlı bir kavram destekler. Herhangi bir derinliğe şimdi geçmeden önce bir bir örneğe bakın:

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

Bu son satırında hello dize 'My sorgu etiketi' toohello sorgu etiketler. Merhaba etiket-Dmv'leri hello sorgulayabilir olduğu gibi bu seçenek özellikle yararlıdır. Bu bize mekanizması tootrack sorun sorguları aşağı sağlar ve ayrıca toohelp ETL Çalıştır ilerlemeyi tanımlayın.

İyi bir adlandırma kuralı gerçekten burada yardımcı olur. Örneğin şuna benzer ' proje: yordamı: DEYİMİ: Açıklama ' hello sorgu kaynak denetiminde tüm hello kodu arasında tanımlamak toouniquely yardımcı.

toosearch kullanan sorgu aşağıdaki hello kullanabileceğiniz etiketine göre dinamik yönetim görünümlerini hello:

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> Sorgulanırken köşeli veya çift tırnak hello word etiket kaydırma gereklidir. Etiket ayrılmış bir sözcük ve onu Sınırlanmamış bir hata neden olur.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
