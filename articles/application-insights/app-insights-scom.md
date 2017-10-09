---
title: "Application Insights ile aaaSCOM tümleştirme | Microsoft Docs"
description: "SCOM kullanıcı değilseniz, Application Insights ile sorunlarını tanılamak ve performansını izleyebilir. Kapsamlı panoları, akıllı uyarıları, güçlü tanılama araçları ve analiz sorguları."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="0e551-104">SCOM için Application Insights kullanarak uygulama performansı izleme</span><span class="sxs-lookup"><span data-stu-id="0e551-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="0e551-105">System Center Operations Manager (SCOM) toomanage sunucularınız kullanıyorsanız, performansı izleyerek ve hello Yardımı ile performans sorunlarını tanılamanıza [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="0e551-105">If you use System Center Operations Manager (SCOM) toomanage your servers, you can monitor performance and diagnose performance issues with hello help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="0e551-106">Application Insights REST ve SQL çağrıları, özel durumlar ve günlük izlemelerini giden web uygulamanızın gelen istekleri izler.</span><span class="sxs-lookup"><span data-stu-id="0e551-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="0e551-107">Panolar ölçüm grafikler ve akıllı uyarıları yanı sıra güçlü tanılama arama ve analitik sorguları ile bu telemetri sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e551-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="0e551-108">SCOM Yönetim Paketi kullanarak Application Insights izleme geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e551-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0e551-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="0e551-109">Before you start</span></span>
<span data-ttu-id="0e551-110">Biz varsayın:</span><span class="sxs-lookup"><span data-stu-id="0e551-110">We assume:</span></span>

