---
title: "aaaUsing kurtarma Yöneticisi toofix parça eşleme sorunları | Microsoft Docs"
description: "Merhaba RecoveryManager sınıfı toosolve parça eşlemeleri sorun kullanın"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>Merhaba RecoveryManager sınıfı toofix parça eşlemesi sorunlarının kullanma
Merhaba [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) sınıfı hello özelliği tooeasily algılayıp hello genel parça eşleme (GSM) parçalı veritabanı ortamında hello yerel parça eşleme (LSM) arasındaki tutarsızlıkları düzeltmek ADO.Net uygulamaları sağlar. 

Merhaba GSM ve LSM izleme hello eşleme parçalı bir ortamda her veritabanı. Bazen, bir kesme hello GSM ve hello LSM arasında oluşur. Bu durumda, hello RecoveryManager sınıfı toodetect kullanın ve hello sonu onarın.

Merhaba RecoveryManager sınıfı hello bir parçasıdır [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md). 

![Parça eşleme][1]

Terim tanımları için bkz: [esnek veritabanı araçlarını sözlüğü](sql-database-elastic-scale-glossary.md). toounderstand nasıl hello **ShardMapManager** kullanılan toomanage veri parçalı bir çözümde bkz [parça eşleme Yönetim](sql-database-elastic-scale-shard-map-management.md).

## <a name="why-use-hello-recovery-manager"></a>Merhaba kurtarma Yöneticisi neden kullanılır?
Parçalı veritabanı ortamında, bir kiracı veritabanı başına ve sunucu başına birçok veritabanı yok. Ayrıca olabilir pek çok sunucu hello ortamında. Böylece çağrıları yönlendirilmiş toohello doğru sunucu ve veritabanı her veritabanı hello parça eşlemesinde eşlenir. Veritabanlarını tooa göre izlenen **parçalama anahtar**, ve her parça atanan bir **anahtar değerlerin**. Örneğin, bir parçalama anahtar hello müşteri adları "D" "F'ye" çok temsil edebilir tüm parça (diğer adıyla veritabanları) eşleme hello ve bunların eşleme aralıkları hello içerdiği **genel parça eşleme (GSM)**. Her veritabanı hello adlandırılıyor hello parça üzerinde yer alan hello aralıkları haritasını de içeren **yerel parça eşleme (LSM)**. Bir uygulama tooa parça bağlandığında, hello eşleme hello app hızlı alma için önbelleğe alınır. Merhaba LSM önbelleğe kullanılan toovalidate verilerdir. 

Merhaba GSM ve LSM nedenleri aşağıdaki Merhaba eşitlenmemiş hale gelebilir:

1. Merhaba, aralığı toono uzun düşünülen bir parça silinmesini kullanın veya parça yeniden adlandırma. Bir parça silme sonuçlanıyor bir **parça eşleme yalnız**. Benzer şekilde, yeniden adlandırılmış bir veritabanını yalnız bırakılmış parça eşleme neden olabilir. Merhaba değişikliğin hello amacı, bağlı olarak hello parça kaldırılan toobe gerekebilir veya güncelleştirilmiş toobe hello parça konum gerekiyor. Silinen bir veritabanını toorecover bkz [silinen bir veritabanını geri](sql-database-recovery-using-backups.md).
2. Bir yük devretme coğrafi olayı oluşur. toocontinue, bir hello sunucu adını ve veritabanı adını parça eşleme Yöneticisi'nde hello uygulama ve güncelleştirme hello parça eşleme ayrıntılarını tüm parça parça eşlemesindeki güncelleştirmeniz gerekir. Bir yük devretme coğrafi ise, böyle bir kurtarma mantık hello yük devretme iş akışı içinde otomatik olarak. Kurtarma eylemleri otomatikleştirme coğrafi etkinleştirilmiş veritabanları için uyumlu bir yönetilebilirlik sağlar ve el ile İnsan Eylemler önler. bir veri merkezi kesintisinden ise bir veritabanı bakın seçenekleri toorecover hakkında toolearn [iş sürekliliği](sql-database-business-continuity.md) ve [olağanüstü durum kurtarma](sql-database-disaster-recovery.md).
3. Bir parça veya hello ShardMapManager geri yüklenen tooan veritabanıdır önceki noktası süre. toolearn yedeklemeler kullanarak zaman kurtarma noktası hakkında bkz [Yedekleme kullanarak kurtarma](sql-database-recovery-using-backups.md).

Azure SQL veritabanı esnek veritabanı araçlarını, coğrafi çoğaltma ve geri yükleme hakkında daha fazla bilgi için hello aşağıdakilere bakın: 

