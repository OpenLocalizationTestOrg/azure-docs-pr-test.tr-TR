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
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="2cb99-103">Bir Azure uygulamasında ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="2cb99-103">Scale up an app in Azure</span></span>
<span data-ttu-id="2cb99-104">Bu makale size nasıl gösterir tooscale uygulamanızı Azure App Service'te.</span><span class="sxs-lookup"><span data-stu-id="2cb99-104">This article shows you how tooscale your app in Azure App Service.</span></span> <span data-ttu-id="2cb99-105">Yukarı ölçeklendirme, ölçeklendirme için iki iş akışlarını vardır ve ölçek genişletme ve bu makalede hello ölçek büyütme iş akışı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="2cb99-105">There are two workflows for scaling, scale up and scale out, and this article explains hello scale up workflow.</span></span>

* <span data-ttu-id="2cb99-106">[Ölçeği artırma](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): daha fazla CPU, bellek, disk alanı ve ayrılmış sanal makine (VM), özel etki alanları ve sertifikalar, hazırlama yuvaları, otomatik ölçeklendirme ve daha fazla özellikten alın.</span><span class="sxs-lookup"><span data-stu-id="2cb99-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="2cb99-107">Fiyatlandırma katmanı, uygulamanızın ait olduğu uygulama hizmeti planının hello değiştirerek ölçeği.</span><span class="sxs-lookup"><span data-stu-id="2cb99-107">You scale up by changing hello pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="2cb99-108">[Ölçeği genişletme](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): uygulamanızı çalıştıran VM örneği hello sayısını artırın.</span><span class="sxs-lookup"><span data-stu-id="2cb99-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase hello number of VM instances that run your app.</span></span>
  <span data-ttu-id="2cb99-109">Fiyatlandırma katmanınıza bağlı 20 örnekleri kadar tooas ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cb99-109">You can scale out tooas many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="2cb99-110">[Uygulama hizmeti ortamları](../app-service/app-service-app-service-environments-readme.md) içinde **Premium** katmanı daha fazla genişleme sayısı too50 örneklerinizi artırın.</span><span class="sxs-lookup"><span data-stu-id="2cb99-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count too50 instances.</span></span> <span data-ttu-id="2cb99-111">Genişletme hakkında daha fazla bilgi için bkz: [örnek sayısı el ile veya otomatik olarak ölçeklendirme](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="2cb99-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="2cb99-112">Bul nasıl otomatik olarak tooscale örnek sayısı olan toouse otomatik ölçeklendirmeyi göre önceden tanımlanmış kurallar ve zamanlamaları giden.</span><span class="sxs-lookup"><span data-stu-id="2cb99-112">There you will find out how toouse autoscaling, which is tooscale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="2cb99-113">Ölçek ayarları Al yalnızca saniye tooapply hello ve tüm uygulamaları etkiler, [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2cb99-113">hello scale settings take only seconds tooapply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="2cb99-114">Bunlar, toochange kodunuzu gerektirmez veya uygulamanızın yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2cb99-114">They do not require you toochange your code or redeploy your application.</span></span>

<span data-ttu-id="2cb99-115">Merhaba fiyatlandırma ve tek tek uygulama hizmeti planları özellikleri hakkında daha fazla bilgi için bkz: [App Service fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="2cb99-115">For information about hello pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="2cb99-116">Bir uygulama hizmeti planında hello geçiş yapmadan önce **serbest** katmanı, hello önce kaldırmalısınız [harcama limitlerini](https://azure.microsoft.com/pricing/spending-limits/) Azure aboneliğiniz için yerinde.</span><span class="sxs-lookup"><span data-stu-id="2cb99-116">Before you switch an App Service plan from hello **Free** tier, you must first remove hello [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="2cb99-117">bkz. Microsoft Azure uygulama hizmeti aboneliğiniz için tooview veya değiştirme seçenekleri [Microsoft Azure abonelikleri][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="2cb99-117">tooview or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="2cb99-118">Fiyatlandırma katmanınızı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="2cb99-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="2cb99-119">Merhaba, tarayıcınızı açmak [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="2cb99-119">In your browser, open hello [Azure portal][portal].</span></span>
2. <span data-ttu-id="2cb99-120">Uygulamanızın dikey penceresinde tıklayın **tüm ayarları**ve ardından **ölçeği Artır**.</span><span class="sxs-lookup"><span data-stu-id="2cb99-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Azure uygulamanızı kurma tooscale gidin.][ChooseWHP]
3. <span data-ttu-id="2cb99-122">Katmanınızı seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="2cb99-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="2cb99-123">Merhaba **bildirimleri** flash yeşil sekmesi **başarı** hello işlemi tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="2cb99-123">hello **Notifications** tab will flash a green **SUCCESS** after hello operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="2cb99-124">İlgili kaynaklar ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="2cb99-124">Scale related resources</span></span>
<span data-ttu-id="2cb99-125">Uygulamanızı Azure SQL veritabanı ya da Azure depolama gibi diğer hizmetler yapılandırmasanız ihtiyaçlarınıza göre bu kaynakları ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cb99-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="2cb99-126">Bu kaynaklar uygulama hizmeti planı hello ile ölçeklenmez ve ayrı olarak ölçeklendirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cb99-126">These resources are not scaled with hello App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="2cb99-127">İçinde **Essentials**, hello tıklatın **kaynak grubu** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="2cb99-127">In **Essentials**, click hello **Resource group** link.</span></span>
   
    ![Azure, uygulamanızın ilgili kaynakları ölçeklendirme](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="2cb99-129">Merhaba, **Özet** hello parçası **kaynak grubu** dikey penceresinde, tooscale istediğiniz kaynak bir tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2cb99-129">In hello **Summary** part of hello **Resource group** blade, click a resource that you want tooscale.</span></span> <span data-ttu-id="2cb99-130">hello ekran izleyen ve bir Azure depolama kaynağı bir SQL veritabanı kaynak gösterir.</span><span class="sxs-lookup"><span data-stu-id="2cb99-130">hello following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Azure uygulamanızı kurma tooresource Grup dikey tooscale gidin](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="2cb99-132">Bir SQL veritabanı kaynağı için tıklatın **ayarları** > **fiyatlandırma katmanı** tooscale hello fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="2cb99-132">For a SQL Database resource, click **Settings** > **Pricing tier** tooscale hello pricing tier.</span></span>
   
    ![Azure uygulamanız için hello SQL veritabanı arka uç ölçeklendirin](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="2cb99-134">Ayrıca açabilirsiniz [coğrafi çoğaltma](../sql-database/sql-database-geo-replication-overview.md) SQL veritabanı Örneğiniz için.</span><span class="sxs-lookup"><span data-stu-id="2cb99-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="2cb99-135">Bir Azure depolama kaynağı için tıklatın **ayarları** > **yapılandırma** tooscale depolama seçeneklerini ayarlama.</span><span class="sxs-lookup"><span data-stu-id="2cb99-135">For an Azure Storage resource, click **Settings** > **Configuration** tooscale up your storage options.</span></span>
   
    ![Azure uygulamanız tarafından kullanılan hello Azure depolama hesabı ölçeklendirin](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="2cb99-137">Geliştirici özellikleri hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2cb99-137">Learn about developer features</span></span>
<span data-ttu-id="2cb99-138">Fiyatlandırma katmanı hello bağlı olarak, hello aşağıdaki Geliştirici yönelimli özellikler mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="2cb99-138">Depending on hello pricing tier, hello following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="2cb99-139">Verileri</span><span class="sxs-lookup"><span data-stu-id="2cb99-139">Bitness</span></span>
* <span data-ttu-id="2cb99-140">Merhaba **temel**, **standart**, ve **Premium** katmanları 64-bit ve 32-bit uygulamalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="2cb99-140">hello **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="2cb99-141">Merhaba **serbest** ve **paylaşılan** plan katmanlarını yalnızca 32-bit uygulamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="2cb99-141">hello **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="2cb99-142">Hata ayıklayıcı desteği</span><span class="sxs-lookup"><span data-stu-id="2cb99-142">Debugger support</span></span>
* <span data-ttu-id="2cb99-143">Hata ayıklayıcı desteği Merhaba kullanılabilir **serbest**, **paylaşılan**, ve **temel** modları uygulama hizmeti planı başına bir bağlantıda.</span><span class="sxs-lookup"><span data-stu-id="2cb99-143">Debugger support is available for hello **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="2cb99-144">Hata ayıklayıcı desteği Merhaba kullanılabilir **standart** ve **Premium** sırasında beş eşzamanlı bağlantı uygulama hizmeti planı başına modları.</span><span class="sxs-lookup"><span data-stu-id="2cb99-144">Debugger support is available for hello **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="2cb99-145">Diğer özellikler hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2cb99-145">Learn about other features</span></span>
* <span data-ttu-id="2cb99-146">Planları, fiyatlandırma dahil olmak üzere ve özellikleri ilgi tooall kullanıcıların (geliştiriciler de dahil), tüm özellikleri hello App Service içinde kalan hello hakkında ayrıntılı bilgi için bkz [App Service fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="2cb99-146">For detailed information about all of hello remaining features in hello App Service plans, including pricing and features of interest tooall users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="2cb99-147">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/) hemen oluşturabileceğiniz bir kısa süreli başlangıç web uygulaması App Service içinde.</span><span class="sxs-lookup"><span data-stu-id="2cb99-147">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2cb99-148">Kredi kartı gerekmez ve hiçbir taahhüt yoktur.</span><span class="sxs-lookup"><span data-stu-id="2cb99-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="2cb99-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2cb99-149">Next steps</span></span>
* <span data-ttu-id="2cb99-150">Azure ile çalışmaya tooget bkz [Microsoft Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2cb99-150">tooget started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2cb99-151">Fiyatlandırma, destek ve SLA hakkında daha fazla bilgi için bağlantılar aşağıdaki hello ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="2cb99-151">For information about pricing, support, and SLA, visit hello following links.</span></span>
  
    [<span data-ttu-id="2cb99-152">Veri aktarımları fiyatlandırma ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="2cb99-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="2cb99-153">Microsoft Azure destek planları</span><span class="sxs-lookup"><span data-stu-id="2cb99-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="2cb99-154">Hizmet Düzeyi Sözleşmeleri</span><span class="sxs-lookup"><span data-stu-id="2cb99-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="2cb99-155">SQL veritabanı fiyatlandırma ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="2cb99-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="2cb99-156">[Sanal makine ve bulut hizmeti boyutları Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="2cb99-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="2cb99-157">Uygulama hizmeti fiyatlandırma ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="2cb99-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="2cb99-158">Uygulama hizmeti fiyatlandırma ayrıntıları - SSL bağlantıları</span><span class="sxs-lookup"><span data-stu-id="2cb99-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="2cb99-159">En iyi yöntemler, ölçeklenebilir ve esnek bir mimari oluşturmak gibi Azure App Service hakkında bilgi için bkz: [en iyi uygulamalar: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cb99-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="2cb99-160">Uygulama hizmeti uygulamaları ölçeklendirme hakkında daha fazla videolar için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="2cb99-160">For videos about scaling App Service apps, see hello following resources:</span></span>
  
  * [<span data-ttu-id="2cb99-161">Zaman tooScale - Stefan Schackow ile Azure Web siteleri</span><span class="sxs-lookup"><span data-stu-id="2cb99-161">When tooScale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="2cb99-162">Azure Web siteleri, CPU ölçeklendirme otomatik veya zamanlanmış - Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="2cb99-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="2cb99-163">-Stefan Schackow ile nasıl Azure Web siteleri ölçek</span><span class="sxs-lookup"><span data-stu-id="2cb99-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
