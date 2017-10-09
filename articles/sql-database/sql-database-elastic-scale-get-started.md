---
title: "aaaGet esnek veritabanı araçları ile başlatılan | Microsoft Docs"
description: "Merhaba esnek veritabanı araçları özelliği Çalıştır kolay örnek uygulaması da dahil olmak üzere Azure SQL veritabanı'nın temel açıklaması."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a>Esnek veritabanı araçlarını kullanmaya başlama
Bu belge toorun hello örnek uygulaması yardımcı olarak toohello geliştirici deneyimi sunar. Merhaba örnek basit parçalı bir uygulama oluşturur ve esnek veritabanı araçlarını anahtar özelliklerini inceler. Merhaba örnek gösterilmektedir hello işlevlerini [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md).

tooinstall hello kitaplığı, çok Git[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Merhaba kitaplığı bölümden hello açıklanan hello örnek uygulama ile birlikte yüklenir.

## <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2012 veya sonraki C# ile. Konumundaki ücretsiz sürümünü karşıdan [Visual Studio indirmeleri](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* NuGet 2.7 veya üzeri. tooget hello en son sürümü, bkz: [yükleme NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).

## <a name="download-and-run-hello-sample-app"></a>Merhaba örnek uygulamasını indirme ve çalıştırma
Merhaba **Azure SQL - Başlarken için esnek DB Araçları** örnek uygulama hello geliştirme deneyimi esnek veritabanı araçlarını kullanın parçalı uygulamalar için en önemli yönlerinden hello gösterir. Anahtar kullanım durumları için odaklanır [parça eşleme Yönetim](sql-database-elastic-scale-shard-map-management.md), [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md), ve [çok parça sorgulama](sql-database-elastic-scale-multishard-querying.md). toodownload ve çalışma hello örnek, şu adımları izleyin: 

1. Merhaba karşıdan [Azure SQL - Getting Started örnek için esnek DB Araçları](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) MSDN'den. Seçtiğiniz hello örnek tooa konumu sıkıştırmasını açın.

2. toocreate bir Proje Aç hello **ElasticScaleStarterKit.sln** hello çözümden **C#** dizin.

3. Merhaba örnek proje Hello çözümde, hello açmak **app.config** dosya. Ardından Azure SQL veritabanı sunucunuzun adını ve oturum açma bilgilerinizi (kullanıcı adı ve parola) hello dosya tooadd hello yönergeleri izleyin.

4. Derleme ve hello uygulamayı çalıştırın. İstendiğinde, Visual Studio toorestore hello NuGet paketlerini hello çözümünün etkinleştirin. Bu hello en son sürümünü hello esnek veritabanı istemci kitaplığını Nuget'ten indirir.

5. Merhaba farklı seçenekler toolearn hello istemci kitaplığı özellikleri hakkında daha fazla deneme. Hello adımları uygulamayı alır hello konsol çıkışı hello ve ücretsiz tooexplore hello kod hello perde arkasında eşitleyerek unutmayın.
   
    ![İlerleme durumu][4]

Tebrikler--başarıyla oluşturulmuş ve SQL Database esnek veritabanı araçlarını kullanarak ilk parçalı uygulamanızı çalıştırın. Visual Studio veya SQL Server Management Studio tooconnect tooyour SQL veritabanını kullan ve oluşturulan örnek hello hello parça hızlı göz atın. Yeni örnek parça veritabanları ve bir parça eşleme manager veritabanı fark edeceksiniz hello örneği oluşturdu.

> [!IMPORTANT]
> Böylece güncelleştirmeleri tooAzure ve SQL veritabanı ile eşitlenmesine, her zaman Management Studio hello en son sürümünü kullanmanızı öneririz. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a>Temel hello kod örneği
* **Eşlemelerini parça ve parça yönetme**: hello kod gösterir nasıl parça, aralıkları ve eşlemeleri hello dosyasındaki toowork **ShardManagementUtils.cs**. Daha fazla bilgi için bkz: [hello parça eşleme Yöneticisi veritabanlarıyla genişletme](http://go.microsoft.com/?linkid=9862595).  

* **Veri bağımlı yönlendirme**: işlemleri toohello sağ parça yönlendirme görüntülenir **DataDependentRoutingSample.cs**. Daha fazla bilgi için bkz: [veri bağımlı yönlendirme](http://go.microsoft.com/?linkid=9862596). 

* **Birden çok parça sorgulama**: parça sorgulama hello dosyasında gösterilen **MultiShardQuerySample.cs**. Daha fazla bilgi için bkz: [çok parça sorgulama](http://go.microsoft.com/?linkid=9862597).

* **Boş parça ekleme**: Merhaba yeni boş parça ekleme yinelemeli hello dosyasındaki hello kodu tarafından gerçekleştirilir **CreateShardSample.cs**. Daha fazla bilgi için bkz: [hello parça eşleme Yöneticisi veritabanlarıyla genişletme](http://go.microsoft.com/?linkid=9862595).

### <a name="other-elastic-scale-operations"></a>Diğer esnek ölçeklendirme işlemleri
* **Varolan bir parça bölme**: hello yetenek toosplit parça hello tarafından sağlanan **bölünmüş Birleştirme aracı**. Daha fazla bilgi için bkz: [ölçeklendirilmiş bulut veritabanları arasında verilerin taşınması](sql-database-elastic-scale-overview-split-and-merge.md).

* **Varolan parça birleştirme**: parça birleştirmeler, hello kullanarak da gerçekleştirilir **bölünmüş Birleştirme aracı**. Daha fazla bilgi için bkz: [ölçeklendirilmiş bulut veritabanları arasında verilerin taşınması](sql-database-elastic-scale-overview-split-and-merge.md).   

## <a name="cost"></a>Maliyet
Merhaba esnek veritabanı araçlarını ücretsizdir. Esnek veritabanı araçlarını kullandığınızda, hiçbir ek bir ücret Azure kullanımınızı hello maliyetini en üstünde almadığınız. 

Örneğin, yeni veritabanları Merhaba örnek uygulaması oluşturur. Merhaba maliyeti seçtiğiniz hello SQL veritabanı sürümü ve hello uygulamanızın Azure kullanım bağlıdır.

Fiyatlandırma bilgileri için bkz: [SQL veritabanı fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Sonraki adımlar
Esnek veritabanı araçları hakkında daha fazla bilgi için sayfalar aşağıdaki hello bakın:

* Kod örnekleri: 
  * [Azure SQL - Başlarken için esnek veritabanı araçları](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [Azure SQL - Entity Framework tümleştirme için esnek veritabanı araçları](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE)
  * [Betik Merkezi'nde parça esneklik](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* Blog: [esnek genişleme Duyurusu](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)
* Microsoft Virtual Academy: [genişleme kullanarak parçalama uygulama'hello esnek veritabanı istemci kitaplığı Video ile](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965) 
* Kanal 9: [esnek genişleme genel bakış videosu](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)
* Tartışma forumu: [Azure SQL veritabanı Forumu](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)
* toomeasure performans: [parça eşleme Yöneticisi için performans sayaçları](sql-database-elastic-database-client-library.md)

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

