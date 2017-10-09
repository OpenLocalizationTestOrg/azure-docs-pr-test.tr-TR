---
title: "aaaCreate hello portalında bir Azure Search Hizmeti | Microsoft Docs"
description: "Azure Search Hizmeti hello portalında sağlayın."
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
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a>Merhaba portalda Azure Search hizmeti oluşturma

Bu makalede nasıl toocreate veya sağlama Azure Search Hizmeti hello Portalı'nda açıklanmaktadır. PowerShell yönergeleri için bkz: [PowerShell ile yönetme Azure Search](search-manage-powershell.md).

## <a name="subscribe-free-or-paid"></a>(Ücretsiz veya Ücretli) abone olma

[Ücretsiz bir Azure hesabı açın](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ve Azure Hizmetleri Ücretli ücretsiz krediler tootry çıkışı kullanın. Krediler bitmiş olsa, hello hesabı sürdürebilir ve Web siteleri gibi toouse ücretsiz Azure hizmetlerinden devam edin. Açıkça ayarlarınızı değiştirip ücret toobe isteyin sürece kredi kartınızdan asla ücret kesilir.

Alternatif olarak, [MSDN abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Bir MSDN aboneliğiniz, ücretli Azure hizmetlerinizi kullanabildiğiniz her ay krediler sağlar. 

## <a name="find-azure-search"></a>Azure Arama Bul
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba artı işareti ("+") içinde hello üst köşe sol tıklayın.
3. Seçin **Web + mobil** > **Azure arama**.

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a>Ad hello hizmeti ve URL uç noktası

Bir hizmet adı API çağrıları karşı verildiği hello URL uç noktası'nın bir parçasıdır. Hello hizmet adınızı yazın **URL** alan. 

Hizmet adı gereksinimleri:
   * uzunluğu 2 ile 60 karakter
   * küçük harf, rakam veya kısa çizgi ("-")
   * hiçbir kısa çizgi ("-") ilk 2 karakteri veya son tek karakter hello gibi
   * Art arda gelen tirelere ("--")

## <a name="select-a-subscription"></a>Abonelik seçin
Birden fazla aboneliğiniz varsa, veri veya dosya depolama hizmetleri de sahip seçin. Azure arama otomatik algıla Azure Table ve Blob Depolama, SQL Database ve Azure Cosmos DB aracılığıyla dizin oluşturma için *dizin oluşturucular*, ancak yalnızca hello hizmetler için aynı abonelik.

## <a name="select-a-resource-group"></a>Kaynak grubu seç
Bir kaynak grubu, Azure Hizmetleri ve birlikte kullanılan kaynakları koleksiyonudur. Azure Search tooindex bir SQL veritabanı kullanıyorsanız, örneğin, ardından her iki hizmet hello parçası olmalıdır aynı kaynak grubu.

> [!TIP]
> Bir kaynak grubunu silme hello Hizmetleri içindeki siler. Merhaba proje bittikten sonra birden çok hizmet yararlanarak, bunların tümünün hello koyma prototip projeleri için aynı kaynak grubunu temizleme kolaylaştırır. 

## <a name="select-a-hosting-location"></a>Bir barındırma konumu seçin 
Bir Azure hizmeti Azure arama Merhaba Dünya veri merkezlerinde barındırılabilir. Unutmayın [fiyatlar farklı](https://azure.microsoft.com/pricing/details/search/) coğrafyaya.

## <a name="select-a-pricing-tier-sku"></a>(SKU) bir fiyatlandırma katmanı seçin
[Azure arama şu anda birden çok fiyatlandırma katmanında sunulan](https://azure.microsoft.com/pricing/details/search/): ücretsiz, temel veya standart. Her katman kendi sahip [kapasite ve sınırlar](search-limits-quotas-capacity.md). Bkz: [bir fiyatlandırma katmanı SKU seçin veya](search-sku-tier.md) Kılavuzu.

Bu kılavuzda, biz hello standart katmanı hizmetimizi için seçtiniz.

## <a name="create-your-service"></a>Hizmet oluşturma

Oturum zaman toopin hizmet toohello panonuz kolay erişim için unutmayın.

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a>Hizmetinizi ölçeklendirme
Bu işlem birkaç dakika toocreate (15 dakika veya daha fazla hello katmanına bağlı olarak) bir hizmet alabilir. Hizmetinizi sağlandıktan sonra toomeet ölçeklendirebilirsiniz gereksinimlerinizi. Azure Search hizmetinizin hello standart katmanı seçtiğinden hizmetinizi iki boyut ölçeklendirebilirsiniz: çoğaltmaları ve bölümler. Merhaba temel katmana tercih etmiş, çoğaltmaları yalnızca ekleyebilirsiniz. Merhaba ücretsiz hizmet sağlanan, Ölçek kullanılabilir değil.

***Bölümler*** hizmet toostore ve daha fazla belge arama izin verir.

***Çoğaltmaları*** hizmet toohandle arama sorguları daha yüksek yükü izin.

> [!Important]
> Bir hizmet olmalıdır [salt okunur SLA için 2 çoğaltma ve 3 çoğaltmaları için okuma/yazma SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

1. Tooyour arama hizmeti dikey penceresinde hello Azure portalına gidin.
2. Merhaba sol gezinti bölmesinde seçin **ayarları** > **ölçek**.
3. Merhaba slidebar tooadd çoğaltmaları veya bölümleri kullanın.

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> Her katman farklı olan [sınırları](search-limits-quotas-capacity.md) hello arama birimi tek bir hizmet olarak izin verilen toplam sayısı (çoğaltmaları * bölümleri toplam arama birimi =).

## <a name="when-tooadd-a-second-service"></a>Zaman tooadd ikinci bir hizmeti

Müşteriler büyük bir çoğunluğu kullanmak hello sağlayan bir katmanını sağlanan tek hizmet [sağ kaynakları bakiyesini](search-sku-tier.md). Bir hizmet birden çok dizin, konu toohello barındırabilir [seçtiğiniz hello katmanının maksimum sınırları](search-capacity-planning.md), başka bir yalıtılmış her dizine sahip. Yönlendirilmiş tooone dizin olmalıdır, diğer yanlışlıkla veya kasıtlı veri alma hello olasılığını en aza hello aynı dizinler yalnızca Azure Search'te istekleri için hizmet.

Müşterilerin çoğu yalnızca bir hizmet kullansa da, hizmet artıklık işletimsel gereksinimlerini hello aşağıdaki eklerseniz gerekli olabilir:

+ Olağanüstü Durum Kurtarma (veri merkezi kesintisinden). Azure arama kesinti hello olayı içinde anlık yük devretme sağlamaz. Öneriler ve yönergeler için bkz: [Hizmet Yönetim](search-manage.md).
+ Araştırmanızı çoklu kiracı model ek hizmetler hello en uygun tasarımı olduğunu belirledi. Daha fazla bilgi için bkz: [çoklu kiracı için tasarım](search-modeling-multitenant-saas-applications.md).
+ Genel olarak dağıtılan uygulamalar için birden çok bölgeleri toominimize gecikme uygulamanızın uluslararası trafiği Azure Search örneğini gerektirebilir.

> [!NOTE]
> Azure Search'te dizin oluşturma ve sorgulama iş yükleri kurabilmeleri olamaz; Bu nedenle, birden fazla hizmet ayrı iş yükleri için hiçbir zaman oluşturursunuz. Bir dizin kapsamda oluşturulan hello hizmette her zaman sorgulanan (bir hizmetinde bir dizin oluşturamaz veya tooanother Kopyala).
>

İkinci bir hizmet yüksek kullanılabilirlik için gerekli değildir. Yüksek kullanılabilirlik sorgular için 2'yi kullanın ya da daha fazla yinelemede aynı hizmet hello elde edilir. Çoğaltma güncelleştirmeleri sıralı, bir hizmet güncelleştirmesi gezinirken en az bir işlem olduğu anlamına gelir. Açık kalma süresi hakkında daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## <a name="next-steps"></a>Sonraki adımlar
Azure Search Hizmeti sağladıktan sonra çok hazır olduğunuz[bir dizin tanımla](search-what-is-an-index.md) karşıya yükleme ve verilerinizi arama.

tooaccess hello hizmetinden kod veya komut dosyası, hello URL'si sağlayın (*hizmet adı*. search.windows.net) ve anahtar. Yönetici anahtarlarına tam erişim; Sorgu anahtarları salt okunur erişim verin. Bkz: [toouse Azure arama nasıl .NET](search-howto-dotnet-sdk.md) tooget başlatıldı.

Bkz: [oluşturmak ve ilk dizininizi sorgulama](search-get-started-portal.md) portal tabanlı hızlı bir öğretici.

