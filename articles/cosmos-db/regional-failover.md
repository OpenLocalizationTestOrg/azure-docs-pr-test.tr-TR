---
title: "Azure Cosmos veritabanı aaaRegional yük devretme | Microsoft Docs"
description: "Azure Cosmos DB ile nasıl elle ve otomatik yük devretme çalıştığı hakkında bilgi edinin."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a>İş sürekliliği Azure Cosmos veritabanı için bölgesel otomatik yük devretme
Azure Cosmos DB basitleştirir hello genel dağıtım veri sunarak tam olarak yönetilen, [bölgeli veritabanı hesaplarını](distribute-data-globally.md) tutarlılık, kullanılabilirlik ve karşılık gelen tüm ile performans arasında NET bileşim sağlayın güvence altına alır. Cosmos DB hesapları teklif yüksek kullanılabilirlik, tek bir basamak ms gecikme [iyi tanımlanmış tutarlılık düzeylerini](consistency-levels.md), çok girişli API'leri ve hello özelliği tooelastically ölçek işleme ve depolama ile bölgesel saydam yük devretme Merhaba Dünya çapında. 

Cosmos DB açık ikisini de destekler ve ilke tabanlı yük devretmeleri, toocontrol hello uçtan uca sistem davranışını hataları hello olayda izin verir. Bu makalede ele:

* El ile yük devretme işlemlerini Cosmos DB'de nasıl çalışır?
* Nasıl Cosmos DB otomatik yük devretme iş ve veri olduğunda neler gider aşağı center?
* Nasıl el ile yük devretme işlemlerini uygulama mimarilerinde kullanabilir miyim?

Ayrıca bu Azure bölgesel yük devretme işlemlerini Cuma video Scott Hanselman ve sorumlu mühendislik Yöneticisi Karthik Raman öğrenebilirsiniz.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a id="ConfigureMultiRegionApplications"></a>Bölgeli uygulamaları yapılandırma
Biz yük devretme modları dalın önce bölgeli kullanılabilirlik uygulama tootake avantajı yapılandırmak ve bölgesel yük devretme işlemlerini hello yüz içinde dayanıklı olmasını nasıl ele.

* İlk olarak, birden çok bölgeye uygulamanızda dağıtma
* tooensure düşük gecikme süresi erişimi, uygulamanın dağıtıldığı her bölgesinden yapılandırma hello karşılık gelen [tercih edilen bölge listesi](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) SDK'ları hello biri aracılığıyla her bölgede desteklenen.

kod parçacığında gösterildiği nasıl aşağıdaki hello tooinitialize bölgeli uygulama. Burada, Azure Cosmos DB hesap hello `contoso.documents.azure.com` iki bölgede ile - Batı ABD ve Kuzey Avrupa yapılandırılır. 

* Merhaba uygulama hello Batı ABD bölgesi (örneğin Azure App Services kullanarak) dağıtılır 
* İle yapılandırılmış `West US` hello ilk tercih edilen bölge, düşük gecikme süresi için okur
* İle yapılandırılmış `North Europe` hello ikinci tercih edilen bölge (için yüksek kullanılabilirlik bölgesel arızalara sırasında) olarak

Hello DocumentDB API, bu yapılandırma hello parçacığını aşağıdaki gibi görünür:

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

Merhaba uygulaması da hello sırasını tersine tercih edilen bölge ile Merhaba Kuzey Avrupa bölgede dağıtılmış. Diğer bir deyişle, hello Kuzey Avrupa bölge ilk düşük gecikme süresi okuma için belirtilir. Ardından, hello Batı ABD bölgesi olarak hello ikinci tercih edilen bölge, yüksek kullanılabilirlik için bölgesel hataları sırasında belirtilir.

Merhaba aşağıdaki mimarisi diyagramı bölgeli uygulama dağıtımı olduğu Cosmos DB ve hello uygulama yapılandırılmış toobe kullanılabilir dört Azure coğrafi bölgelerde gösterilir.  

![Genel olarak dağıtılmış uygulama dağıtımı Azure Cosmos DB ile](./media/regional-failover/app-deployment.png)

Şimdi, hello Cosmos DB hizmetiyle otomatik yük devretme işlemlerini aracılığıyla bölgesel arızalara nasıl işlediğini konumundaki bakalım. 

