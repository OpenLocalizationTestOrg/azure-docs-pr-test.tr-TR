---
title: SQL Data warehouse'da aaaTransactions | Microsoft Docs
description: "Çözümleri geliştirme için Azure SQL Data Warehouse'da işlemleri uygulamak için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>SQL veri ambarı işlemleri
Beklediğiniz gibi SQL veri ambarı işlemleri hello veri ambarı iş yükü bir parçası olarak destekler. Ancak, SQL Data Warehouse tooensure hello performansını karşılaştırılan tooSQL sunucu bazı özellikleri sınırlıdır ölçekte korunur. Bu makalede hello farklar vurgular ve listeleri başkalarının hello. 

## <a name="transaction-isolation-levels"></a>İşlem yalıtım düzeyi
SQL veri ambarı ACID işlemlerini uygular. Bununla birlikte, hello yalıtım hello işlem desteği, çok sınırlıdır`READ UNCOMMITTED` ve bu değiştirilemez. Bu sizin için önemliyse tooprevent kirli verilerini okur kodlama yöntemleri sayısı uygulayabilirsiniz. Merhaba en popüler yöntemleri hem CTAS hem de (genellikle kayan pencere düzenini hello olarak bilinir) tabloda bölüm değiştirme yararlanan tooprevent kullanıcıların hala hazırlanan veri sorgulama. Filtre öncesi hello verileri de popüler bir yaklaşım olduğu görünümleri.  

## <a name="transaction-size"></a>İşlem boyutu
Bir tek veri değişikliği işlem boyutu sınırlıdır. Merhaba sınır Bugün "dağıtım" uygulanır. Bu nedenle, hello toplam ayırma hello dağıtım sayısına göre hello sınırı çarpılmasıyla hesaplanır. tooapproximate hello satır sayısının üst sınırını hello işlemde hello dağıtım cap hello tarafından her satırın toplam boyutu bölün. Değişken uzunlukta sütunlar için hello en büyük boyutu kullanmak yerine bir ortalama sütun uzunluğu alma göz önünde bulundurun.

Merhaba aşağıda hello tablosundaki aşağıdaki varsayımlar yapılmıştır:

* Bir dağılmış verilerinizin oluştu 
* Merhaba ortalama satır uzunluğu 250 bayttır

| [DWU][DWU] | Dağıtım (GiB) cap | Dağıtımların sayısı | En fazla işlem boyutu (GiB) | # Dağıtım başına satır | İşlem başına en fazla satır |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4,000,000 |240,000,000 |
| DW200 |1.5 |60 |90 |6,000,000 |360,000,000 |
| DW300 |2.25 |60 |135 |9,000,000 |540,000,000 |
| DW400 |3 |60 |180 |12,000,000 |720,000,000 |
| DW500 |3.75 |60 |225 |15,000,000 |900,000,000 |
| DW600 |4.5 |60 |270 |18,000,000 |1,080,000,000 |
| DW1000 |7.5 |60 |450 |30,000,000 |1,800,000,000 |
| DW1200 |9 |60 |540 |36,000,000 |2,160,000,000 |
| DW1500 |11.25 |60 |675 |45,000,000 |2,700,000,000 |
| DW2000 |15 |60 |900 |60,000,000 |3,600,000,000 |
| DW3000 |22.5 |60 |1,350 |90,000,000 |5,400,000,000 |
| DW6000 |45 |60 |2,700 |180,000,000 |10,800,000,000 |

Merhaba işlem boyut sınırı, işlem veya işlem uygulanır. Tüm eşzamanlı işlemler arasında uygulanmaz. Bu nedenle her bir işlem olduğundan toowrite bu miktarda veri toohello günlük izin verilir. 

toooptimize ve hello toohello günlüğüne yazılan veri miktarını en aza toohello başvurun [işlemleri en iyi uygulamalar] [ Transactions best practices] makalesi.

> [!WARNING]
> Hello için KARMA işlem boyutu yalnızca elde edilebilir veya dağıtılmış ROUND_ROBIN tabloları, burada hello yayılan veri hello maksimum bile. Merhaba işlem toohello dağıtımları çarpık bir şekilde veri yazma, hello sınırı önceki toohello maksimum hareket boyut üst sınırına büyük olasılıkla toobe yoktur.
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>İşlem durumu
SQL veri ambarı hello XACT_STATE() işlevi tooreport hello değerini -2 kullanarak başarısız bir işlem kullanır. Bu hello işlem başarısız oldu ve yalnızca geri almak için işaretlenmiş anlamına gelir

