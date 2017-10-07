---
title: "aaaElastic veritabanı araçları sözlüğü | Microsoft Docs"
description: "Esnek veritabanı araçları için kullanılan terimler açıklaması"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a>Esnek veritabanı araçlarını sözlüğü
Merhaba aşağıdaki terimler hello için tanımlanan [esnek veritabanı araçlarını](sql-database-elastic-scale-introduction.md), Azure SQL veritabanı özelliğidir. Merhaba kullanılan toomanage araçlardır [parça eşlemeleri](sql-database-elastic-scale-shard-map-management.md)ve hello dahil [istemci Kitaplığı](sql-database-elastic-database-client-library.md), hello [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md), [esnek havuzlar](sql-database-elastic-pool.md), ve [sorguları](sql-database-elastic-query-overview.md). 

Aşağıdaki terimler kullanılır [esnek veritabanı araçlarını kullanarak bir parça ekleme](sql-database-elastic-scale-add-a-shard.md) ve [hello RecoveryManager sınıfı toofix parça eşlemesi sorunlarının kullanarak](sql-database-elastic-database-recovery-manager.md).

![Esnek ölçeklendirme koşulları][1]

**Veritabanı**: bir Azure SQL veritabanı. 

**Veri bağımlı yönlendirme**: Merhaba belirli parçalama anahtara verilen bir uygulama tooconnect tooa parça sağlayan işlevselliği. Bkz: [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md). Çok karşılaştırma**[çok parça sorgu](sql-database-elastic-scale-multishard-querying.md)**.

**Genel parça eşleme**: hello harita parçalama anahtarları ve bunların ilgili parça içinde arasında bir **parça kümesi**. Merhaba genel parça eşleme hello depolanan **parça eşleme Yöneticisi**. Çok karşılaştırma**yerel parça eşleme**.

**Liste parça eşleme**: bir parça eşleme hangi parçalama anahtarları ayrı ayrı eşlendi. Çok karşılaştırma**aralığı parça eşleme**.   

**Yerel parça eşleme**: parça üzerinde depolanan, hello yerel parça eşleme hello parça üzerinde bulunan hello shardlets eşlemeler içerir.

**Çok parça sorgu**: özelliği tooissue bir sorgu birden fazla parça hello; sonuç kümeleri, UNION ALL semantiği (olarak da bilinen "yayma sorgu") kullanılarak döndürülür. Çok karşılaştırma**veri bağımlı yönlendirme**.

**Çok kiracılı** ve **tek Kiracı**: Bu tek Kiracı veritabanı ve çok Kiracı veritabanı gösterir:

![Tek ve çoklu kiracı veritabanları](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

Bir gösterimini işte **parçalı** tek ve çoklu kiracı veritabanları. 

![Tek ve çoklu kiracı veritabanları](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

**Aralık parça eşleme**: hangi hello parça Dağıtım stratejisi temel birden çok bitişik değerleri aralığı üzerinde bir parça eşleme. 

**Başvuru tabloları**: parçalı değildir ancak parça arasında çoğaltılan tabloları. Örneğin, posta kodları başvuru tablosunda depolanabilir. 

**Parça**: parçalı bir veri kümesinden veri depolayan bir Azure SQL veritabanı. 

**Parça esneklik**: her iki özelliği tooperform hello **yatay ölçekleme** ve **dikey ölçeklendirme**.

**Parçalı tabloları**: tabloları, parçalı, başka bir deyişle, verileri parçalama anahtar değerlerine göre parça dağıtılır. 

**Parçalama anahtar**: veri parça arasında nasıl dağıtıldığını belirler bir sütun değeri. Merhaba değer türü hello aşağıdakilerden biri olabilir: **int**, **bigint**, **varbinary**, veya **uniqueidentifier**. 

**Parça kümesi**: Merhaba öznitelikli toohello olan parça koleksiyonunu hello parça eşleme Yöneticisi'nde aynı parça eşleme.  

**Shardlet**: tüm hello verileri tek bir parça bir parçalama anahtar değeriyle ilişkilendirilmiş. Bir shardlet hello en küçük olası veri taşıma parçalı tabloları dağıtırken birimidir. 

**Parça eşleme**: Merhaba parçalama anahtarları ve bunların ilgili parça arasındaki eşlemeleri kümesi.

**Parça eşleme Yöneticisi**: hello parça harita(lar), parça konumları ve bir veya daha fazla parça kümeleri için eşlemelerini içeren bir Yönetim nesnesi ve veri deposu.

![Eşlemeleri][2]

## <a name="verbs"></a>Fiiller
**Yatay ölçekleme**: hello (veya) ölçeklendirme eylemi ekleyerek veya parça tooa parça eşleme, aşağıda gösterildiği gibi kaldırarak parça koleksiyonu.

![Yatay ve dikey ölçekleme][3]

**Birleştirme**: hello eylemi shardlets iki parça tooone parça taşıma ve uygun şekilde hello parça eşleme güncelleştiriliyor.

**Shardlet taşıma**: hello act tek shardlet tooa farklı parça taşıma. 

**Parça**: yatay aynı bölümleme hello eylemi bir parçalama anahtarına göre birden çok veritabanı arasında veri yapılandırılmış.

**Bölünmüş**: hello act birkaç shardlets bir parça tooanother (genellikle yeni) parça taşıma. Başlangıç noktasını Böl gibi bir parçalama anahtar hello kullanıcı tarafından sağlanır.

**Dikey ölçeklendirme**: hello Yukarı (veya aşağı) ölçeklendirme eylemi hello performans düzeyini tek tek bir parça. Örneğin, bir parça (ve daha fazla bilgi işlem kaynakları sonuçlanır) standart tooPremium gelen değiştirme. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