## <a id="AutomaticFailovers"></a>Otomatik Yük devretme
Merhaba ender olayda Azure bölgesel kesinti veya veri merkezi kesintisinden, Cosmos DB etkilenen hello bölgede bulunan bir durum tüm Cosmos DB hesaplarıyla yük otomatik olarak tetikler. 

**Okuma bölge kesinti varsa ne olur?**

Etkilenen hello bölgelerinden okuma bir bölgede cosmos DB hesaplarıyla otomatik olarak kendi yazma bölgesinden bağlantısı kesilen ve çevrimdışı olarak işaretli. Merhaba Cosmos DB SDK'ları uygulama tooautomatically sağlayan bir bölgesel Bulma Protokolü bir bölge kullanılabilir olduğunda ve yeniden yönlendirme çağrıları toohello sonraki kullanılabilir bölge hello tercih edilen bölge listesinde okuma algıla. Merhaba hello bölgelerde hiçbiri bölge listesi kullanılabilir tercih edilen, çağrıları otomatik olarak geri toohello geçerli yazma bölge ayrılır. Değişiklik uygulama, kod toohandle bölgesel yerine gerekli değildir. Tüm bu işlem sırasında tutarlılık Cosmos DB tarafından dikkate alınır toobe devam edin.

![Azure Cosmos veritabanı okuma bölge hataları](./media/regional-failover/read-region-failures.png)

Etkilenen hello bölge hello kesintisi kurtarır sonra hello bölge içindeki tüm etkilenen hello Cosmos DB hesaplar hello hizmeti tarafından otomatik olarak kurtarılır. Etkilenen hello bölgede okuma bölge vardı cosmos DB hesapları sonra otomatik olarak geçerli yazma bölge ile eşitleme ve çevrimiçi Aç. Merhaba Cosmos DB SDK'ları hello yeni bölge hello kullanılabilirliğini bulmak ve hello geçerli okuma bölge hello uygulama tarafından yapılandırılmış hello tercih edilen bölge listesi dayalı olarak hello bölge seçili olup olmadığını değerlendirin. Sonraki okuma herhangi bir değişiklik tooyour uygulama kodu gerektirmeden yeniden yönlendirilen toohello kurtarılan bölge ' dir.

**Bir yazma bölge kesinti varsa ne olur?**

Merhaba etkilenen bölge hello geçerli yazma bölge belirtilen Cosmos DB hesabı ise, ardından hello bölge otomatik olarak çevrimdışı olarak işaretlenir. Sonra etkilenen her Cosmos DB hesabı bölge Hello yazma gibi alternatif bir Bölge yükseltilir. Merhaba bölge seçimi siparişi hello Azure portal aracılığıyla Cosmos DB hesaplarınız için tam olarak kontrol edebilirsiniz veya [program aracılığıyla](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange). 

![Azure Cosmos DB için yük devretme öncelikler](./media/regional-failover/failover-priorities.png)

Otomatik Yük devretme sırasındaki Cosmos DB otomatik olarak hello sonraki yazma bölge için belirtilen Cosmos DB seçer hello üzerinde temel hesabı belirtilen öncelik sırası. 

