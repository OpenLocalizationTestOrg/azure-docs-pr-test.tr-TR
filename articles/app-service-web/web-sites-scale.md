---
title: "bir Azure uygulamasında yukarı aaaScale | Microsoft Docs"
description: "Bilgi nasıl tooscale bir uygulamada Azure App Service tooadd kapasite ve özellikleri ayarlama."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a>Bir Azure uygulamasında ölçeklendirin
Bu makale size nasıl gösterir tooscale uygulamanızı Azure App Service'te. Yukarı ölçeklendirme, ölçeklendirme için iki iş akışlarını vardır ve ölçek genişletme ve bu makalede hello ölçek büyütme iş akışı açıklanır.

* [Ölçeği artırma](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): daha fazla CPU, bellek, disk alanı ve ayrılmış sanal makine (VM), özel etki alanları ve sertifikalar, hazırlama yuvaları, otomatik ölçeklendirme ve daha fazla özellikten alın. Fiyatlandırma katmanı, uygulamanızın ait olduğu uygulama hizmeti planının hello değiştirerek ölçeği.
* [Ölçeği genişletme](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): uygulamanızı çalıştıran VM örneği hello sayısını artırın.
  Fiyatlandırma katmanınıza bağlı 20 örnekleri kadar tooas ölçeklendirebilirsiniz. [Uygulama hizmeti ortamları](../app-service/app-service-app-service-environments-readme.md) içinde **Premium** katmanı daha fazla genişleme sayısı too50 örneklerinizi artırın. Genişletme hakkında daha fazla bilgi için bkz: [örnek sayısı el ile veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md). Bul nasıl otomatik olarak tooscale örnek sayısı olan toouse otomatik ölçeklendirmeyi göre önceden tanımlanmış kurallar ve zamanlamaları giden.

Ölçek ayarları Al yalnızca saniye tooapply hello ve tüm uygulamaları etkiler, [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
Bunlar, toochange kodunuzu gerektirmez veya uygulamanızın yeniden dağıtın.

Merhaba fiyatlandırma ve tek tek uygulama hizmeti planları özellikleri hakkında daha fazla bilgi için bkz: [App Service fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Bir uygulama hizmeti planında hello geçiş yapmadan önce **serbest** katmanı, hello önce kaldırmalısınız [harcama limitlerini](https://azure.microsoft.com/pricing/spending-limits/) Azure aboneliğiniz için yerinde. bkz. Microsoft Azure uygulama hizmeti aboneliğiniz için tooview veya değiştirme seçenekleri [Microsoft Azure abonelikleri][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Fiyatlandırma katmanınızı ölçeklendirme
1. Merhaba, tarayıcınızı açmak [Azure portal][portal].
2. Uygulamanızın dikey penceresinde tıklayın **tüm ayarları**ve ardından **ölçeği Artır**.
   
    ![Azure uygulamanızı kurma tooscale gidin.][ChooseWHP]
3. Katmanınızı seçin ve ardından **seçin**.
   
    Merhaba **bildirimleri** flash yeşil sekmesi **başarı** hello işlemi tamamlandıktan sonra.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>İlgili kaynaklar ölçeklendirme
Uygulamanızı Azure SQL veritabanı ya da Azure depolama gibi diğer hizmetler yapılandırmasanız ihtiyaçlarınıza göre bu kaynakları ölçeklendirebilirsiniz. Bu kaynaklar uygulama hizmeti planı hello ile ölçeklenmez ve ayrı olarak ölçeklendirilmesi gerekir.

1. İçinde **Essentials**, hello tıklatın **kaynak grubu** bağlantı.
   
    ![Azure, uygulamanızın ilgili kaynakları ölçeklendirme](./media/web-sites-scale/RGEssentialsLink.png)
2. Merhaba, **Özet** hello parçası **kaynak grubu** dikey penceresinde, tooscale istediğiniz kaynak bir tıklatın. hello ekran izleyen ve bir Azure depolama kaynağı bir SQL veritabanı kaynak gösterir.
   
    ![Azure uygulamanızı kurma tooresource Grup dikey tooscale gidin](./media/web-sites-scale/ResourceGroup.png)
3. Bir SQL veritabanı kaynağı için tıklatın **ayarları** > **fiyatlandırma katmanı** tooscale hello fiyatlandırma katmanı.
   
    ![Azure uygulamanız için hello SQL veritabanı arka uç ölçeklendirin](./media/web-sites-scale/ScaleDatabase.png)
   
    Ayrıca açabilirsiniz [coğrafi çoğaltma](../sql-database/sql-database-geo-replication-overview.md) SQL veritabanı Örneğiniz için.
   
    Bir Azure depolama kaynağı için tıklatın **ayarları** > **yapılandırma** tooscale depolama seçeneklerini ayarlama.
   
    ![Azure uygulamanız tarafından kullanılan hello Azure depolama hesabı ölçeklendirin](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>Geliştirici özellikleri hakkında bilgi edinin
Fiyatlandırma katmanı hello bağlı olarak, hello aşağıdaki Geliştirici yönelimli özellikler mevcuttur:

### <a name="bitness"></a>Verileri
* Merhaba **temel**, **standart**, ve **Premium** katmanları 64-bit ve 32-bit uygulamalarını destekler.
* Merhaba **serbest** ve **paylaşılan** plan katmanlarını yalnızca 32-bit uygulamaları destekler.

### <a name="debugger-support"></a>Hata ayıklayıcı desteği
* Hata ayıklayıcı desteği Merhaba kullanılabilir **serbest**, **paylaşılan**, ve **temel** modları uygulama hizmeti planı başına bir bağlantıda.
* Hata ayıklayıcı desteği Merhaba kullanılabilir **standart** ve **Premium** sırasında beş eşzamanlı bağlantı uygulama hizmeti planı başına modları.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>Diğer özellikler hakkında bilgi edinin
* Planları, fiyatlandırma dahil olmak üzere ve özellikleri ilgi tooall kullanıcıların (geliştiriciler de dahil), tüm özellikleri hello App Service içinde kalan hello hakkında ayrıntılı bilgi için bkz [App Service fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/) hemen oluşturabileceğiniz bir kısa süreli başlangıç web uygulaması App Service içinde. Kredi kartı gerekmez ve hiçbir taahhüt yoktur.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Sonraki adımlar
* Azure ile çalışmaya tooget bkz [Microsoft Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Fiyatlandırma, destek ve SLA hakkında daha fazla bilgi için bağlantılar aşağıdaki hello ziyaret edin.
  
    [Veri aktarımları fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Microsoft Azure destek planları](https://azure.microsoft.com/support/plans/)
  
    [Hizmet Düzeyi Sözleşmeleri](https://azure.microsoft.com/support/legal/sla/)
  
    [SQL veritabanı fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Sanal makine ve bulut hizmeti boyutları Microsoft Azure][vmsizes]
  
    [Uygulama hizmeti fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/app-service/)
  
    [Uygulama hizmeti fiyatlandırma ayrıntıları - SSL bağlantıları](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* En iyi yöntemler, ölçeklenebilir ve esnek bir mimari oluşturmak gibi Azure App Service hakkında bilgi için bkz: [en iyi uygulamalar: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).
* Uygulama hizmeti uygulamaları ölçeklendirme hakkında daha fazla videolar için kaynakları aşağıdaki hello bakın:
  
  * [Zaman tooScale - Stefan Schackow ile Azure Web siteleri](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [Azure Web siteleri, CPU ölçeklendirme otomatik veya zamanlanmış - Stefan Schackow](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [-Stefan Schackow ile nasıl Azure Web siteleri ölçek](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
