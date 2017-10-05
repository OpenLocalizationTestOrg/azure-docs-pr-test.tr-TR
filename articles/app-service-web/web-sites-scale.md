---
title: "Bir Azure uygulamasında ölçeklendirin | Microsoft Docs"
description: "Kapasite ve özellikleri eklemek için Azure App Service'te bir uygulama ölçeklendirin öğrenin."
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
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a>Bir Azure uygulamasında ölçeklendirin
Bu makalede, uygulamanızı Azure App Service'te ölçeklendirme gösterilmektedir. Yukarı ölçeklendirme, ölçeklendirme için iki iş akışlarını vardır ve ölçek genişletme ve bu makalede ölçek büyütme iş akışını açıklar.

* [Ölçeği artırma](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): daha fazla CPU, bellek, disk alanı ve ayrılmış sanal makine (VM), özel etki alanları ve sertifikalar, hazırlama yuvaları, otomatik ölçeklendirme ve daha fazla özellikten alın. Uygulamanızın ait olduğu App Service planının fiyatlandırma katmanını değiştirerek ölçeği.
* [Ölçeği genişletme](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): uygulamanızı çalıştıran VM örneği sayısını artırın.
  Out kadar 20 örneklerine fiyatlandırma katmanınıza bağlı ölçeklendirebilirsiniz. [Uygulama hizmeti ortamları](../app-service/app-service-app-service-environments-readme.md) içinde **Premium** katmanı daha fazla genişleme sayınız 50 örneklerine artırın. Genişletme hakkında daha fazla bilgi için bkz: [örnek sayısı el ile veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md). Vardır, otomatik ölçeklendirme, örnek sayısı otomatik olarak önceden tanımlanmış kurallar ve zamanlamaları göre ölçeklendirme olduğu kullanmak nasıl bulacaksınız.

Ölçek ayarları uygulamak ve tüm uygulamaları etkiler yalnızca saniye sürebilir, [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
Bunlar, uygulamanızın yeniden dağıtın veya kodunuzu değiştirmek gerektirmez.

Fiyatlandırma ve tek tek uygulama hizmeti planları özellikleri hakkında daha fazla bilgi için bkz: [App Service fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Bir uygulama hizmeti planında geçiş yapmadan önce **serbest** katmanı, ilk kaldırmalısınız [harcama limitlerini](https://azure.microsoft.com/pricing/spending-limits/) Azure aboneliğiniz için yerinde. Görüntülemek veya Microsoft Azure uygulama hizmeti aboneliğinizi seçeneklerini değiştirmek için bkz: [Microsoft Azure abonelikleri][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Fiyatlandırma katmanınızı ölçeklendirme
1. Tarayıcınızda açın [Azure portal][portal].
2. Uygulamanızın dikey penceresinde tıklayın **tüm ayarları**ve ardından **ölçeği Artır**.
   
    ![Azure uygulamanızı ölçeklendirmek için gidin.][ChooseWHP]
3. Katmanınızı seçin ve ardından **seçin**.
   
    **Bildirimleri** flash yeşil sekmesi **başarı** işlemi tamamlandıktan sonra.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>İlgili kaynaklar ölçeklendirme
Uygulamanızı Azure SQL veritabanı ya da Azure depolama gibi diğer hizmetler yapılandırmasanız ihtiyaçlarınıza göre bu kaynakları ölçeklendirebilirsiniz. Bu kaynaklar ile uygulama hizmeti planı ölçeklenmez ve ayrı olarak ölçeklendirilmesi gerekir.

1. İçinde **Essentials**, tıklatın **kaynak grubu** bağlantı.
   
    ![Azure, uygulamanızın ilgili kaynakları ölçeklendirme](./media/web-sites-scale/RGEssentialsLink.png)
2. İçinde **Özet** parçası **kaynak grubu** dikey penceresinde, ölçeklendirmek istediğiniz kaynağı tıklatın. Aşağıdaki ekran görüntüsü ve bir Azure depolama kaynağı bir SQL veritabanı kaynak gösterir.
   
    ![Azure uygulamanızı ölçeklendirmek için kaynak grubu dikey penceresine gidin](./media/web-sites-scale/ResourceGroup.png)
3. Bir SQL veritabanı kaynağı için tıklatın **ayarları** > **fiyatlandırma katmanı** fiyatlandırma katmanı için.
   
    ![SQL veritabanı arka ucu Azure uygulamanız için ölçeklendirin](./media/web-sites-scale/ScaleDatabase.png)
   
    Ayrıca açabilirsiniz [coğrafi çoğaltma](../sql-database/sql-database-geo-replication-overview.md) SQL veritabanı Örneğiniz için.
   
    Bir Azure depolama kaynağı için tıklatın **ayarları** > **yapılandırma** depolama seçeneklerinizi ölçeklendirmek için.
   
    ![Azure uygulamanız tarafından kullanılan Azure Storage hesabı ölçeklendirin](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>Geliştirici özellikleri hakkında bilgi edinin
Fiyatlandırma katmanına bağlı olarak aşağıdaki Geliştirici yönelimli özellikler mevcuttur:

### <a name="bitness"></a>Verileri
* **Temel**, **standart**, ve **Premium** katmanları 64-bit ve 32-bit uygulamalarını destekler.
* **Serbest** ve **paylaşılan** plan katmanlarını yalnızca 32-bit uygulamaları destekler.

### <a name="debugger-support"></a>Hata ayıklayıcı desteği
* Hata ayıklayıcı desteği için kullanılabilir **serbest**, **paylaşılan**, ve **temel** modları uygulama hizmeti planı başına bir bağlantıda.
* Hata ayıklayıcı desteği için kullanılabilir **standart** ve **Premium** sırasında beş eşzamanlı bağlantı uygulama hizmeti planı başına modları.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>Diğer özellikler hakkında bilgi edinin
* Planları, fiyatlandırma dahil olmak üzere ve özellikleri (geliştiriciler dahil) tüm kullanıcılara ilgi tüm App Service'te kalan özellikleri hakkında ayrıntılı bilgi için bkz [App Service fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service'i kullanmaya başlamak istiyorsanız, Git [App Service'i deneyin](https://azure.microsoft.com/try/app-service/) hemen oluşturabileceğiniz bir kısa süreli başlangıç web uygulaması App Service içinde. Kredi kartı gerekmez ve hiçbir taahhüt yoktur.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Sonraki adımlar
* Azure ile çalışmaya başlamak için bkz: [Microsoft Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Fiyatlandırma, destek ve SLA hakkında daha fazla bilgi için aşağıdaki bağlantıları ziyaret edin.
  
    [Veri aktarımları fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Microsoft Azure destek planları](https://azure.microsoft.com/support/plans/)
  
    [Hizmet Düzeyi Sözleşmeleri](https://azure.microsoft.com/support/legal/sla/)
  
    [SQL veritabanı fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Sanal makine ve bulut hizmeti boyutları Microsoft Azure][vmsizes]
  
    [Uygulama hizmeti fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/app-service/)
  
    [Uygulama hizmeti fiyatlandırma ayrıntıları - SSL bağlantıları](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* En iyi yöntemler, ölçeklenebilir ve esnek bir mimari oluşturmak gibi Azure App Service hakkında bilgi için bkz: [en iyi uygulamalar: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).
* Uygulama hizmeti uygulamaları ölçeklendirme hakkında daha fazla videolar için aşağıdaki kaynaklara bakın:
  
  * [Azure ile Web siteleri - Stefan Schackow ölçeklendirmek ne zaman](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
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