* <span data-ttu-id="0e551-111">Web sunucuları ile SCOM tanıdık ve IIS SCOM 2012 R2 veya 2016 toomanage kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e551-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 toomanage your IIS web servers.</span></span>
* <span data-ttu-id="0e551-112">Application Insights ile toomonitor istediğiniz bir web uygulaması sunucularınıza zaten yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="0e551-112">You have already installed on your servers a web application that you want toomonitor with Application Insights.</span></span>
* <span data-ttu-id="0e551-113">Uygulama framework .NET 4.5 veya üzeri sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="0e551-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="0e551-114">Erişim tooa abonelik sahip [Microsoft Azure](https://azure.com) ve toohello kaydolabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e551-114">You have access tooa subscription in [Microsoft Azure](https://azure.com) and can sign in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0e551-115">Kuruluşunuz bir aboneliğe sahip ve Microsoft hesabı tooit ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e551-115">Your organization may have a subscription, and can add your Microsoft account tooit.</span></span>

<span data-ttu-id="0e551-116">(Merhaba geliştirme ekip hello [Application Insights SDK'sı](app-insights-asp-net.md) hello web uygulamada.</span><span class="sxs-lookup"><span data-stu-id="0e551-116">(hello development team might build hello [Application Insights SDK](app-insights-asp-net.md) into hello web app.</span></span> <span data-ttu-id="0e551-117">Bu derleme araçları bunları özel telemetri yazma büyük esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e551-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="0e551-118">Ancak, önemli değildir: ile ya da SDK'sı yerleşik olarak hello olmadan burada açıklanan başlangıç adımları izleyebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="0e551-118">However, it doesn't matter: you can follow hello steps described here either with or without hello SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="0e551-119">(Bir saat) Application Insights Yönetimi paketini yükleyin</span><span class="sxs-lookup"><span data-stu-id="0e551-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="0e551-120">Operations Manager çalıştırdığı hello makinede:</span><span class="sxs-lookup"><span data-stu-id="0e551-120">On hello machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="0e551-121">Merhaba Yönetim Paketi herhangi bir eski sürümü kaldırın:</span><span class="sxs-lookup"><span data-stu-id="0e551-121">Uninstall any old version of hello management pack:</span></span>
   1. <span data-ttu-id="0e551-122">Operations Manager'da yönetim, yönetim paketleri açın.</span><span class="sxs-lookup"><span data-stu-id="0e551-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="0e551-123">Merhaba eski sürümünü silin.</span><span class="sxs-lookup"><span data-stu-id="0e551-123">Delete hello old version.</span></span>
2. <span data-ttu-id="0e551-124">İndirip hello Yönetim Paketi hello Kataloğu'ndan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e551-124">Download and install hello management pack from hello catalog.</span></span>
3. <span data-ttu-id="0e551-125">Operations Manager'ı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0e551-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="0e551-126">Bir yönetim paketi oluşturun</span><span class="sxs-lookup"><span data-stu-id="0e551-126">Create a management pack</span></span>
1. <span data-ttu-id="0e551-127">Operations Manager'da açmak **yazma**, **.NET Application Insights ile...**, **izleme Ekleme Sihirbazı'nı**, yeniden seçin **.NET Application Insights ile...**.</span><span class="sxs-lookup"><span data-stu-id="0e551-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="0e551-128">Uygulamanızı sonra adı hello yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="0e551-128">Name hello configuration after your app.</span></span> <span data-ttu-id="0e551-129">(Bir zamanda tooinstrument bir uygulama vardır.)</span><span class="sxs-lookup"><span data-stu-id="0e551-129">(You have tooinstrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="0e551-130">Üzerinde hello aynı sihirbaz sayfasında, ya da oluşturma yeni bir Yönetim Paketi veya Application Insights için daha önce oluşturduğunuz bir paket seçin.</span><span class="sxs-lookup"><span data-stu-id="0e551-130">On hello same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="0e551-131">(Application Insights hello [Yönetim Paketi](https://technet.microsoft.com/library/cc974491.aspx) örneği oluşturduğunuz bir şablonu.</span><span class="sxs-lookup"><span data-stu-id="0e551-131">(hello Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="0e551-132">Merhaba aynı örnek daha sonra yeniden kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="0e551-132">You can reuse hello same instance later.)</span></span>

    ![Hello genel özellikler sekmesi, hello uygulama hello adını yazın.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="0e551-136">Bir uygulama seçin toomonitor istiyor.</span><span class="sxs-lookup"><span data-stu-id="0e551-136">Choose one app that you want toomonitor.</span></span> <span data-ttu-id="0e551-137">sunucularınızda yüklü uygulamalar arasında Hello arama özelliğini arar.</span><span class="sxs-lookup"><span data-stu-id="0e551-137">hello search feature searches among apps installed on your servers.</span></span>
   
    ![Hangi tooMonitor sekmesinde Ekle'yi tıklatın, hello uygulama ad bölümünü yazın, Ara'yı tıklatın, hello uygulama ve ekleme, Tamam'ı seçin.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="0e551-139">tüm sunucuları toomonitor hello uygulamada istemiyorsanız hello isteğe bağlı izleme kapsamı alan kullanılan toospecify, sunucularınızın bir alt olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e551-139">hello optional Monitoring scope field can be used toospecify a subset of your servers, if you don't want toomonitor hello app in all servers.</span></span>
2. <span data-ttu-id="0e551-140">Merhaba sonraki sihirbaz sayfasında, kimlik bilgileri toosign tooMicrosoft Azure içinde ilk sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e551-140">On hello next wizard page, you must first provide your credentials toosign in tooMicrosoft Azure.</span></span>
   
    <span data-ttu-id="0e551-141">Bu sayfada hello Application Insights kaynağı Analiz ve görüntülenen hello telemetri verileri toobe istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="0e551-141">On this page, you choose hello Application Insights resource where you want hello telemetry data toobe analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="0e551-142">Merhaba uygulama geliştirme sırasında Application Insights için yapılandırıldıysa, var olan kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="0e551-142">If hello application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="0e551-143">Aksi takdirde, başlangıç uygulaması için adlı yeni bir kaynak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e551-143">Otherwise, create a new resource named for hello app.</span></span> <span data-ttu-id="0e551-144">Bileşenlerinin başka uygulamalar varsa hello aynı sistem put bunları hello aynı kaynak grubu, toomake erişim toohello telemetri daha kolay toomanage.</span><span class="sxs-lookup"><span data-stu-id="0e551-144">If there are other apps that are components of hello same system, put them in hello same resource group, toomake access toohello telemetry easier toomanage.</span></span>
     
     <span data-ttu-id="0e551-145">Bu ayarları daha sonra değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e551-145">You can change these settings later.</span></span>
     
     ![Application Insights Ayarlar sekmesinde, 'oturum aç' tıklayın ve Azure için Microsoft hesabı kimlik bilgilerinizi sağlayın.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="0e551-148">Tam hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="0e551-148">Complete hello wizard.</span></span>
   
    ![Oluştur’a tıklayın](./media/app-insights-scom/070.png)

<span data-ttu-id="0e551-150">Toomonitor istediğiniz her uygulama için bu yordamı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="0e551-150">Repeat this procedure for each app that you want toomonitor.</span></span>

<span data-ttu-id="0e551-151">Toochange ayarları daha sonra gerekirse hello İzleyicisi Merhaba yazma penceresinde hello özelliklerini yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="0e551-151">If you need toochange settings later, re-open hello properties of hello monitor from hello Authoring window.</span></span>

![Yazma, .NET uygulama performansı izleme Application Insights ile seçin, sizin İzleyicisi'ni seçin ve Özellikler'i tıklatın.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="0e551-153">İzleme doğrulayın</span><span class="sxs-lookup"><span data-stu-id="0e551-153">Verify monitoring</span></span>
<span data-ttu-id="0e551-154">Merhaba İzleyicisi her sunucuda yüklü uygulamanızı arar.</span><span class="sxs-lookup"><span data-stu-id="0e551-154">hello monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="0e551-155">Burada hello uygulama bulur Application Insights Durum İzleyicisi toomonitor hello uygulama yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="0e551-155">Where it finds hello app, it configures Application Insights Status Monitor toomonitor hello app.</span></span> <span data-ttu-id="0e551-156">Gerekirse, hello sunucuda ilk Durum İzleyicisi'ni yükler.</span><span class="sxs-lookup"><span data-stu-id="0e551-156">If necessary, it first installs Status Monitor on hello server.</span></span>

<span data-ttu-id="0e551-157">Merhaba uygulama hangi örneklerini bulduğu doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e551-157">You can verify which instances of hello app it has found:</span></span>

![İzleme, Application Insights açın](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="0e551-159">Application Insights telemetrisi görünümü</span><span class="sxs-lookup"><span data-stu-id="0e551-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="0e551-160">Merhaba, [Azure portal](https://portal.azure.com), uygulamanız için toohello kaynak göz atın.</span><span class="sxs-lookup"><span data-stu-id="0e551-160">In hello [Azure portal](https://portal.azure.com), browse toohello resource for your app.</span></span> <span data-ttu-id="0e551-161">[Telemetri gösteren grafikleri görmek](app-insights-dashboards.md) uygulamanızdan.</span><span class="sxs-lookup"><span data-stu-id="0e551-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="0e551-162">(Hello ana sayfasında henüz gösterilen kurmadı, Canlı ölçümleri akış'ı tıklatın.)</span><span class="sxs-lookup"><span data-stu-id="0e551-162">(If it hasn't shown up on hello main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e551-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e551-163">Next steps</span></span>
* <span data-ttu-id="0e551-164">[Bir Pano ayarlamak](app-insights-dashboards.md) toobring birlikte hello en önemli grafikleri bu ve diğer uygulamalar izleme.</span><span class="sxs-lookup"><span data-stu-id="0e551-164">[Set up a dashboard](app-insights-dashboards.md) toobring together hello most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="0e551-165">Ölçümler hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="0e551-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="0e551-166">Uyarıları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0e551-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="0e551-167">Performans sorunlarını tanılama</span><span class="sxs-lookup"><span data-stu-id="0e551-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="0e551-168">Güçlü Analytics sorgular</span><span class="sxs-lookup"><span data-stu-id="0e551-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="0e551-169">Kullanılabilirlik web testleri</span><span class="sxs-lookup"><span data-stu-id="0e551-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