![Azure Cosmos DB'de yazma bölge hataları](./media/regional-failover/write-region-failures.png)

Etkilenen hello bölge hello kesintisi kurtarır sonra hello bölge içindeki tüm etkilenen hello Cosmos DB hesaplar hello hizmeti tarafından otomatik olarak kurtarılır. 

* Önceki yazma bölgelerini etkilenen hello bölgede cosmos DB hesaplarıyla bile hello bölgesinin hello kurtarma işleminden sonra okuma kullanılabilirlik ile çevrimdışı modda kalır. 
* Bu bölge toocompute hello geçerli yazma bölgede kullanılabilir hello veri karşılaştırarak hello kesintisi sırasında çoğaltılmamış tüm yazma sorgulayabilirsiniz. Uygulamanızın Hello gereksinimlerine göre birleştirme ve/veya Çakışma çözümlemesi ve hello son değişiklikleri geri toohello geçerli yazma bölge kümesinin yazma. 
* Birleştirme değişiklikleri tamamladıktan sonra etkilenen hello bölge tekrar çevrimiçi kaldırarak ve hello bölge tooyour Cosmos DB hesabı yeniden ekleniyor kullanıma sunabilirsiniz. Merhaba bölge geri eklendikten sonra geri hello yazma bölgeye el ile bir yük devretme hello Azure portal aracılığıyla gerçekleştirerek yapılandırabilirsiniz ya da [program aracılığıyla](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).

## <a id="ManualFailovers"></a>El ile yük devretme

Ayrıca belirli bir Cosmos DB hesaba bölgesini hello varolan okuma bölgelerinin tooone el ile bir dinamik olarak değiştirilebilir tooautomatic yerine, geçerli hello yazma. El ile yük devretme işlemlerini hello Azure portal başlatılabilir veya [program aracılığıyla](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate). 

El ile yük devretme sağlamak **sıfır veri kaybı** ve **sıfır kullanılabilirlik** kaybına ve düzgün bir şekilde hello eski aktarımı yazma durumundan yazma bölge toohello yeni bir hello Cosmos DB hesabı belirtilen için. Otomatik Yük devretme işlemlerini Cosmos DB SDK otomatik olarak hello gibi tanıtıcıları yazma: bölge el ile yük devretme işlemleri sırasında değiştirir ve çağrıları otomatik olarak yeniden yönlendirilen toohello yeni yazma bölgesi olmasını sağlar. Kod veya yapılandırma değişiklik, uygulama toomanage yerine gerekli değildir. 

![El ile yük devretme işlemlerini Azure Cosmos veritabanı](./media/regional-failover/manual-failovers.png)

Burada el ile yük devretme yararlı olabilir hello yaygın senaryolardan bazıları şunlardır:

**Başlangıç saati modelini izler**: hello günün başlangıç zamanı temel alınarak tahmin edilebilir trafik düzenlerini uygulamalarınız varsa, hello günün zamana dayalı hello yazma durumu toohello en aktif coğrafi bölge düzenli aralıklarla değiştirebilirsiniz.

**Hizmet Güncelleştirmesi**: belirli genel dağıtılmış uygulama dağıtımı, planlanan hizmet güncelleştirmesi sırasında trafiği toodifferent bölge trafik Yöneticisi aracılığıyla yeniden yönlendirilmesine gerektirebilir. Artık böyle uygulama dağıtımı el ile yük devretme tookeep hello yazma durumu toohello bölge burada var olduğuna toobe etkin trafiği hello hizmet güncelleştirme penceresi sırasında kullanabilirsiniz.

**İş devamlılığı ve olağanüstü durum kurtarma (BCDR) ve yüksek kullanılabilirlik ve olağanüstü durum kurtarma (HADR) ayrıntısına**: çoğu kuruluş uygulamaları kendi geliştirme ve sürüm işleminin bir parçası iş sürekliliği testleri içerir. BCDR HADR sınama ise genellikle uyumluluk sertifikalarından önemli bir adım ve bölgesel kesintileri hello durumda hizmet kullanılabilirliği güvence altına alır. Merhaba BCDR hazırlık Cosmos DB depolama için el ile bir yük devretme Cosmos DB hesabınızın tetikleme ve/veya ekleme ve bir bölge dinamik olarak kaldırma kullanan uygulamalar test edebilirsiniz.

Bu makalede, Cosmos DB nasıl elle ve otomatik yük devretme iş ve, Cosmos DB hesaplarının ve uygulamaların toobe genel olarak kullanılabilir nasıl yapılandırabileceğinizi gözden. Cosmos DB'ın genel çoğaltma desteği kullanarak, uçtan uca gecikme geliştirmek ve hatta hello olayda bölge hatalar yüksek oranda kullanılabilir olduğundan emin olun. 

## <a id="NextSteps"></a>Sonraki Adımlar
* Cosmos DB nasıl desteklediği hakkında bilgi edinin [genel dağıtım](distribute-data-globally.md)
* Hakkında bilgi edinin [Azure Cosmos DB ile genel tutarlılık](consistency-levels.md)
* Azure Cosmos veritabanı kullanarak birden fazla bölge ile geliştirme [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md)
* Bilgi nasıl toobuild [bölgeli yazan mimarileri](multi-region-writers.md) Azure DocumentDB ile

