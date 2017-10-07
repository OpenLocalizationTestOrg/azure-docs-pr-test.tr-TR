---
title: "aaaUpgrade toohello son esnek veritabanı istemci kitaplığı | Microsoft Docs"
description: "Uygulamalar ve kitaplıkları Nuget kullanarak yükseltme"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>Bir uygulama toouse hello son esnek veritabanı istemci kitaplığı yükseltme
Merhaba yeni sürümlerini [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md) NuGetand hello NuGetPackage Yöneticisi arabiriminde, Visual Studio aracılığıyla kullanılabilir. Yükseltmeler hello istemci kitaplığı yeni özellikler için destek ve hata düzeltmeleri içerir.

**Merhaba en son sürümü için:** çok Git[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Uygulamanızı hello yeni kitaplığı ile yeniden gibi Azure SQL veritabanlarını toosupport yeni özellikler depolanan parça eşleme Yöneticisi meta verileriniz varolan değiştirin.

Adımları sırayla gerçekleştirilmesi meta veri nesnesi güncelleştirildiğinde, hello istemci kitaplığı eski sürümleri artık eski sürümü meta veri nesnelerinin yükseltmeden sonra oluşturulmaz anlamına gelir, ortamınızda mevcut olmasını sağlar.   

## <a name="upgrade-steps"></a>Yükseltme adımları
**1. Uygulamalarınızı yükseltin.** Visual Studio, indirme ve başvuru hello son istemci kitaplığı sürümü tüm geliştirme projelerinizi hello kitaplığını kullanın; Daha sonra yeniden oluşturun ve dağıtın. 

* Visual Studio çözümünüzde seçin **Araçları** --> **NuGet Paket Yöneticisi** -->  **çözüm için NuGet paketlerini Yönet**. 
* (Visual Studio 2013) Merhaba sol panelinde seçin **güncelleştirmeleri**seçip hello **güncelleştirme** hello paket düğmesinde **Azure SQL Database esnek ölçek istemci Kitaplığı** hello görüntülenir penceresini açın.
* (Visual Studio 2015) Merhaba filtre kutusuna çok ayarlamak**kullanılabilir yükseltme**. Merhaba paket tooupdate seçin ve hello tıklayın **güncelleştirme** düğmesi.
* (Visual Studio 2017) Merhaba iletişim Hello üstünde seçin **güncelleştirmeleri**. Merhaba paket tooupdate seçin ve hello tıklayın **güncelleştirme** düğmesi.
* Derleme ve dağıtma. 

**2. Komut dosyalarınızı yükseltin.** Kullanıyorsanız **PowerShell** toomanage parça komutlar [hello yeni kitaplık sürümü yüklemek](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) ve kendisinden, yürütme komut dosyaları hello dizinine kopyalayın. 

**3. Bölünmüş birleştirme hizmetinizi yükseltin.** Merhaba esnek veritabanı bölünmüş Birleştirme aracı tooreorganize parçalı veriler, kullanırsanız [karşıdan yükleyip hello hello aracının en son sürümünü dağıtmak](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/). Ayrıntılı hizmet bulunabilir hello için yükseltme adımları [burada](sql-database-elastic-scale-overview-split-and-merge.md). 

**4. Parça eşleme Yöneticisi veritabanlarınızı yükseltme**. Azure SQL veritabanı'nda, parça eşlemeleri destekleme hello meta verileri yükseltin.  Bu, PowerShell veya C# kullanarak gerçekleştirmenin iki yolu vardır. Her iki seçenek aşağıda verilmiştir.

***Seçenek 1: Meta veri PowerShell kullanarak yükseltme***

1. Merhaba son komut satırı yardımcı programı Nuget'ten için karşıdan [burada](http://nuget.org/nuget.exe) ve tooa klasöre kaydedin. 
2. Bir komut istemi açın, toohello gidin aynı klasöre ve sorunu hello komutu:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. Yalnızca, örneğin yüklediğiniz hello yeni istemci DLL sürümü içeren toohello alt klasöre gidin:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. Hello Hello esnek veritabanı istemci yükseltme Resimli karşıdan [Komut Merkezi](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), ve hello içine Kaydet aynı içeren klasör hello DLL.
5. Bu klasördeki "PowerShell.\upgrade.ps1" Merhaba komut isteminden çalıştırın ve hello istemleri izleyin.

***Seçenek 2: C# kullanarak meta verileri yükseltme***

Alternatif olarak, hello meta veri yükseltmesi hello yöntemlerini çağırarak gerçekleştirir, ShardMapManager açar ve tüm parça tekrarlanan bir Visual Studio uygulaması oluşturma [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) ve [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) Bu örnekte olduğu gibi: 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

Bu teknikler meta verileri yükseltmeler için birden çok kez zarar uygulanabilir. Eski bir sürüm zaten güncelleştirdikten sonra yanlışlıkla bir parça oluşturur, örneğin, yükseltme yeniden tüm parça tooensure bu hello çalıştırabilirsiniz, altyapınız son meta veri sürümü varsa. 

**Not:** hello istemci Kitaplığı'nın yeni sürümleri yayımlanan tarih için Azure SQL DB ve tam tersini hello parça eşleme Yöneticisi meta verilerini önceki sürümleriyle toowork devam edin.   Ancak hello son istemcisinde, meta veri hello yeni özelliklerden bazıları tootake avantajlarından toobe yükseltilmesi gerekir.   Meta veri yükseltme tüm kullanıcı verileri ve uygulamaya özgü verileri, oluşturulan ve hello parça eşleme Yöneticisi tarafından kullanılan nesneler yalnızca etkilemez unutmayın.  Ve uygulamalar toooperate yukarıda açıklanan hello yükseltme sırası üzerinden devam eder. 

## <a name="elastic-database-client-version-history"></a>Esnek veritabanı istemci sürüm geçmişi
Sürüm geçmişi için çok Git[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

