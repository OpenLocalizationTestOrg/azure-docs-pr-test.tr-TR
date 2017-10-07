---
title: "aaaAzure SQL esnek ölçek SSS | Microsoft Docs"
description: "Azure SQL Database esnek ölçeği hakkında sık sorulan sorular."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>Esnek veritabanı araçlarını SSS
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>Tek Kiracı başına parça ve hiçbir parçalama anahtarı varsa, nasıl hello parçalama anahtarı hello şema bilgilerini doldurmak?
Yalnızca kullanılan toosplit birleştirme senaryoları Hello şema bilgileri nesnesidir. Bir uygulama kendiliğinden tek Kiracı ise hello bölünmüş Birleştirme aracı gerektirmez ve böylece gerek toopopulate hello şema bilgileri nesne yok.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>Bir veritabanı sağlanan ve bir parça eşleme Yöneticisi zaten, bu yeni veritabanını bir parça nasıl kaydettirebilirim?
Lütfen bakın  **[hello esnek veritabanı istemci kitaplığı kullanılarak bir parça tooan uygulaması ekleme](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>Esnek veritabanı araçlarını ne kadar maliyet?
Merhaba esnek veritabanı istemci kitaplığı kullanılarak maliyetlerin tabi değildir. Yalnızca parça ve hello parça eşleme Yöneticisi için kullandığınız hello Azure SQL veritabanları gibi hello web/çalışan rolleri için hello bölünmüş Birleştirme aracı sağlamak için maliyetleri tahakkuk.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>Neden bir parça sunucusundan farklı bir sunucuya eklediğinizde kimlik bilgilerimi çalışmayan?
Kimlik bilgileri hello biçiminde kullanmayın "kullanıcı kimliği =username@servername", bunun yerine yalnızca kullanın "kullanıcı kimliği kullanıcı adı =".  Ayrıca, bu hello "username" oturum açma hello parça üzerinde izinleri bulunduğundan emin olun.

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>I toocreate parça eşleme Yöneticisi gerekir ve uygulamalarım Başlat her zaman parça doldurmak?
Hayır — hello hello parça eşleme Yöneticisi oluşturulmasını (örneğin,  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) tek seferlik bir işlemdir.  Uygulamanız hello çağrısı kullanacak  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  uygulama başlatma zaman.  Uygulama etki alanı başına yalnızca bir tür çağrısı var olmalıdır.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>I esnek veritabanı araçlarını kullanma hakkında sorularınız varsa, bunları yanıtlanan nasıl sağlarım?
Lütfen hello üzerinde toous ulaşmak [Azure SQL veritabanı Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>Bir parçalama anahtarı kullanarak bir veritabanı bağlantısı aldığınızda, diğer parçalama hello üzerinde aynı anahtarları için hala sorgu veri miyim parça.  Bu tasarım gereği mi?
Merhaba esnek ölçeklendirme API'leri parçalama anahtarınız için bir bağlantı toohello doğru veritabanı vermek, ancak parçalama anahtar filtreleme sağlamaz.  Ekleme **burada** yan tümceleri tooyour sorgu toorestrict hello kapsam toohello gerekirse, parçalama anahtarı, sağlanan.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>Farklı bir Azure veritabanı sürümü için her parça my parça kümesinde kullanabilir miyim?
Evet, bir parça tek tek bir veritabanıdır ve bu nedenle bir parça Premium edition başka Standard edition olsa da olabilir. Ayrıca, bir parça hello sürümü birden çok kez hello ömrü hello parça boyunca yukarı veya aşağı ölçeklendirebilirsiniz.

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>Bölünmüş Birleştirme aracı sağlama hello (veya mu Sil) bir bölme veya birleştirme işlemi sırasında bir veritabanı?
Hayır. İçin **bölme** işlemleri hello hedef veritabanı ile uygun şema hello bulunmalı ve hello parça eşleme Yöneticisi ile kayıtlı olması.  İçin **birleştirme** işlemleri hello parça hello parça eşleme Yöneticisi'nden silin ve hello veritabanı silmeniz gerekir.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