> [!NOTE]
> Merhaba -2 hello XACT_STATE işlevi toodenote başarısız işlem temsil farklı bir davranış tooSQL sunucusu kullanın. SQL Server hello -1 değeri toorepresent kaydedilemez bir işlem kullanır. SQL Server, olarak kaydedilemez işaretlenmiş toobe sahip bir işlemin içindeki bazı hatalar dayanabilir. Örneğin `SELECT 1/0` hataya neden, ancak bir işlem kaydedilemez bir duruma zorla sağlamaz. SQL Server hello kaydedilemez işlemde de okuma izin verir. Ancak, SQL Data Warehouse, bunun izin vermez. Merhaba -2 durumu otomatik olarak girer ve mümkün toomake olmaz bir SQL Data Warehouse işlem içinde bir hata oluşursa, hello deyimi geri kadar daha fazla deyimleri seçin. Bu nedenle, XACT_STATE() gibi kullanıyorsa, uygulama kodu toosee toomake kod değişikliklerini gerekebilir önemli toocheck olur.
> 
> 

Örneğin, SQL Server'da şuna benzer bir işlem görebilirsiniz:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Ardından yukarıda olduğu gibi kodunuzu değiştirmeden bırakırsanız hello aşağıdaki hata iletisini alırsınız:

Msg 111233, Level 16, State 1, 1 satır 111233; hello işlem iptal ve bekleyen tüm değişiklikleri geri alındığından geçerli. Neden: Bir işlemi yalnızca geri alma durumunda açıkça DDL, DML veya SELECT deyimi önce geri alınmadı.

Ayrıca hello çıktı hello ERROR_ * işlevlerin almazsınız.

SQL veri ambarı'nda hello kod biraz değiştirilmiş toobe gerekir:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Merhaba, şimdi davranış gözlenir bekleniyordu. Merhaba hata hello işlemde yönetilir ve beklendiği gibi hello ERROR_ * işlevleri değerler sağlayın.

Değişen tek şey, hello `ROLLBACK` hello hello hata bilgilerinin hello okumadan önce hello işleme toohappen sahipti. `CATCH` bloğu.

## <a name="errorline-function"></a>Error_Line() işlevi
Ayrıca, SQL Data Warehouse uygulama ya da hello ERROR_LINE() işlevini destekler olduğunu dikkate değerdir. Bu, kodunuzda varsa tooremove gerekir, toobe SQL Data Warehouse ile uyumlu. Sorgu etiketleri, kodunuzda, bunun yerine tooimplement eşdeğer işlevini kullanın. Lütfen toohello bakın [etiket] [ LABEL] bu özellik hakkında daha fazla ayrıntı için makale.

## <a name="using-throw-and-raiserror"></a>THROW ve RAISERROR kullanma
THROW SQL Data warehouse'da özel durumlarını oluşturma için daha modern uygulama hello ancak RAISERROR de desteklenen değildir. Dikkat toohowever ödeme değer olan bazı farklar vardır.

* Kullanıcı tanımlı hata iletileri sayı hello THROW 100.000 150.000 aralığının olamaz
* RAISERROR hata iletileri 50.000 düzeltilen
* Sistem iletilerinde kullanımı desteklenmiyor

## <a name="limitiations"></a>Limitiations
SQL veri ambarı tootransactions ilgili diğer bazı kısıtlamalar sahip.

Bunlar aşağıdaki gibidir:

* Dağıtılmış işlem
* İzin verilen hiçbir iç içe geçmiş işlemler
* İzin verilen noktaları kaydetme
* Adlandırılmış işlem
* İşaretli işlem
* DDL gibi desteği `CREATE TABLE` işlem içinde bir kullanıcı tanımlı

## <a name="next-steps"></a>Sonraki adımlar
işlemler, en iyi duruma getirme hakkında daha fazla toolearn bkz [işlemleri en iyi uygulamalar][Transactions best practices].  toolearn diğer SQL Data Warehouse en iyi uygulamalar hakkında bkz [SQL veri ambarı en iyi yöntemler][SQL Data Warehouse best practices].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
