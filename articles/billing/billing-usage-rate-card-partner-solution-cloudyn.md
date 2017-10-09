---
title: "aaaMicrosoft Azure kullanım ve RateCard API'leri etkinleştirin Cloudyn tooProvide ITFM müşteriler için | Microsoft Docs"
description: "Microsoft Azure fatura ortağında Cloudyn, kendi üründe hello Azure faturalama API'leri tümleştirme deneyimlerini benzersiz bir perspektif sağlar.  Bu, özellikle kullanarak/Cloudyn için Azure Services çalışırken ilginizi çekiyor mu Azure ve Cloudyn müşteriler için kullanışlıdır."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a>Microsoft Azure kullanım ve RateCard API'leri etkinleştirin Cloudyn tooProvide ITFM müşteriler için
Cloudyn, bir Microsoft geliştirme iş ortağı ve bulut yönetim özellikleri, baştaki sağlayıcısının Microsoft Azure kaynak kullanımı ve RateCard API'leri hello yeni özel önizlemesi için seçildi.  Merhaba kullanım API'si tooestimated Azure tüketim verilere erişmek için bir abonelik sağlar. Merhaba RateCard API tüm fiyatlandırma bilgilerine olmayan - Kurumsal Anlaşma EA müşteriler için tüm Azure hizmetleri sağlar. Bu API'leri birlikte tümleşik Cloudyn tarafından sağlanan gibi BT Finansal Yönetimi (ITFM) araçları giriş için bir tam bilgi temel sunar.

## <a name="introduction"></a>Giriş
Merhaba kullanım API'si verilerini hello RateCard API verilerle sözde "çarpma" Merhaba (kullanım [birimler] [$unit] fiyat ayrıntılı kullanım ve maliyet =) hello en ayrıntılı, doğru ve güvenilir için faturalama bilgilerini kullanılabilir Azure bugün oluşturur.

![ITFM genel bakış][1]

