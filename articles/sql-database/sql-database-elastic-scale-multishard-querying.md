---
title: "aaaQuery parçalı Azure SQL veritabanları | Microsoft Docs"
description: "Sorguları hello esnek veritabanı istemci kitaplığı kullanılarak parça çalıştırın."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>Çok parça sorgulama
## <a name="overview"></a>Genel Bakış
Merhaba ile [esnek veritabanı araçlarını](sql-database-elastic-scale-introduction.md), parçalı veritabanı çözümleri oluşturabilirsiniz. **Çok parça sorgulama** koleksiyonu/bir sorgu çalıştırılarak gerektiren raporlama verilerini birden fazla parça uzatır gibi görevler için kullanılır. (Bu çok Karşıtlık[veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md), tek bir parça tüm çalışma gerçekleştirir.) 

1. Alma bir [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) veya [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) hello kullanarak [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), veya hello [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) yöntemi. Bkz: [ **bir ShardMapManager oluşturma** ](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) ve [ **RangeShardMap veya ListShardMap almak**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Oluşturma bir  **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**  nesnesi.
3. Oluşturma bir  **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Set hello  **[CommandText özelliği](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa T-SQL komutu.
5. Tarafından arama hello Hello bağlamını  **[ExecuteReader yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Hello kullanarak hello sonuçlarını görüntülemek  **[MultiShardDataReader sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Örnek
Merhaba aşağıdaki kod gösterir kullanarak sorgulama yapmayı çok parça hello kullanımını bir verilen **ShardMap** adlı *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


En önemli fark, çok parça bağlantılarının hello yapıdır. Burada **SqlConnection** tek bir veritabanı üzerinde hello çalışır **MultiShardConnection** geçen bir ***parça koleksiyonunu*** giriş olarak. Parça parça eşlemesinden Hello koleksiyonunu doldurun. Merhaba sorgu kullanarak parça hello koleksiyonunu sonra yürütülür **UNION ALL** semantiği tooassemble tek bir genel sonuç. Merhaba satır kaynaklandığı hello parça hello adını hello kullanarak çıktıyı toohello isteğe bağlı olarak eklenebilir **ExecutionOptions** özelliği komutu. 

Merhaba çağrısı çok Not**myShardMap.GetShards()**. Bu yöntem tüm parça hello parça eşlemesinden alır ve bir kolay bir yolu toorun tüm ilgili veritabanları arasında bir sorgu sağlar. Hello koleksiyonunu parça çok parça sorgu Gelişmiş için başka bir LINQ gerçekleştirerek sorgulama çok hello çağrısından döndürülen hello koleksiyon üzerinde**myShardMap.GetShards()**. Merhaba kısmi sonuçlar İlkesi ile birlikte, çok parça sorgulama içinde geçerli yetenek hello onlarca parça toohundreds yedeklemek için tasarlanmış toowork olmuştur.

Çok parça sorgulama ile bir sınırlama şu anda Merhaba, parça ve sorgulanır shardlets için doğrulama yetersizliğidir. Veri bağımlı yönlendirme verilen parça sorgulama hello zaman hello parça eşleme parçası olduğunu doğrularken çok parça sorguları bu denetimi gerçekleştirme. Bu toomulti parça sorguları hello parça eşlemesinden kaldırılmış olan veritabanlarında çalıştırma neden olabilir.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Çok parça sorgular ve bölünmüş birleştirme işlemleri
Çok parça sorguları shardlets hello sorgulanan veritabanı üzerinde devam eden bölünmüş birleştirme işlemleri katılan olup olmadığını denetlemez. (Bkz [ölçeklendirme hello esnek veritabanı bölünmüş-birleştirme aracını kullanarak](sql-database-elastic-scale-overview-split-and-merge.md).) Burada satırları hello birden çok veritabanları için aynı shardlet Göster hello tooinconsistencies bu yol açabilir aynı çok parça sorgu. Bu sınırlamalara dikkat edin ve devam eden bölünmüş birleştirme işlemleri ve değişiklikleri toohello parça eşleme çok parça sorguları gerçekleştirirken boşaltma göz önünde bulundurun.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>Ayrıca bkz.
**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**  sınıflar ve yöntemler.

Parça Hello kullanarak yönetmek [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md). Adlı bir ad alanı içeren [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) tek bir sorgu ve sonuç kullanarak birden çok parça hello özelliği tooquery sağlar. Bu, bir parça koleksiyon sorgulanırken bir Özet sağlar. Ayrıca alternatif yürütme ilkelerini, özellikle kısmi sonuçlar, toodeal hatalarıyla çok sayıda parça sorgulanırken sağlar.  

