---
title: "SQL veri ambarı aaaAssign değişkenleri | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse Transact-SQL değişkenleri atamak için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>SQL veri ambarı değişkenlerde atayın
SQL veri ambarı değişkenlerde hello kullanılarak ayarlanır `DECLARE` deyimi veya hello `SET` deyimi.

Tüm hello aşağıdaki mükemmel geçerli yolları tooset bir değişken değeri şunlardır:

## <a name="setting-variables-with-declare"></a>DECLARE değişkenlerle ayarlama
DECLARE değişkenlerle başlatılıyor hello en esnek şekilde tooset SQL Data warehouse'da bir değişken değeri biridir.

```sql
DECLARE @v  int = 0
;
```

Bir kerede bir değişken birden çok DECLARE tooset de kullanabilirsiniz. Kullanamazsınız `SELECT` veya `UPDATE` toodo bu:

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

İnitialise ve bir değişkeni hello kullanın aynı DECLARE deyimi. tooillustrate hello noktası hello örnek aşağıdaki **değil** izin @p1 hem başlatılır ve hello kullanılan aynı DECLARE deyimi. Bu bir hatayla sonuçlanır.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>SET değerleri ayarlama
Kümesi, tek bir değişken ayarlamak için yaygın bir yöntemdir.

Tüm hello örneklere kümesine sahip bir değişken ayarlama geçerli yöntemlerdir:

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

KÜMESİYLE aynı anda yalnızca bir değişken ayarlayabilirsiniz. Ancak, yukarıda görüldüğü gibi bileşik işleçler kabul edilebilir değildir.

## <a name="limitations"></a>Sınırlamalar
Değişken ataması için SELECT veya UPDATE kullanamazsınız.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
