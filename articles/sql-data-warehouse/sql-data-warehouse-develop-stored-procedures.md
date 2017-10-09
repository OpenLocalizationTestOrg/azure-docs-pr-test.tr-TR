---
title: "SQL veri ambarı aaaStored yordamlarda | Microsoft Docs"
description: "Saklı yordamlar çözümleri geliştirmek için Azure SQL Data Warehouse'da uygulamak için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a>Saklı yordamlar SQL veri ambarı
SQL veri ambarı SQL Server'da bulunan hello Transact-SQL özelliklerini çoğunu destekler. Daha da önemlisi biz tooleverage toomaximize hello çözümünüzün performansını istediğiniz belirli özellikleri genişletme vardır.

Ancak, toomaintain hello ölçek ve var. SQL veri ambarı performansını ayrıca bazı özellikler ve davranış farklılıkları ve diğerleri desteklenmeyen işlev değildir.

Bu makalede nasıl tooimplement saklı yordamlar SQL Data warehouse'da açıklanmaktadır.

## <a name="introducing-stored-procedures"></a>Saklı yordamlar Tanıtımı
Saklı yordamlar SQL kodunuzu Kapsüllenen harika bir yöntemdir; Bu, hello veri ambarında Kapat tooyour veri depolama. Merhaba kod yönetilebilir birimler halinde kapsülleyerek saklı yordamlar çözümleri modülarize etmek geliştiricilerin yardımcı; kod büyük re-usability kolaylaştırmanın. Her bir saklı yordam parametreleri toomake kabul edebilir bunları bile daha esnektir.

SQL veri ambarı Basitleştirilmiş ve kolaylaştırılmış saklı yordam uygulamasını sağlar. Bu saklı yordam hello sunucusudur hello büyük karşılaştırıldığında fark tooSQL önceden derlenmiş kod değil. Veri ambarları genellikle hello derleme süresi ile daha az endişe duyuyoruz. Merhaba saklı yordamı kodu doğru büyük veri birimlerine karşı çalışırken en iyi duruma getirilmiş emin daha önemlidir. Merhaba toosave saat, dakika ve saniyeleri değil milisaniye hedeftir. Bu nedenle SQL mantığı için kapsayıcı olarak daha yararlı toothink saklı yordamların orantılıdır.     

SQL veri ambarı yürütüldüğünde, saklı yordam hello SQL deyimleri ayrıştırılır, çevrilen ve çalışma zamanında en iyi duruma getirilmiş. Bu işlem sırasında her deyim dağıtılmış sorgular dönüştürülür. Merhaba hello veri karşı gerçekleştirilmeden SQL kodu gönderildi farklı toohello sorgudur.

## <a name="nesting-stored-procedures"></a>İç içe geçme saklı yordamlar
Ne zaman saklı yordamlar diğer saklı yordamlar çağırabilir veya hello iç saklı yordam veya kod çağırma toobe iç içe geçmiş denirse ardından dinamik sql Yürüt.

SQL veri ambarı en fazla 8 iç içe geçme düzeyi destekler. Biraz farklı tooSQL sunucu budur. SQL Server'da Hello iç içe geçirme düzeyi 32'dir.

Merhaba üst düzey saklı yordam çağrısı toonest düzey 1 karşılık gelir.

```sql
EXEC prc_nesting
```
Merhaba depolanan yordamı de başka bir yürütme çağrı yapar sonra bu hello iç içe geçirme düzeyi too2 artırır

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
Ardından Hello ikinci yordam sonra bazı dinamik sql çalıştırırsa bu hello iç içe geçirme düzeyi too3 artırır

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

Not SQL Data Warehouse desteklememektedir@NESTLEVEL. İç içe geçirme düzeyi izini tookeep kendiniz gerekir. Merhaba 8 iç içe geçirme düzeyi sınırı karşılaşır ancak, bunu yaparsanız kodunuzu toore iş gerekir ve ", böylece bu sınırı içinde sığar düzleştirmek" olası değil.

## <a name="insertexecute"></a>EKLE... YÜRÜTME
SQL veri ambarı tooconsume hello sonuç kümesi, INSERT deyimi olan bir saklı yordam izin vermez. Ancak, kullanabileceğiniz alternatif bir yaklaşım yoktur.

Lütfen aşağıdaki makaleye bakın toohello başvurun [geçici tablolara] konusunda bir örnek toodo bu.

## <a name="limitations"></a>Sınırlamalar
SQL veri ambarı'nda uygulanmadı Transact-SQL saklı yordamları bazı yönleri vardır.

Bunlar:

* geçici saklı yordamlar
* numaralandırılmış saklı yordamlar
* genişletilmiş saklı yordamlar
* CLR saklı yordamlar
* şifreleme seçeneği
* çoğaltma seçeneği
* Tablo değerli parametreleri
* salt okunur parametreleri
* varsayılan parametreleri
* yürütme bağlamı
* return deyimi

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].

<!--Image references-->

<!--Article references-->
[geçici tablolara]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