* [Genel Bakış: SQL veritabanı ile iş devamlılığı ve veritabanı olağanüstü durum kurtarma bulut](sql-database-business-continuity.md) 
* [Esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md)  
* [ShardMap Yönetimi](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>Bir ShardMapManager RecoveryManager alınıyor
Merhaba ilk adımı toocreate RecoveryManager örneği oluşturur. Merhaba [GetRecoveryManager yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) döndürür hello hello geçerli kurtarma Yöneticisi [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) örneği. Merhaba parça bulunan tüm tutarsızlıkları tooaddress eşleme, hello RecoveryManager hello belirli parça eşleme için ilk almanız gerekir. 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

Bu örnekte, hello RecoveryManager hello ShardMapManager ' başlatılır. Merhaba bir ShardMap içeren ShardMapManager de zaten başlatılmış. 

Bu uygulama kodu hello parça eşleme kendisini yöneten beri hello Fabrika yönteminde kullanılan kimlik bilgileri hello (örneğin, önceki hello içinde smmConnectionString) hello tarafından başvurulan hello GSM veritabanı üzerinde okuma-yazma izinlerine sahip kimlik bilgileri olmalıdır bağlantı dizesi. Bu kimlik bilgileri, veri bağımlı yönlendirme için kullanılan kimlik bilgileri tooopen bağlantılar genellikle farklıdır. Daha fazla bilgi için bkz: [hello esnek veritabanı istemci kimlik bilgilerini kullanarak](sql-database-elastic-scale-manage-credentials.md).

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>Bir parça silindikten sonra bir parça hello ShardMap ' kaldırma
Merhaba [DetachShard yöntemi](https://msdn.microsoft.com/library/azure/dn842083.aspx) parça hello parça eşlemesinden verilen hello ayırır ve hello parça ile ilişkili eşlemeleri siler.  

* Merhaba konum parametresi hello parça, özellikle sunucu adını ve veritabanı adını ayrılmakta hello parça konumdur. 
* Merhaba shardMapName parametresi hello parça eşleme adıdır. Bu yalnızca olan birden fazla parça eşlemeleri hello tarafından yönetildiğinde gerekli aynı parça eşleme Yöneticisi. İsteğe bağlı. 


> [!IMPORTANT]
> Yalnızca hello aralığı güncelleştirilmiş hello eşlemesi için boş olduğundan eminseniz bu tekniği kullanın. Yukarıdaki Hello yöntemleri taşınan hello aralığı için veri denetleme, en iyi şekilde kodunuzda tooinclude denetler.
>

Bu örnek parça hello parça eşlemesinden kaldırır. 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

Merhaba parça eşleme hello parça hello GSM hello parça hello silinmesini önce konumda yansıtır. Merhaba parça silindiği için bu kasıtlı ve hello parçalama anahtar aralığı artık kullanımda varsayılır. Aksi durumda, zaman içinde nokta geri yükleme yürütebilir. bir önceki noktası zaman gelen toorecover hello parça. (Bu durumda, aşağıdaki bölümde toodetect parça tutarsızlıklar hello gözden geçirin.) toorecover, bkz: [zaman kurtarma noktası](sql-database-recovery-using-backups.md).

Merhaba veritabanı silme kasıtlı varsayıldığından hello son yönetim temizleme toodelete hello girişi toohello parça hello parça eşleme Yöneticisi'nde bir eylemdir. Bu, istemeden beklenmiyor bilgiler tooa aralığı yazmasını Merhaba uygulaması engeller.

## <a name="toodetect-mapping-differences"></a>toodetect eşleme farklar
Merhaba [DetectMappingDifferences yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) seçer ve her iki parça eşlemeleri (GSM ve LSM) eşlemesi uzlaştırır hello parça eşlemeleri (yerel veya genel) gerçekte hello kaynağı olarak döndürür.

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* Merhaba *konumu* hello sunucu adını ve veritabanı adını belirtir. 
* Merhaba *shardMapName* parametredir hello parça eşleme adı. Yalnızca budur birden fazla parça eşlemeleri hello tarafından yönetilen, gerekli aynı parça eşleme Yöneticisi. İsteğe bağlı. 

## <a name="tooresolve-mapping-differences"></a>tooresolve eşleme farklar
Merhaba [ResolveMappingDifferences yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) hello parça eşlemeleri (yerel veya genel) birini gerçekte hello kaynağı olarak seçer ve her iki parça eşlemeleri (GSM ve LSM) eşlemesi uzlaştırır.

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* Merhaba *RecoveryToken* parametresi hello eşlemeleri hello farklılıkları hello GSM hello belirli parça Merhaba LSM arasındaki numaralandırır. 
* Merhaba [MappingDifferenceResolution numaralandırma](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) hello parça eşlemeleri hello birbirinden çözmek için kullanılan tooindicate hello yöntemidir. 
* **MappingDifferenceResolution.KeepShardMapping** hello LSM içerdiğinde hello doğru eşleme ve bu nedenle hello parça hello eşlemesindeki kullanılmalıdır önerilir. Bir yük devretme ise genellikle hello böyledir: hello parça şimdi yeni bir sunucuda yer alıyor. Merhaba parça (Merhaba RecoveryManager.DetachShard yöntemi kullanılarak) GSM hello kaldırılmalıdır olduğundan, bir eşleme GSM hello üzerinde artık yok. Bu nedenle, hello LSM kullanılan toore olmalıdır-hello parça eşleme oluşturun.

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>Bir parça geri yüklendikten sonra parça toohello ShardMap ekleme
Merhaba [AttachShard yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) ekler hello verilen parça toohello parça eşleme. Parça eşleme tutarsızlıkları algılar ve hello eşlemeleri toomatch hello parça hello parça geri yükleme işlemi hello noktada güncelleştirir. Merhaba zaman içinde nokta geri yüklemesi hello damgasıyla eklenmiş tooa yeni veritabanı varsayılan olarak bu yana hello veritabanının da (Merhaba parça geri önce) yeniden adlandırılmış tooreflect hello özgün veritabanı adıdır varsayılır. 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* Merhaba *konumu* parametredir hello sunucu adını ve veritabanı adını iliştirilmekte hello parça. 
* Merhaba *shardMapName* parametredir hello parça eşleme adı. Bu yalnızca olan birden fazla parça eşlemeleri hello tarafından yönetildiğinde gerekli aynı parça eşleme Yöneticisi. İsteğe bağlı. 

Bu örnek, önceki noktası-zaman bir yakın zamanda geri bir parça toohello parça eşlemesi ekler. Merhaba parça (yani hello hello LSM içinde hello parça eşleme) geri olduğundan, büyük olasılıkla tutarsız hello parça hello GSM girişi ile kalır. Bu örnek kod dışında hello parça geri yüklendi ve hello veritabanının toohello orijinal adı yeniden adlandırıldı. Geri yüklenen beri hello güvenilen eşleme hello eşleme hello LSM içinde olduğu varsayılır. 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>Bir coğrafi-yük devretme (geri yükleme) hello parça parça konumları güncelleştiriliyor
Bir yük devretme coğrafi ise hello ikincil veritabanı yazma erişilebilir yapılır ve hello yeni birincil veritabanı haline gelir. Merhaba sunucu ve potansiyel olarak (bağlı olarak yapılandırmanızı) hello veritabanı adı Merhaba, hello özgün birincil sunucudan farklı olabilir. Bu nedenle hello GSM içinde hello parça eşleme girdileri hello ve LSM düzeltilmesi gerekir. Benzer şekilde, hello veritabanının geri yüklenen tooa farklı bir ad veya konum veya tooan ise daha önceki bir noktaya, bu neden olabilecek tutarsızlıklar hello parça eşlemeleri. Merhaba parça eşleme Yöneticisi açık bağlantıları toohello doğru veritabanı hello dağıtımını işler. Dağıtım hello parça eşleme ve hello hello uygulamaları isteği hello hedefidir hello parçalama anahtarının değerini hello verileri temel alır. Coğrafi-yük devretme sonrasında, bu bilgileri hello doğru sunucu adını, veritabanı adının ve hello kurtarılan veritabanının parça eşleme ile güncelleştirilmesi gerekir. 

## <a name="best-practices"></a>En iyi uygulamalar
Coğrafi yük devretme ve kurtarma genellikle Merhaba uygulaması özellikle Azure SQL veritabanları iş sürekliliği özelliklerden biri kullanılarak bir bulut Yöneticisi tarafından yönetilen işlemleridir. İş sürekliliği planlama işlemleri, yordamlar ve işletme işlemleri kesintisiz devam edebilirsiniz ölçüleri tooensure gerektirir. Merhaba yöntemleri hello RecoveryManager sınıfı parçası kullanıldığı şekilde kullanılabilir bu iş akışı tooensure hello içinde GSM ve LSM hello kurtarma eyleme geçen bağlı güncel tutulur. Beş temel adımı vardır hello sağlama tooproperly GSM ve LSM hello doğru bilgileri bir yük devretme olayından sonra yansıtır. Bu adımları mevcut araçlar ve iş akışı tümleşik uygulama kodu tooexecute hello. 

1. Merhaba RecoveryManager hello ShardMapManager ' alın. 
2. Merhaba eski parça hello parça eşlemesinden kullanımdan çıkarın.
3. Merhaba yeni parça konum dahil olmak üzere hello yeni parça toohello parça eşleme, ekleyin.
4. Tutarsızlıklar GSM ve LSM hello arasında eşleme hello algıla. 
5. Merhaba GSM ve hello LSM, güvenen hello LSM arasındaki farklılıkları giderin. 

Bu örnek hello aşağıdaki adımları gerçekleştirir:

1. Parça parça konumlarını hello yük devretme olayından önce gösterecek parça eşleme hello kaldırır.
2. Parça toohello parça eşleme yansıtıcı hello yeni parça konumlar ekler (Merhaba parametresi "Configuration.SecondaryServer" Merhaba yeni bir sunucu adı olan, ancak aynı hello veritabanı adı).
3. Hello GSM ve her parça Merhaba LSM arasındaki eşleme farkları algılayarak Hello kurtarma belirteçlerini alır. 
4. Merhaba her parça LSM güvenen hello eşlemesinden tarafından Hello tutarsızlıklar çözümler. 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

