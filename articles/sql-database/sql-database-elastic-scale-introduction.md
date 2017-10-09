---
title: "Azure SQL Database ile kullanıma aaaScaling | Microsoft Docs"
description: "Bir hizmet (SaaS) geliştiriciler olarak yazılım kolayca esnek oluşturabilirsiniz, bu araçları kullanarak hello ölçeklenebilir veritabanlarında bulut"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Azure SQL Database ile ölçek genişletme
Out hello kullanarak Azure SQL veritabanlarını kolayca ölçeklendirebilirsiniz **esnek veritabanı** araçları. Bu araçları ve özelliklerinin hello neredeyse sınırsız kullanmanıza olanak tanır veritabanı kaynaklarını **Azure SQL veritabanı** işlem iş yükleri ve özellikle yazılım hizmet (SaaS) uygulamaları olarak toocreate çözümleri. Esnek veritabanı özellikleri hello aşağıdakilerden oluşur:

* [Esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md): hello istemci kitaplığı toocreate sağlar ve parçalı veritabanlarını korumak bir özelliktir.  Bkz: [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).
* [Esnek veritabanı bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md): parçalı veritabanları arasında verileri taşır. Bu, bir çok Kiracı veritabanı tooa tek Kiracı veritabanı (veya tersi) veri taşıma için kullanışlıdır. Bkz: [esnek veritabanı bölünmüş Birleştirme aracı Öğreticisi](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [Esnek veritabanı iş](sql-database-elastic-jobs-overview.md) (Önizleme): kullanım işleri toomanage çok sayıda Azure SQL veritabanları. Kolayca şema değişiklikleri, kimlik bilgileri yönetimi, başvuru veri güncelleştirmeleri, performans verileri toplama veya Kiracı (müşteri) telemetri koleksiyonunu işlemleriyle gibi yönetim işlemlerini gerçekleştirin.
* [Esnek veritabanı sorgusu](sql-database-elastic-query-overview.md) (Önizleme): birden çok veritabanı yayılan toorun Transact-SQL sorgusu tanır. Bu, Excel, Powerbı, Tableau, vb. gibi bağlantı tooreporting araçları sağlar.
* [Esnek işlemleri](sql-database-elastic-transactions-overview.md): Bu özellik, Azure SQL veritabanı birkaç veritabanlarında span toorun işlemler sağlar. Esnek veritabanı işlemleri ADO .NET kullanarak .NET uygulamaları için kullanılabilir ve hello kullanarak hello tanıdık programlama deneyimiyle tümleştirmenize [System.Transaction sınıfları](https://msdn.microsoft.com/library/system.transactions.aspx).

Merhaba aşağıda görüldüğü hello içeren bir mimari **esnek veritabanı özelliklerini** ilişkisi tooa koleksiyonunda veritabanları.

Bu grafikte renkleri hello veritabanı şemaları temsil eder. Veritabanları ile Merhaba aynı renk paylaşımına hello aynı şema.

1. Bir dizi **Azure SQL veritabanlarını** parçalama mimarisi kullanarak Azure'da barındırılır.
2. Merhaba **esnek veritabanı istemci Kitaplığı** kullanılan toomanage bir parça ayarlanır.
3. Bir alt hello veritabanlarının içine konur bir **esnek havuz**. (Bkz [bir havuzu nedir?](sql-database-elastic-pool.md)).
4. Bir **esnek veritabanı iş** zamanlanmış çalıştırmaları veya geçici T-SQL betikleri tüm veritabanlarında.
5. Merhaba **bölünmüş Birleştirme aracı** bir parça tooanother kullanılan toomove verilerdir.
6. Merhaba **esnek veritabanı sorgusu** toowrite hello parça kümesindeki tüm veritabanları yayılan bir sorgu sağlar.
7. **Esnek işlemleri** birden fazla veritabanı span toorun işlemler sağlar. 

![Elastik Veritabanı araçları][1]

## <a name="why-use-hello-tools"></a>Merhaba araçları neden kullanılır?
Sağlanması esneklik ve ölçek bulut uygulamaları için VM'ler ve blob depolama--basit yalnızca eklemek veya birimleri çıkarın veya güç artırın. Ancak, durum bilgisi olan veri işleme ilişkisel veritabanları için bir sınama kaldığını. Bu senaryolarda zorluklar ortaya çıktı:

* Büyüyen ve hello ilişkisel veritabanı bölümü, iş yükü için kapasite küçültme.
* Belirli bir alt - özellikle meşgul end-müşteri (Kiracı) gibi veri kümesini etkileyen kaynaklanabilecek etkin yönetme.

Geleneksel olarak, aşağıdaki gibi senaryoları büyük ölçekli veritabanı sunucuları toosupport hello uygulamada yatırım tarafından giderilmiştir. Ancak, bu seçenek, tüm işlemler önceden tanımlanmış ticari donanımlarda nerede olacağını hello bulutta sınırlıdır. Bunun yerine, veri dağıtımı ve birçok veritabanı arasında aynı yapılandırılmış işleme ("parçalama" bilinen bir genişleme deseni), bir alternatif tootraditional büyütme yaklaşımlar hem maliyet ve esneklik açısından'e sağlar.

## <a name="horizontal-and-vertical-scaling"></a>Yatay ve dikey ölçekleme
Aşağıdaki Hello şekilde hello hello esnek veritabanları Genişletilebilir hello temel yolu olan ölçeklendirme, yatay ve dikey boyutları gösterilmektedir.

![Yatay ve dikey genişletme][2]

Yatay ölçekleme tooadding veya kaldırma veritabanları sipariş tooadjust kapasite ya da genel performansı gösterir. Bu aynı zamanda "ölçeklendirme" belirtilmiştir. Parçalama, hangi veri bölümlenmiş özdeş olarak yapılandırılmış veritabanları koleksiyonunda olan yaygın bir şekilde tooimplement yatay ölçeklendirme.  

Dikey ölçekleme başvuruyor tooincreasing veya tek bir veritabanının hello performans düzeyini azaltarak — bu "ölçeklendirmeyi." olarak da bilinir

Çoğu bulut ölçekli veritabanı uygulamalar, bu iki stratejileri bileşimini kullanır. Örneğin, bir hizmet uygulaması olarak bir yazılım yatay ölçeklendirme tooprovision yeni end-müşteriler ve tooallow toogrow veya küçültme her bitiş müşterinin veritabanı kaynaklarını hello iş yükü tarafından gerektiği şekilde ölçeklendirme dikey kullanabilir.

* Yatay ölçekleme yönetilir hello kullanarak [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md).
* Dikey ölçeklendirme gerçekleştirilir Azure PowerShell cmdlet'leri toochange hello hizmet katmanı kullanarak veya bir esnek havuz veritabanları koyarak.

## <a name="sharding"></a>Parçalama
*Parçalama* teknik toodistribute büyük miktarlarda veri özdeş olarak yapılandırılmış bir bağımsız veritabanları arasında sayısıdır. Son müşterilere veya işletmeler için yazılım hizmet (SAAS) tekliflerini oluşturma bulut geliştiriciler ile özellikle yaygın olarak kullanılır. Bu son sık başvurulan tooas "kiracılar" müşterilerdir. Parçalama birkaç nedenden dolayı için gerekli olabilir:  

* Merhaba toplam veri çok büyük toofit hello kısıtlamaları tek bir veritabanının içindeki miktarıdır
* Merhaba hareket işleme Merhaba genel iş yükü hello özellikleri tek bir veritabanının aşıyor.
* Ayrı veritabanlarını her bir kiracı için gerektiği şekilde kiracılar birbirinden, fiziksel yalıtım gerektirebilir
* Bir veritabanı farklı bölümlerini farklı coğrafyalara tooreside uyumluluk, performans veya jeopolitik nedenleri için gerekebilir.

Dağıtılmış aygıtlardan veri alım gibi diğer senaryolarda parçalama kullanılan toofill geçici olarak düzenlenmiş bir veritabanları kümesi olabilir. Örneğin, ayrı bir veritabanı tooeach gün veya hafta ayrılabilir. Bu durumda, bir tamsayı temsil eden başlangıç tarihi (mevcut hello parçalı tabloları tüm satırlarda) hello parçalama anahtarı olabilir ve bir tarih aralığı için bilgileri alınıyor sorguları hello uygulama toohello alt hello aralığında kapsayan veritabanlarının tarafından yönlendirilmesi gereken Soru.

Parçalama en iyi çalışır bir uygulamadaki her işlem kısıtlı tooa olabilir, tek bir parçalama anahtar değeri. Bu, tüm işlemleri yerel tooa belirli veritabanı olmasını sağlar.

## <a name="multi-tenant-and-single-tenant"></a>Çok kiracılı ve tek Kiracı
Bazı uygulamalar her bir kiracı için ayrı bir veritabanı oluşturma hello basit yaklaşımı kullanın. Merhaba budur **tek bir kiracı parçalama düzeni** yalıtımı, yedekleme/geri yükleme yeteneği ve kaynak hello Kiracı hello bazda ölçeklendirme sağlar. Tek bir kiracı parçalama ile her veritabanı bir belirli Kiracı kimliği değeri (veya müşteri anahtar değeri ile) ilgili değildir ancak bu anahtarı her zaman hello verilerde kendisini bulunması gerekmez. Bunu olduğu hello uygulamanın sorumluluk tooroute her isteği toohello uygun veritabanı - ve hello istemci kitaplığı bu kolaylaştırabilir.

![Tek bir kiracı çok kiracılı karşılaştırması][4]

Diğer senaryolar paketi birden çok kiracıya birlikte ayrı veritabanlarına yalıtma yerine veritabanları içine. Tipik bir budur **çok kiracılı parçalama düzeni** - ve uygulamanın çok küçük kiracılar çok sayıda yönetir hello gerçeğiyle güdümlü. Çok kiracılı parçalama tüm toocarry hello Kiracı kimliği veya parçalama anahtarı tanımlayan anahtar tasarlanmış hello satırları hello veritabanı tablolarındaki edilir. Yeniden hello uygulama katmanı, bir kiracının isteği toohello uygun veritabanı yönlendirme için sorumludur ve bu hello esnek veritabanı istemci kitaplığı tarafından desteklenebilir. Ayrıca, satır düzeyi güvenlik hangi satırların her Kiracı erişebilir - Ayrıntılar için bkz: kullanılan toofilter olabilir [çok kiracılı uygulamalarla esnek veritabanı araçlarını ve satır düzeyi güvenlik](sql-database-elastic-tools-multi-tenant-row-level-security.md). Verileri veritabanları arasında yeniden dağıtma hello çok kiracılı parçalama desenle gerekli olabilir ve bu hello esnek veritabanı bölünmüş Birleştirme aracı tarafından sayesinde kolaylaşır. Esnek havuzları kullanan SaaS uygulamaları için Tasarım desenleri hakkında daha fazla toolearn bkz [Azure SQL veritabanı ile çok kiracılı SaaS uygulamaları için Tasarım desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>Birden çok toosingle kiralama veritabanlarından veri taşıma
Bir SaaS uygulaması oluştururken, deneme sürümünü tipik toooffer müşteri adayları olan hello yazılım. Bu durumda, düşük maliyetli toouse hello veri için bir çok Kiracı veritabanı değil. Bir müşteri adaylarını olur, çünkü daha iyi performans sağlar ancak, tek Kiracı veritabanı daha iyidir. Merhaba müşteri verileri hello deneme süresi boyunca yarattıysanız hello kullan [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md) toomove hello veritabanındaki verileri hello çok kiracılı toohello yeni tek Kiracı.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba istemci Kitaplığı gösteren bir örnek uygulama için bkz: [esnek Datababase araçları ile çalışmaya başlama](sql-database-elastic-scale-get-started.md).

tooconvert varolan veritabanları toouse hello araçları, bkz: [geçirme varolan veritabanları tooscale kullanıma](sql-database-elastic-convert-to-use-elastic-tools.md).

Merhaba esnek havuzun toosee hello özellikleri bkz [esnek havuzlar için fiyat ve performans konuları](sql-database-elastic-pool.md), veya ile yeni bir havuz oluşturma [esnek havuzlar](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

