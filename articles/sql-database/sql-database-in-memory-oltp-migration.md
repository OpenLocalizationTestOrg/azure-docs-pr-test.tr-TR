---
title: "aaaIn bellek içi OLTP artırır SQL işlemlerinin perf | Microsoft Docs"
description: "Varolan bir SQL veritabanında adopt bellek içi OLTP tooimprove işlem performansı."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>Kullanım bellek içi OLTP tooimprove SQL veritabanında, uygulama performansı
[Bellek içi OLTP](sql-database-in-memory.md) kullanılan tooimprove hello performansını işlem, veri alımı ve geçici veri senaryoları olabilir [Premium](sql-database-service-tiers.md) artırma olmadan Azure SQL veritabanları hello fiyatlandırma katmanı. 

> [!NOTE] 
> Bilgi nasıl [çekirdek % 70'sql Database tarafından DTU düşürürken anahtar veritabanının iş yükü Katlar](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)


Mevcut veritabanını bu adımları tooadopt bellek içi OLTP izleyin.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>1. adım: bir Premium veritabanı kullandığınızdan emin olun
Bellek içi OLTP yalnızca Premium veritabanlarında desteklenir. Bellek içi hello sonucudur 1 döndürülürse desteklenir (0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP* anlamına gelir *aşırı işlem işleme*



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>2. adım: nesneleri toomigrate tooIn-belleği tanımlayan OLTP
SSMS içeren bir **işlem Performans Analizi genel bakış** etkin bir iş yükü olan bir veritabanına karşı çalıştırabilirsiniz rapor. Merhaba raporu, tablolar ve geçiş adaylar saklı yordamlar tanımlar tooIn bellek içi OLTP.

SSMS toogenerate hello raporu:

* Merhaba, **Nesne Gezgini**, veritabanı düğümünü sağ tıklatın.
* Tıklatın **raporları** > **standart raporları** > **işlem Performans Analizi genel bakış**.

Daha fazla bilgi için bkz: [belirleme bir tablo veya saklı yordam gereken olması bağlantı noktalı tooIn bellek içi OLTP](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>3. adım: karşılaştırılabilir test veritabanı oluşturma
Veritabanınızı Hello rapor gösterir varsayalım olmaktan için yararlı bir tablo tooa bellek için iyileştirilmiş tablo dönüştürülen. Test ederek tooconfirm hello göstergesi ilk sınamanızı öneririz.

Üretim veritabanınız test kopyasını gerekir. Merhaba test veritabanı olmalıdır hello aynı katmanı düzeyini üretim veritabanınız olarak hizmet.

Test, tooease test veritabanınızı gibi ince ayar:

1. SSMS kullanarak toohello test veritabanı bağlanın.
2. tooavoid gerek WITH (SNAPSHOT) seçeneği sorgularda Merhaba, hello veritabanı seçeneği T-SQL deyimi aşağıdaki hello gösterilen şekilde ayarlayın:
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>4. adım: tabloları geçirme
Oluşturmalı ve bellek için iyileştirilmiş kopyasını doldurmak Merhaba tablonun tootest istiyor. Kullanarak oluşturabilirsiniz:

* Merhaba SSMS kullanışlı belleği en iyi duruma getirme sihirbazında.
* El ile T-SQL.

#### <a name="memory-optimization-wizard-in-ssms"></a>Belleği en iyi duruma getirme Sihirbazı'nda SSMS
toouse bu geçiş seçeneği:

1. Toohello test veritabanı SSMS ile bağlanma.
2. Merhaba, **Object Explorer**hello tabloyu sağ tıklatın ve ardından **belleği en iyi duruma getirme Danışmanı**.
   
   * Merhaba **tablo bellek iyileştirici Danışmanı** Sihirbazı görüntülenir.
3. Başlangıç Sihirbazı'nda tıklatın **geçiş doğrulama** (veya hello **sonraki** düğmesi) Merhaba tablonun herhangi varsa toosee desteklenmeyen bellek için iyileştirilmiş tablolarda desteklenmeyen özellikler. Daha fazla bilgi için bkz.
   
   * Merhaba *belleği en iyi duruma getirme denetim listesi* içinde [belleği en iyi duruma getirme Danışmanı](http://msdn.microsoft.com/library/dn284308.aspx).
   * [Bellek içi OLTP tarafından desteklenmeyen transact-SQL yapıları](http://msdn.microsoft.com/library/dn246937.aspx).
   * [Geçirme tooIn bellek içi OLTP](http://msdn.microsoft.com/library/dn247639.aspx).
4. Merhaba tablonun desteklenmeyen özellikleri yok varsa hello Danışmanı hello gerçek şema ve veri geçişi sizin için gerçekleştirebilir.

#### <a name="manual-t-sql"></a>El ile T-SQL
toouse bu geçiş seçeneği:

1. Tooyour test veritabanı SSMS (veya benzer bir yardımcı programını) kullanarak bağlanın.
2. Merhaba tam T-SQL komut dosyası, tablo ve dizinlerini edinin.
   
   * SSMS, tablo düğümünü sağ tıklatın.
   * Tıklatın **komut tablo olarak** > **için oluşturun** > **yeni sorgu penceresinde**.
3. WITH Hello komut penceresinde ekleyin (memory_optımızed = ON) toohello CREATE TABLE deyimi.
4. Bir kümelenmiş dizin ise tooNONCLUSTERED değiştirin.
5. Merhaba var olan tablo SP_RENAME kullanarak yeniden adlandırın.
6. Düzenlenen CREATE TABLE kodunuzu çalıştırarak Hello yeni bellek için iyileştirilmiş Merhaba tablonun kopyasını oluşturun.
7. Merhaba veri tooyour bellek için iyileştirilmiş Tablo Ekle kullanarak Kopyala... SEÇİN * İÇİNE:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>(İsteğe bağlı) 5. adım: saklı yordamları geçirme
Merhaba bellek içi özelliği, Gelişmiş performans için bir saklı yordam de değiştirebilirsiniz.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Yerel koda derlenmiş saklı yordamlar ile ilgili önemli noktalar
Yerel koda derlenmiş bir saklı yordam aşağıdaki seçenekler, T-SQL WITH yan tümcesi'hello olması gerekir:

* NATIVE_COMPILATION ÖĞESİNİ
* Şemaya Bağlama: saklı yordam hello anlamı tabloların sütun tanımlarını hello saklı yordamı bırakma sürece hello saklı yordamı etkileyecek herhangi bir şekilde değiştirilmiş sahip olamaz.

Yerel bir modül biri büyük kullanmalısınız [ATOMİK bloklar](http://msdn.microsoft.com/library/dn452281.aspx) işlem yönetimi. Herhangi bir rol veya geri alma işlemi için açık BEGIN TRANSACTION yok. Kodunuzu bir iş kuralı ihlal algılarsa, hello atomik blok sonlandırabilir bir [THROW](http://msdn.microsoft.com/library/ee677615.aspx) deyimi.

### <a name="typical-create-procedure-for-natively-compiled"></a>İçin tipik CREATE PROCEDURE yerel koda derlenmiş
Genellikle hello T-SQL toocreate yerel koda derlenmiş bir saklı yordam benzer toohello şablonu aşağıdaki gibidir:

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* Merhaba TRANSACTION_ISOLATION_LEVEL hello en yaygın değeri hello yerel koda derlenmiş saklı yordamı anlık görüntüsüdür. Ancak, bir alt kümesini hello diğer değerleri de desteklenir:
  
  * YİNELENEBİLİR OKUMA
  * SERİ HALE GETİRİLEBİLİR
* Merhaba dil değerini hello sys.languages görünümünde mevcut olması gerekir.

### <a name="how-toomigrate-a-stored-procedure"></a>Nasıl toomigrate bir saklı yordam
Merhaba geçiş adımları şunlardır:

1. Merhaba CREATE PROCEDURE betik toohello normal yorumlanan saklı yordam edinin.
2. Kendi üstbilgi toomatch hello önceki şablonu yeniden yazın.
3. Merhaba saklı yordamı T-SQL kodunu yerel koda derlenmiş saklı yordamlar için desteklenmeyen herhangi bir özellik kullanıp kullanmadığını onaylaması. Geçici Çözümler gerekirse uygulayın.
   
   * Ayrıntılar için bkz: [yerel olarak depolanan yordamlar derlenmiş geçiş sorunları](http://msdn.microsoft.com/library/dn296678.aspx).
4. Merhaba eski saklı yordam SP_RENAME kullanarak yeniden adlandırın. Veya yalnızca BIRAKILAMIYOR.
5. Düzenlenen oluşturma yordamı T-SQL betiğini çalıştırın.

## <a name="step-6-run-your-workload-in-test"></a>6. adım: İş yükünüzün testi çalıştırın.
Test veritabanınızdaki üretim veritabanınız çalıştıran benzer toohello iş yükü olan bir iş yükü çalıştırın. Bu, tabloları ve saklı yordamlar için hello bellek içi özelliği kullanımınız tarafından elde hello performans kazancı ortaya çıkarır.

Merhaba iş yükünün önemli öznitelikleri şunlardır:

* Eşzamanlı bağlantı sayısı.
* Okuma/yazma oranı.

tootailor ve çalışma hello test iş yükü, göz önünde bulundurun gösterilen hello kullanışlı ostress.exe aracını kullanarak [burada](sql-database-in-memory.md).

hello testinizi çalıştırmak toominimize ağ gecikmesini hello veritabanının bulunduğu aynı Azure coğrafi bölge.

## <a name="step-7-post-implementation-monitoring"></a>7. adım: Uygulama sonrası izleme
Bellek içi uygulamalarınızda üretim Hello performans etkisini izleme göz önünde bulundurun:

* [Bellek içi depolama izleme](sql-database-in-memory-oltp-monitoring.md).
* [Dinamik yönetim görünümlerini kullanarak Azure SQL Database’i izleme](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>İlgili bağlantılar
* [Bellek içi OLTP (bellek içi iyileştirme)](http://msdn.microsoft.com/library/dn133186.aspx)
* [Giriş tooNatively derlenmiş saklı yordamlar](http://msdn.microsoft.com/library/dn133184.aspx)
* [Belleği en iyi duruma getirme Danışmanı](http://msdn.microsoft.com/library/dn284308.aspx)

