---
title: "aaaManage Azure App Service'te bir web uygulaması"
description: "Azure App Service'in web uygulamasında yönetmek için bağlantılar tooresources."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="f9333-103">Azure App Service'in web uygulamasında yönetme</span><span class="sxs-lookup"><span data-stu-id="f9333-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="f9333-104">Bu konu, bir web uygulamasını yönetmek için bağlantılar tooresources içerir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f9333-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="f9333-105">Yönetim web uygulamanız sorunsuz çalışmasını devam hello görevlerin tümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="f9333-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="f9333-106">Bir web uygulaması hello ömrü boyunca, ilk dağıtım toonormal işlemi, Bakım ve güncelleştirmelerini taşımak gibi farklı yönetim görevleri gerçekleştirmeniz gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="f9333-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="f9333-107">Birçok web uygulama yönetimi görevlerini hello Azure Portal gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="f9333-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="f9333-108">Web uygulaması tooproduction dağıtmadan önce</span><span class="sxs-lookup"><span data-stu-id="f9333-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="f9333-109">Bir katmanı seçin</span><span class="sxs-lookup"><span data-stu-id="f9333-109">Choose a tier</span></span>
<span data-ttu-id="f9333-110">Azure uygulama hizmeti beş katmanlarda sunulur: ücretsiz, paylaşılan, temel, standart ve Premium.</span><span class="sxs-lookup"><span data-stu-id="f9333-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="f9333-111">Merhaba özellikler ve her katman için fiyatlandırma hakkında daha fazla bilgi için bkz: [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="f9333-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="f9333-112">[Uygulama hizmeti planları](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) hello altında birden çok web uygulamaları Grup izin aynı katmanı.</span><span class="sxs-lookup"><span data-stu-id="f9333-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="f9333-113">Her zaman [geçiş katmanları](web-sites-scale.md) web uygulamanızı oluşturduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="f9333-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="f9333-114">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f9333-114">Configuration</span></span>
<span data-ttu-id="f9333-115">Kullanım hello [Azure Portal](https://portal.azure.com/) tooset çeşitli yapılandırma seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="f9333-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="f9333-116">Ayrıntılar için bkz [Azure App Service'te web uygulamalarını yapılandırma](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="f9333-117">Hızlı bir denetim listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="f9333-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="f9333-118">Seçin **çalışma zamanı sürümlerini** .NET, PHP, Java ya da gerekirse Python için.</span><span class="sxs-lookup"><span data-stu-id="f9333-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="f9333-119">Etkinleştirme **WebSockets** web uygulamanız hello WebSocket Protokolü kullanıyorsa.</span><span class="sxs-lookup"><span data-stu-id="f9333-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="f9333-120">(Bunu kullanan uygulamalar içeren [ASP.NET SignalR](http://www.asp.net/signalr) veya [Socket.IO](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="f9333-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="f9333-121">Sürekli web işleriniz kullanıyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="f9333-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="f9333-122">Bu durumda, etkinleştirme **her zaman açık**.</span><span class="sxs-lookup"><span data-stu-id="f9333-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="f9333-123">Set hello **varsayılan belge**, index.html gibi.</span><span class="sxs-lookup"><span data-stu-id="f9333-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="f9333-124">Toplama toothese temel yapılandırma ayarlarında tooconfigure hello aşağıdaki isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f9333-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="f9333-125">**Güvenli Yuva Katmanı (SSL)** şifreleme.</span><span class="sxs-lookup"><span data-stu-id="f9333-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="f9333-126">SSL toouse bir özel etki alanı adı ile almanız gerekir bir SSL sertifikası ve web uygulama toouse yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="f9333-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="f9333-127">Bkz: [Azure App Service'te bir web uygulaması için HTTPS'yi etkinleştir](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="f9333-128">**Özel etki alanı adı.**</span><span class="sxs-lookup"><span data-stu-id="f9333-128">**Custom domain name.**</span></span> <span data-ttu-id="f9333-129">Web uygulamanız otomatik olarak azurewebsites.net altında bir alt etki alanı vardır.</span><span class="sxs-lookup"><span data-stu-id="f9333-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="f9333-130">Bir özel etki alanı adı contoso.com gibi ilişkilendirebilirsiniz. Bkz: [Azure App Service'te özel etki alanı adı yapılandırma](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="f9333-131">Dile özgü yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="f9333-131">Language-specific configuration:</span></span>

* <span data-ttu-id="f9333-132">**PHP**: [Azure App Service Web Apps PHP yapılandırma](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="f9333-133">**Python**: [yapılandırma Python Azure uygulama hizmeti ile Web uygulamaları](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="f9333-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="f9333-134">Web uygulamanızı çalışırken</span><span class="sxs-lookup"><span data-stu-id="f9333-134">While your web app is running</span></span>
<span data-ttu-id="f9333-135">Web uygulamanızı çalışırken toomake kullanılabilir olduğundan ve toomeet kullanıcı trafiğinin ölçeklendirir istiyor.</span><span class="sxs-lookup"><span data-stu-id="f9333-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="f9333-136">Tootroubleshoot hataları da gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f9333-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="f9333-137">İzleme</span><span class="sxs-lookup"><span data-stu-id="f9333-137">Monitoring</span></span>
* <span data-ttu-id="f9333-138">Hello Azure Portal yapabilecekleriniz [performans ölçümleri eklemek](web-sites-monitor.md) CPU kullanımı ve istemci istekleri sayısı gibi.</span><span class="sxs-lookup"><span data-stu-id="f9333-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="f9333-139">[Web uygulamanız ölçeği](web-sites-scale.md) yanıt tootraffic içinde.</span><span class="sxs-lookup"><span data-stu-id="f9333-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="f9333-140">Katmanına bağlı olarak VM hello sayısını ve/veya hello VM örnekleri hello boyutunu ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9333-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="f9333-141">Web uygulamanız otomatik olarak sabit bir zamanlama ya yanıt tooload ölçeklendirir şekilde hello standart ve Premium katmanlar, otomatik ölçeklendirmeyi ayarlayalım ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9333-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="f9333-142">Yedeklemeler</span><span class="sxs-lookup"><span data-stu-id="f9333-142">Backups</span></span>
* <span data-ttu-id="f9333-143">Ayarlama [otomatik yedeklemeler](web-sites-backup.md) , web uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="f9333-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="f9333-144">Yedeklemelerin hakkında daha fazla bilgi [bu videoyu](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="f9333-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="f9333-145">Başlangıç seçenekleri hakkında bilgi edinin [veritabanı kurtarma](../sql-database/sql-database-business-continuity.md) Azure SQL veritabanında.</span><span class="sxs-lookup"><span data-stu-id="f9333-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="f9333-146">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f9333-146">Troubleshooting</span></span>
* <span data-ttu-id="f9333-147">Bir sorun yaşanırsa yapabilecekleriniz [Visual Studio'daki sorun giderme](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), tanılama günlüklerini kullanma ve hello bulutta hata ayıklama Canlı.</span><span class="sxs-lookup"><span data-stu-id="f9333-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="f9333-148">Visual Studio dışında çeşitli yolları toocollect tanılama günlükleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f9333-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="f9333-149">Bkz: [Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="f9333-150">Node.js uygulamaları için bkz: [nasıl toodebug bir Node.js web uygulamasını Azure App Service'te](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="f9333-151">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="f9333-151">Restoring Data</span></span>
* <span data-ttu-id="f9333-152">[Geri yükleme](web-sites-restore.md) daha önce yedeklenen bir web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f9333-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="f9333-153">Web uygulamanızı güncelleştirdiğinizde</span><span class="sxs-lookup"><span data-stu-id="f9333-153">When you update your web app</span></span>
<span data-ttu-id="f9333-154">Otomatik yedekleme etkinleştirmediyseniz oluşturabileceğiniz bir [el ile Yedekleme](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="f9333-155">Kullanmayı [dağıtım hazırlanan](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f9333-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="f9333-156">Bu seçenek, güncelleştirmeleri tooa yan yana çalışır dağıtım hazırlama yayımlama sağlar, Üretim dağıtımı ile.</span><span class="sxs-lookup"><span data-stu-id="f9333-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


