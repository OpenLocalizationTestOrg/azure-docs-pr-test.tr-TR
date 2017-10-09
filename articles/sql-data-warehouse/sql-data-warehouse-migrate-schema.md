---
title: "aaaMigrate, şema tooSQL veri ambarı | Microsoft Docs"
description: "Çözümleri geliştirmek için şema tooAzure SQL Data Warehouse geçirmek için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a>Şemalar tooSQL veri ambarına geçirme
SQL şemaları tooSQL veri ambarı geçirmek için yönergeler. 

## <a name="plan-your-schema-migration"></a>Şema geçişinizi planlayın

Geçiş planlıyorsanız hello görmeniz [tablo genel bakışı] [ table overview] toobecome istatistikleri, dağıtım, bölümlendirme ve dizin oluşturma gibi tablo tasarım konuları hakkında bilgi sahibi.  Ayrıca bazı listeler [desteklenmeyen tablo özellikleri] [ unsupported table features] ve bunların geçici çözümleri.

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a>Kullanıcı tanımlı şemaları tooconsolidate veritabanları kullanın

Var olan İş yükünüzün büyük olasılıkla birden fazla veritabanı var. Örneğin, bir SQL Server veri ambarı Hazırlama veritabanı, veri ambarı veritabanı ve bazı veri reyonu veritabanı içerebilir. Bu topolojide, her veritabanı ayrı bir iş yükü ayrı güvenlik ilkeleriyle birlikte çalışır.

Bunun aksine, SQL Data Warehouse hello tüm veri ambarı iş yükü bir veritabanı içinde çalışır. Veritabanı birleştirmeler izin verilmez. Bu nedenle, SQL Data Warehouse hello bir veritabanı içinde depolanan hello veri ambarı toobe tarafından kullanılan bütün tablolar bekliyor.

Kullanıcı tanımlı şemaları tooconsolidate kullanarak mevcut İş yükünüzün bir veritabanına öneririz. Örnekler için bkz: [kullanıcı tanımlı şemaları](sql-data-warehouse-develop-user-defined-schemas.md)

## <a name="use-compatible-data-types"></a>Uyumlu veri türleri kullanın
SQL Data Warehouse ile uyumlu olan veri türleri toobe değiştirin. Desteklenen ve desteklenmeyen veri türlerinin listesi için bkz: [veri türleri][data types]. Bu konuda desteklenmeyen hello türleri için geçici çözümler sunar. Ayrıca bir sorgu SQL veri ambarı'nda desteklenmeyen tooidentify varolan türler sağlar.

## <a name="minimize-row-size"></a>Satır boyutu en aza indir
En iyi performans için tablolarınızı hello satır uzunluğu en aza indirin. Daha kısa satır uzunlukları toobetter performans neden olduğundan, çalışan hello en küçük veri türleri, verileriniz için kullanın. 

Tablo satır genişliğini için PolyBase 1 MB sınırı vardır.  PolyBase ile SQL veri ambarında tooload veri planlıyorsanız, 1 MB'tan az, tablolar toohave en fazla satır genişliğini güncelleştirin. 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a>Merhaba dağıtım seçeneğini belirtin
SQL veri ambarı dağıtılmış bir veritabanı sistemidir. Her tablo dağıtılmış veya hello işlem düğümleri arasında çoğaltılan. Nasıl toodistribute hello veri belirtmenize olanak sağlar. bir tablo seçeneği yoktur. Merhaba çoğaltılan, hepsini, seçimlerdir veya karma dağıtılmış. Her Artıları ve eksileri vardır. Merhaba dağıtım seçeneği belirtmezseniz, SQL Data Warehouse hepsini hello varsayılan olarak kullanın.

- Hepsini hello varsayılandır. Merhaba basit toouse olan ve hello verileri kadar hızlı yükler, ancak sorgu performansını yavaşlatır veri taşıma birleştirmeler gerektirir.
- Her işlem düğümünde Merhaba tablonun kopyasını bir çoğaltılmış depolar. Çoğaltılmış tablolar kullanıcı olduklarından, veri taşıma birleşimler ve Toplamalar için gerektirmez. Bunlar ek depolama alanı gerektirir ve bu nedenle daha küçük tablolar için en iyi çalışır.
- Dağıtılmış karma hello satırları karma işlevi ile tüm hello düğümler arasında dağıtır. Tasarlanmış tooprovide yüksek sorgu performansı büyük tablolarda olduğundan dağıtılmış karma tabloları hello Kalp SQL veri ambarı ' dir. Bu seçenek bazı planlama tooselect hello en iyi sütun hangi toodistribute hello verileri gerektirir. İlk kez hello en iyi sütun hello seçmezseniz, ancak, kolayca hello verileri farklı bir sütun üzerinde yeniden dağıtabilirsiniz. 

toochoose hello her tablo için en iyi dağıtım seçeneği bkz [dağıtılmış tabloları](sql-data-warehouse-tables-distribute.md).


## <a name="next-steps"></a>Sonraki adımlar
Veritabanı şeması tooSQL veri ambarı başarıyla geçirdikten sonra aşağıdaki makaleler hello tooone devam edin:

* [Verilerinizi geçirme][Migrate your data]
* [Kodunuzu geçirme][Migrate your code]

SQL veri ambarı en iyi uygulamalar hakkında daha fazla bilgi için bkz: Merhaba [en iyi uygulamalar] [ best practices] makalesi.

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