Bu API'leri kullanan müşterilerin kullanım ve maliyetleri Cloudyn tooanalyze müşteri hesapları çeşitli ITFM görevleri bir basit ve programlı bir şekilde ve tooperform müşterilerine için izin vererek, önemli bilgiler sağlar.

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a>Merhaba RateCard ile Cloudyn ve kullanım API tümleştirme
Merhaba RateCard API--bölge bilgileri, para birimi ve yerel ayar--ancak hello Azure önerme hello müşteri hello türünü (Kullandıkça Öde, eski 6 ve 12 aylık taahhütte kullanarak belirtir OfferDurableID biridir en önemli gibi çeşitli giriş parametreleri gerektirir planları, MSDN tekliflerini, MPN teklifleri, promosyon teklifleri ve diğerleri). Merhaba OfferDurableID hello bulunabilir [Azure kullanım ve fatura portalı](https://account.windowsazure.com/Subscriptions), hello "Teklif abonelik verilen kimliği" Merhaba altında.

Kayıt sırasında [Cloudyn Azure](https://www.cloudyn.com/microsoft-azure/) Hizmetleri, müşterilerin Cloudyn toopull hello RateCard API aracılığıyla ilgili fiyatlandırma bilgileri sağlar ve OfferDurableID kodunu ekleyebilirsiniz.  Merhaba farklı teklifleri türleri hakkında bilgi bir hello bulunabilir [Microsoft Azure Teklif Ayrıntıları](https://azure.microsoft.com/support/legal/offer-details/) sayfası.

![Cloudyn ITFM altyapısı genel bakış][2]

Toplama toohello Azure Performans Uyarısı API, toocreate ek Katmanlar görselleştirme, analiz, kullanım ve RateCard API'leri, her ikisi de hello Cloudyn kullanır raporlama, yönetim ve uygulanabilir öneriler, Azure müşterilerin güvenilir sağlama maliyeti Kurumsal bulut ITFM aracı.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Kullanım ve RateCard API tümleştirmesi etkin Cloudyn ITFM kullanım örnekleri
Ortak Cloudyn ITFM kullanım kullanımı etkinleştirilmiş ve RateCard API'leri şunları içerir:

* **Analiz maliyetiyle** -bulut sağlar tooany boyut (sağlayıcısı, hizmeti, hesap, bölge vb.) tanımlayan yerel bozuk toobe maliyetleri. Hello Azure kullanım ve RateCard API'leri Bu kolay bir görev hello en ayrıntılı kullanım ve maliyet verilerini sonra gruplandırılmış ve Cloudyn tarafından filtre ve toohello kullanıcı, bir grafik veya Tablo formunda sunulan hesap başına dökümünü sağlayarak yapın.

![Analiz pasta grafik maliyet][3]

* **Ayırma 360 maliyet** -etkinleştirir Finans BT yöneticileri toouncover hello gerçek maliyet ve çözümleme, sürücüler ve bunların bulut dağıtım eğilimleri. Daha fazla tooeasily ilişkilendirme dağıtım giderleri Departmanlar, Departmanlar, bölgeler ve daha fazla ile yöneticileri sağlayan bulut maliyetleri eşi görülmemiş Öngörüler sağlayarak ve kurumsal ödemelerin ve showbacks kolaylaştırmanın. Hello Azure kullanım ve RateCard API'leri yöntemleri ve etiketlenmemiş veya untaggable kaynaklarını ayırma için iş mantığı tanımlayarak hello API'leri tamamlar giriş tooCloudyn's maliyet ayırma altyapısı işlevini görür.

![Maliyet ayırma 360 grafik][4]

* **Düşük maliyetli boyutlandırma** -az sanal makineler, böylece büyük boyutlu veya aşırı sağlanan makine hello Müşteri'nin giderlerini azaltmak için boyutlandırmaya öneriler sağlar. Bunu sanal makine CPU ve RAM ölçümleri (aracılığıyla performans API), çalışma zamanı (aracılığıyla kullanım API'si) ve Maliyet (RateCard API) aracılığıyla saatlik inceleyerek yapar. Cloudyn sonra az CPU veya RAM kaynaklara (performans) bağlı boyutlandırmaya önerileri sağlar ve tahmini tasarrufları hello gerçek zaman-kullanımı (kullanımı) hello tarafından hello VM'ler arasında hello fiyat delta (RateCard) çarparak hesaplar az makine.

![Düşük maliyetli boyutlandırma][5]

* **Bulut bağlantı noktası oluşturma önerileri** -bulut üzerinde finansal çözmelerini sağlayan taşıma. Kullanıcının geçerli maliyetleri büyük bulut Satıcılar'dağıtılan bulut kaynaklarının inceler ve Azure üzerinde eşdeğer bir dağıtım toohello maliyetini karşılaştırır. Ardından ayrıntılı, sağlar başına-kaynak, mali önerileri tooAzure taşıma tabanlı. (Performans ölçümleri ve kullanıcı tercihlerine bağlı olarak) Azure ile ilgili gerekli hello eşdeğer dağıtım değerlendiriliyor sonra Cloudyn Azure'da hello RateCard API tooevaluate hello hello eşdeğer dağıtım maliyetini kullanır.
* **Performans raporları** -Azure'nın performans API tarafından etkinse, bu raporları CPU ve RAM kullanımını özelliklerinden bir dizi toooptimization öneriler sağlar. Ortalama CPU kullanımı örneği dökümünü sunan bir örnek kullanımı raporu örneği aşağıdadır.

![Performans raporları][6]

* **Kategori Yöneticisi** -toounorganized bulut kaynakları sipariş getirir Cloudyn uygulamasında güçlü bir özelliktir. Kullanıcıların hello özgürlük toocreate, etkili ölçme ve uygun olarak iş uygulamaları, raporlama için kendi benzersiz kategorileri (etiketleri) sağlar. Ayrıca, kullanıcılar kolayca düzenleyen ve (yani, yazım hatalarını ve diğer tutarsızlıklar) tutarsız etiketleme kategorilere ayırmak ve doğru maliyet attribution etiketlenmemiş kaynakları otomatik olarak algıla.

![Kategori Yöneticisi][7]

## <a name="video"></a>Video
Bir Azure müşteri Azure ve hello Azure faturalama API'leri, Azure tüketim verilerine ilişkin toogain bilgiler için Cloudyn nasıl kullanabileceğinizi gösteren kısa bir video aşağıdadır.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
* Ücretsiz Başlat [Cloudyn Azure](https://www.cloudyn.com/microsoft-azure/) nasıl edinebilirsiniz deneme toosee maliyet özelleştirilmiş raporlama ve analiz Microsoft Azure bulut dağıtımınız için saydamlığı.
* Bkz: [Microsoft Azure kaynak tüketimini Öngörüler elde](billing-usage-rate-card-overview.md) hello Azure kaynak kullanımı ve RateCard API'leri genel bakış.
* Merhaba denetleyin [Azure faturalama REST API Başvurusu](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) hem API'ler hakkında daha fazla bilgi için Azure Resource Manager hello tarafından sağlanan API'leri hello kümesinin parçası olan.
* Bizim Microsoft Azure fatura API kod örnekleri sağ hello örnek koda toodive kullanmak isterseniz, denetleme [Azure Kod örnekleri](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Daha Fazla Bilgi Edinin
* Lütfen Microsoft Azure Kurumsal Anlaşma (Kurumsal Sözleşme) teklifleri hakkında daha fazla toolearn adresini ziyaret edin [lisans Azure hello kuruluş için](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Merhaba bkz [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md) makale toolearn hello Azure Resource Manager hakkında daha fazla bilgi.
* Bulut bir anlayış sağlamasını içinde gerekli toohelp harcadığı hello suite araçlar hakkında ek bilgi için lütfen çok başvurun Gartner makale [BT Finansal Yönetimi (ITFM) araçları için Pazar Kılavuzu](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
