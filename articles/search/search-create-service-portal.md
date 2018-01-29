---
title: "Portalda Azure Search hizmeti oluşturma | Microsoft Docs"
description: "Portalda Azure Search Hizmeti sağlayın."
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 11/07/2017
ms.author: heidist
ms.openlocfilehash: b31844dd0dad1168b12d91ce536589099ab16a7e
ms.sourcegitcommit: e19f6a1709b0fe0f898386118fbef858d430e19d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/13/2018
---
# <a name="create-an-azure-search-service-in-the-portal"></a>Portalda Azure Search hizmeti oluşturma

Oluşturma veya bir Azure Search Hizmeti Portalı'nda sağlamak öğrenin. 

PowerShell tercih ediyorsunuz? Azure Kaynak Yöneticisi'ni [hizmet şablonu](https://azure.microsoft.com/resources/templates/101-azure-search-create/). Başlarken Yardım için bkz: [PowerShell ile yönetme Azure Search](search-manage-powershell.md) arka planı için.

## <a name="subscribe-free-or-paid"></a>(Ücretsiz veya Ücretli) abone olma

[Ücretsiz bir Azure hesabı açın](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ve Ücretli Azure hizmetlerini denemek için ücretsiz krediler kullanın. Krediler bitmiş olsa, hesabı sürdürebilir ve Web siteleri gibi ücretsiz Azure hizmetlerini kullanmaya devam edin. Açıkça ayarlarınızı değiştirip ücretlendirme sürece kredi kartınızdan asla ücret kesilir.

Alternatif olarak, [MSDN abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Bir MSDN aboneliğiniz, ücretli Azure hizmetlerinizi kullanabildiğiniz her ay krediler sağlar. 

## <a name="find-azure-search"></a>Azure Arama Bul
1. [Azure Portal](https://portal.azure.com/) oturum açın.
2. Artı işareti ("+") sol üst köşede'ı tıklatın.
3. Seçin **Web + mobil** > **Azure arama**.

![](./media/search-create-service-portal/find-search3.png)

## <a name="name-the-service-and-url-endpoint"></a>Hizmet ve URL uç adı

Bir hizmet adı karşı hangi API çağrıları yayımlanan URL uç parçasıdır: `https://your-service-name.search.windows.net`. Hizmet adınızı girin **URL** alan. 

Hizmet adı gereksinimleri:
   * Search.windows.net ad alanı içinde benzersiz olmalıdır
   * uzunluğu 2 ile 60 karakter
   * Küçük harf, rakam veya kesik çizgi kullanın ("-")
   * Tireler kaçının ("-") ilk 2 karakteri veya son tek karakter olarak
   * Art arda gelen tirelere ("--") her yerden

## <a name="select-a-subscription"></a>Abonelik seçin
Birden fazla aboneliğiniz varsa, veri veya dosya depolama hizmetleri de sahip seçin. Azure arama otomatik algıla Azure Table ve Blob Depolama, SQL Database ve Azure Cosmos DB aracılığıyla dizin oluşturma için [ *dizin oluşturucular*](search-indexer-overview.md), ancak yalnızca aynı abonelik içindeki Hizmetleri.

## <a name="select-a-resource-group"></a>Kaynak grubu seç
Bir kaynak grubu, Azure Hizmetleri ve birlikte kullanılan kaynakları koleksiyonudur. Örneğin, bir SQL veritabanı dizini oluşturmak için Azure Search kullanıyorsanız, her iki hizmet aynı kaynak grubunun parçası olmalıdır.

> [!TIP]
> Bir kaynak grubunu silme içindeki Hizmetler siler. Proje bittikten sonra birden çok hizmet kullanılarak prototip projeleri için bunların tümünün aynı kaynak grubunda koyma temizleme kolaylaştırır. 

## <a name="select-a-hosting-location"></a>Bir barındırma konumu seçin 
Bir Azure hizmeti Azure arama dünyanın veri merkezlerinde barındırılabilir. Unutmayın [fiyatlar farklı](https://azure.microsoft.com/pricing/details/search/) coğrafyaya.

## <a name="select-a-pricing-tier-sku"></a>(SKU) bir fiyatlandırma katmanı seçin
[Azure arama şu anda birden çok fiyatlandırma katmanında sunulan](https://azure.microsoft.com/pricing/details/search/): ücretsiz, temel veya standart. Her katman kendi sahip [kapasite ve sınırlar](search-limits-quotas-capacity.md). Bkz: [bir fiyatlandırma katmanı SKU seçin veya](search-sku-tier.md) Kılavuzu.

Bu kılavuzda, biz hizmetimizi için standart katmana seçtiniz.

Bir fiyatlandırma katmanı hizmeti oluşturulduktan sonra değiştirilemez. Daha yüksek veya düşük katmanı daha sonra gerekirse, hizmet yeniden oluşturmanız gerekir.

## <a name="create-your-service"></a>Hizmet oluşturma

Oturum zaman Panoya hizmetiniz kolay erişim için PIN unutmayın.

![](./media/search-create-service-portal/new-service3.png)

## <a name="scale-your-service"></a>Hizmetinizi ölçeklendirme
(15 dakika veya daha fazla katmanı bağlı olarak) bir hizmet oluşturmak için birkaç dakika sürebilir. Hizmetinizi sağlandıktan sonra gereksinimlerinizi karşılayacak şekilde ölçeklendirebilirsiniz. Azure Search hizmetiniz için standart katmana seçtiğinden hizmetinizi iki boyut ölçeklendirebilirsiniz: çoğaltmaları ve bölümler. Temel katman tercih etmiş, çoğaltmaları yalnızca ekleyebilirsiniz. Ücretsiz hizmeti sağlanan, Ölçek kullanılabilir değil.

***Bölümler*** depolamak ve daha fazla belgelerde arama hizmetinizi izin.

***Çoğaltmaları*** hizmetinizin arama sorguları, daha yüksek bir yükü işlemek için izin verin.

> [!Important]
> Bir hizmet olmalıdır [salt okunur SLA için 2 çoğaltma ve 3 çoğaltmaları için okuma/yazma SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

1. Azure Portalı'ndaki arama hizmeti sayfanıza gidin.
2. Sol gezinti bölmesinde seçin **ayarları** > **ölçek**.
3. Slidebar çoğaltmalar veya bölüm eklemek için kullanın.

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> Her katman farklı olan [sınırları](search-limits-quotas-capacity.md) arama birimi tek bir hizmet olarak izin verilen toplam sayısı (çoğaltmaları * bölümleri toplam arama birimi =).

## <a name="when-to-add-a-second-service"></a>İkinci bir hizmet eklemek ne zaman

Müşteriler büyük bir çoğunluğu kullanmak yalnızca bir hizmet sağlayan bir katmanını sağlanan [sağ kaynakları bakiyesini](search-sku-tier.md). Bir hizmet birden çok dizin, konusu barındırabilir [seçtiğiniz katmanının maksimum sınırları](search-capacity-planning.md), başka bir yalıtılmış her dizine sahip. Azure Search'te istekleri yalnızca aynı hizmetin diğer dizinlerde yanlışlıkla veya kasıtlı veri alımı olasılığını en aza bir dizin için yönlendirilebilir.

Müşterilerin çoğu yalnızca bir hizmet kullansa da, hizmet artıklık işletimsel gereksinimleri şunları içerir, gerekli olabilir:

+ Olağanüstü Durum Kurtarma (veri merkezi kesintisinden). Azure arama, bir kesinti durumunda anlık yük devretme sağlamaz. Öneriler ve yönergeler için bkz: [Hizmet Yönetim](search-manage.md).
+ Araştırmanızı çoklu kiracı model ek hizmetler en uygun tasarımı olduğunu belirledi. Daha fazla bilgi için bkz: [çoklu kiracı için tasarım](search-modeling-multitenant-saas-applications.md).
+ Genel olarak dağıtılan uygulamalar için birden çok bölgeye uygulamanızın uluslararası trafiği gecikme süresi en aza indirmek için Azure Search'te örneği gerektirebilir.

> [!NOTE]
> Azure Search'te dizin oluşturma ve sorgulama iş yükleri kurabilmeleri olamaz; Bu nedenle, birden fazla hizmet ayrı iş yükleri için hiçbir zaman oluşturursunuz. Bir dizin kapsamda oluşturulan hizmette her zaman sorgulanan (bir hizmetinde bir dizin oluşturamaz veya diğerine kopyalamak).
>

İkinci bir hizmet yüksek kullanılabilirlik için gerekli değildir. Aynı hizmeti 2 veya daha fazla çoğaltmaları kullandığınızda sorgular için yüksek kullanılabilirlik elde edilir. Çoğaltma güncelleştirmeleri sıralı, bir hizmet güncelleştirmesi gezinirken en az bir işlem olduğu anlamına gelir. Açık kalma süresi hakkında daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## <a name="next-steps"></a>Sonraki adımlar
Azure Search Hizmeti sağladıktan sonra hazırsınız [bir dizin tanımla](search-what-is-an-index.md) karşıya yükleme ve verilerinizi arama. 

> [!div class="nextstepaction"]
> [Azure Search .NET ile kullanma](search-howto-dotnet-sdk.md)
