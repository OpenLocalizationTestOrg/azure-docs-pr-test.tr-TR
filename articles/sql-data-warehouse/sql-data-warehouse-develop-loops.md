---
title: "aaaLeverage T-SQL Azure SQL Data Warehouse'da döngü | Microsoft Docs"
description: "Transact-SQL döngüler ve çözümleri geliştirmek için Azure SQL Data Warehouse değiştirerek imleçler için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a>SQL Data warehouse'da döngüler
SQL veri ambarı destekleyen hello [sırada][sırada] art arda deyim blokları yürütmek döngü. Koşullar doğru olduğunda Hello belirtilen sürece veya kadar hello kod özellikle hello kullanarak hello döngü sonlandırır için devam eder `BREAK` anahtar sözcüğü. Döngüler SQL kod içinde tanımlanan imleçler değiştirme için özellikle yararlıdır. Neyse ki, SQL kodda yazılır neredeyse tüm imleçler Merhaba Hızlı İleri, yalnızca çeşitli salt okunurdur. Bu nedenle [sırada] döngüler kendinizi tooreplace bir sahip bulursanız mükemmel bir alternatif olan.

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a>Döngüler yararlanan ve SQL Data Warehouse imleçler değiştirme
Ancak, head ilk girmeden önce kendinize sorun hello Soru: "Bu imleç olabilir yeniden yazılı toouse ayarlama işlemleri göre mi?". Çoğu durumda hello yanıt Evet olacaktır ve genellikle hello en iyi yaklaşımdır. Temel ayarlama işlemi genellikle yinelemeli, satır temelinde bir yaklaşım daha önemli ölçüde daha hızlı gerçekleştirir.

İleri Sarma salt okunur imleçler, döngü yapısı ile kolayca değiştirilebilir. Basit bir örnek aşağıda verilmiştir. Bu kod örneği hello veritabanındaki her tablo için hello istatistiklerini güncelleştirir. Yineleme hello döngü hello tablolarda üzerinden biz tarafından mümkün tooexecute olan her bir komut dizisi.

İlk olarak, bir benzersiz bir satır numarası kullanılan tooidentify hello tek tek deyimleri içeren geçici bir tablo oluşturun:

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

İkinci olarak, hello değişkenleri gerekli tooperform hello döngü başlatılamadı:

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

Şimdi bir yürütme deyimleri döngü birer birer:

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

Son olarak hello ilk adımda oluşturduğunuz hello geçici tablo bırakma

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sırada]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
